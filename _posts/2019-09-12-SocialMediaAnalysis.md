---
title: 'Can Social Media Help Predict a Product''s Success?'
date: 2019-09-12
permalink: /posts/2019/09/SocialMediaAnalysis/
tags:
  - NLP
  - Data Analysis
---

An NLP Analysis of Samsung Galaxy S8 vs. Apple iPhone 8 & X

Social media has revolutionized how companies market their products. With a treasure trove of consumer opinions readily available, brands can glean incredible insights into what customers love, hate, and anticipate.  But to what extent can this data be used to predict the success of a product or refine product strategies?

Our team tackled this question by analyzing consumer reviews, comments, and posts around the Samsung Galaxy S8 vs. Apple iPhone 8 and X. Using natural language processing (NLP) techniques, we aimed to uncover valuable insights.

Data
------
* Twitter: Initially 69527 rows, 41 columns; preprocessed to 22703 rows, 5 columns.
* Non-Twitter: Initially 443183 rows, 41 columns; preprocessed to 300844 rows, 5 columns.

Methodology
------
* Data Sources: We sourced data from various platforms, including blogs, forums, and social media sites (both Twitter and non-Twitter sources).
* Preprocessing: We extensively cleaned the data, removing duplicates, irrelevant posts, and social media 'noise' (e.g., slang, emoticons).
* Analysis Techniques:
  * Keyword Tagging: Identified posts related to Apple, Samsung, or both.
  * BERT/XLNET: Disambiguated untagged or confusing posts.
  * LDA Topic Modeling: Revealed key themes within the discussions.
  * Feature Detection: Extracted frequently mentioned product attributes.
  * Sentiment Analysis: Used VADER to gauge sentiment towards both products and their features, pre- and post-launch.

Key Findings
------
* **Platform Insights**: Blogs are the most popular platform for tech discussions, followed by Tumblr, Instagram, and forums. This tells us where companies should focus marketing efforts.
* **Country-Specific Preferences**: Data helped pinpoint which social media platforms are most popular in various countries, allowing for targeted campaigns.
* **Important Features**: We pinpointed the most discussed features for each product:
  * Apple: Camera, charging, display, design, price
  * Samsung: Screen, display, camera, Bixby, Android
* **Sentiment Tracking**:
  * Apple: Positive sentiment towards OLED display and wireless charging; negative sentiment towards price and removal of Touch ID.
  * Samsung: Mixed sentiment towards most features; dislike towards the dedicated Bixby button.
* **Pre vs. Post Launch Insights**: Sentiment analysis around product launches helped us identify features that were well-received or disliked, and whether consumer expectations were met.


Recommendations
------
* **Feature Development and Refinement**: Sentiment analysis pinpoints strengths and weaknesses, guiding future product iterations.
* **Targeted Marketing**: Understanding regional preferences informs marketing strategies. Additionally, companies can segment users based on whether they prioritize price, quality, or value in their product choices.
* **Production Planning**: Pre-release data can help predict product uptake, aiding in production forecasts.

Final thoughts
------
Our analysis demonstrates the value of social media listening in product development and marketing. While we didn't always uncover groundbreaking results, we experimented with cutting-edge NLP techniques.  Future studies could refine our methodologies and explore deeper segmentation of consumers based on their expressed preferences.

> Team: Maitri Vasa, Yamuna Bhaskar and me! 

References
------
* [Notebook 1, Twitter data](https://gist.github.com/pavannaidu/2f224dc2fd2836e43b60eaa2519c7c99)
* [Notebook 2, Non-Twitter data](https://gist.github.com/pavannaidu/868b0dffb0a01316a8c5a57cdf47bd6a)

