# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

```bash
# Install dependencies
npm install

# Run local development server (localhost:4321 with hot reload)
npm run dev

# Build production site
npm run build

# Preview production build
npm run preview
```

## Architecture

This is an Astro static site with Tailwind CSS, hosted on GitHub Pages.

**Configuration:**
- `astro.config.mjs` - Astro configuration
- `tailwind.config.mjs` - Tailwind CSS with dark mode and typography plugin
- `src/data/siteConfig.ts` - Site metadata, author info, navigation

**Content Collections (src/content/):**
- `blog/` - Blog posts (markdown with frontmatter: title, date, description, tags, image)
- `portfolio/` - Portfolio items (markdown with frontmatter: title, date, description, image, technologies)
- `config.ts` - Zod schemas for content validation

**Components (src/components/):**
- `BaseHead.astro` - Meta tags, fonts, dark mode script
- `Header.astro` - Navigation with mobile menu
- `Footer.astro` - Social links
- `ThemeToggle.astro` - Dark/light mode toggle
- `BlogCard.astro` / `PortfolioCard.astro` - Content cards
- `TagList.astro` - Tag display component

**Layouts (src/layouts/):**
- `BaseLayout.astro` - Root layout with ViewTransitions and search modal
- `BlogPostLayout.astro` - Blog post layout
- `PortfolioLayout.astro` - Portfolio item layout

**Pages (src/pages/):**
- `index.astro` - Homepage
- `blog/` - Blog listing and posts
- `portfolio/` - Portfolio listing and items
- `cv.astro` - CV/Resume page
- `tags/` - Tag listing and filtered views
- `404.astro` - Error page

**Static Assets (public/):**
- `images/` - Image files
- `favicon.ico` - Site favicon

## Features

- **View Transitions** - Smooth page navigation
- **Dark Mode** - Toggle with localStorage persistence
- **Search** - Pagefind static search (Cmd+K to open)
- **Responsive** - Mobile-first design with Tailwind

## Deployment

GitHub Actions workflow (`.github/workflows/deploy.yml`) automatically builds and deploys to GitHub Pages on push to master.
