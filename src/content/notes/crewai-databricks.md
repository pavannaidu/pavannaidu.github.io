---
title: 'Running CrewAI with Databricks-Hosted LLMs'
date: 2026-02-07
description: 'How to run CrewAI multi-agent workflows on Databricks using hosted foundation models instead of OpenAI, with LiteLLM and MLflow tracing.'
tags:
  - CrewAI
  - Databricks
  - LLM
  - AI Agents
  - MLflow
---

Most CrewAI tutorials assume you're using OpenAI. But if your organization runs on Databricks and you already have foundation models served through Model Serving endpoints, there's no reason to add another vendor. CrewAI supports Databricks-hosted LLMs natively through LiteLLM, and the setup is straightforward.

This post walks through running a multi-agent CrewAI workflow entirely on Databricks, using a hosted Meta Llama 3.3 70B model — no OpenAI API key required.

## Why Databricks Instead of OpenAI?

- **Data governance** — your prompts and responses stay within your Databricks workspace
- **Cost control** — use pay-per-token foundation model APIs or provisioned throughput
- **Observability** — MLflow tracing captures the full agent execution pipeline
- **No external dependencies** — everything runs inside your existing infrastructure

## The Setup

CrewAI uses [LiteLLM](https://docs.litellm.ai/) under the hood to connect to LLMs. LiteLLM supports Databricks Model Serving endpoints with the `databricks/` model prefix. This means you can point CrewAI at any model served through Databricks — DBRX, Llama, Mixtral, or any custom model you've deployed.

### Install Dependencies

From a Databricks notebook:

```python
%pip install crewai crewai-tools litellm mlflow apscheduler 'pydantic[email]' --quiet
dbutils.library.restartPython()
```

### Configure Authentication

The key step is pulling your workspace URL and token from the notebook context, then setting them as environment variables that LiteLLM expects:

```python
import os
import mlflow
from crewai import Agent, Task, Crew, Process, LLM

# Enable MLflow tracing for CrewAI
mlflow.crewai.autolog()

# Get Databricks workspace URL and token from the notebook context
workspace_url = spark.conf.get("spark.databricks.workspaceUrl")
token = dbutils.notebook.entry_point.getDbutils().notebook().getContext().apiToken().get()

# Set environment variables for Databricks authentication
os.environ["DATABRICKS_HOST"] = f"https://{workspace_url}"
os.environ["DATABRICKS_TOKEN"] = token

# Prevent any accidental OpenAI API calls
os.environ["OPENAI_API_KEY"] = "NA"
```

Setting `OPENAI_API_KEY` to `"NA"` is a safety net — it ensures that if any part of the pipeline defaults to OpenAI, it fails fast rather than silently sending data externally.

### Configure the LLM

```python
model_name = "databricks-meta-llama-3-3-70b-instruct"

databricks_llm = LLM(
    model=f"databricks/{model_name}",
    api_base=f"https://{workspace_url}/serving-endpoints",
    api_key=token,
    temperature=0.7
)
```

The `databricks/` prefix tells LiteLLM to route requests to your Databricks serving endpoint. The `api_base` points directly at your workspace's serving infrastructure.

## Building the Multi-Agent Workflow

With the LLM configured, you can create agents exactly as you would with OpenAI — just pass `databricks_llm` instead:

```python
researcher = Agent(
    role='Data Researcher',
    goal='Find and explain information about the topic',
    backstory='You are an expert researcher with deep domain knowledge.',
    llm=databricks_llm,
    verbose=True,
    allow_delegation=False
)
```

### A Trip Planning Example

The full notebook demonstrates a trip planning crew with two specialized agents — a City Selection Expert and a Local Expert — that collaborate to produce a travel guide:

```python
class TripAgents:
    def __init__(self, llm):
        self.llm = llm

    def city_selection_agent(self):
        return Agent(
            role="City Selection Expert",
            goal="Select the best city based on weather, season, and prices",
            backstory="An expert in analyzing travel data to pick ideal destinations.",
            llm=self.llm,
            verbose=True,
            allow_delegation=False
        )

    def local_expert(self):
        return Agent(
            role="Local Expert at this city",
            goal="Provide the BEST insights about the selected city",
            backstory="A knowledgeable local guide with extensive information "
                      "about the city, its attractions and customs.",
            llm=self.llm,
            verbose=True,
            allow_delegation=False
        )
```

The crew is assembled and executed like any standard CrewAI setup. The only difference is that `memory=False` is set to avoid the default OpenAI embeddings dependency:

```python
crew = Crew(
    agents=[city_selector_agent, local_expert_agent],
    tasks=[identify_task, gather_task],
    verbose=True,
    memory=False,  # Avoids OpenAI embeddings dependency
    manager_llm=databricks_llm,
)

result = crew.kickoff()
```

## Things to Watch Out For

**Memory and embeddings** — CrewAI's memory feature defaults to OpenAI embeddings. If you enable `memory=True`, you'll need to configure a custom embedder that uses your Databricks-hosted embedding model. Otherwise, keep it disabled.

**Instruct mode alternation** — Some Databricks-served models enforce strict user/assistant message alternation. If you hit an error about "Chat message input roles must alternate", you may need to adjust the model or use LiteLLM's `user_continue_message` parameter.

**External tools** — Tools like `SerperDevTool` or `WebsiteSearchTool` require external API access. In restricted Databricks environments, you may need to rely on the LLM's built-in knowledge or use Databricks-native tools like `DatabricksQueryTool` for SQL-based lookups.

## MLflow Tracing

One advantage of running on Databricks is automatic observability. With `mlflow.crewai.autolog()`, every agent interaction, task execution, and LLM call is captured as an MLflow trace. This gives you full visibility into what each agent did, how long it took, and what tokens were consumed — all viewable in the MLflow UI within your workspace.

## Full Notebook

The complete working notebook is available as a GitHub Gist:

[CrewAI with Databricks Hosted Model — Notebook](https://gist.github.com/pavannaidu/a61c25fe76b07601bee4aa5138aefffe)

## References

- [CrewAI LLM Connections Docs](https://docs.crewai.com/en/learn/llm-connections)
- [LiteLLM + Databricks Guide](https://community.databricks.com/t5/technical-blog/simplifying-multi-model-llm-development-a-developer-s-guide-to/ba-p/80623)
- [Databricks Model Serving](https://docs.databricks.com/aws/en/machine-learning/model-serving)
- [MLflow CrewAI Tracing](https://docs.databricks.com/aws/en/mlflow3/genai/tracing/integrations/crewai)
- [Databricks Community Post](https://community.databricks.com/t5/generative-ai/how-to-use-crewai-with-databricks-hosted-llms-not-openai/td-p/144612)
