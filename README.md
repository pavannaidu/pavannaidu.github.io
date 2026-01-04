# Personal Website

![Deploy Status](https://github.com/pavannaidu/pavannaidu.github.io/actions/workflows/deploy.yml/badge.svg)

A modern personal website built with Astro and Tailwind CSS, featuring a clean design with dark mode support.

## 🚀 Features

- **Modern Stack**: Built with Astro, Tailwind CSS, and TypeScript
- **Dark Mode**: Automatic theme switching with localStorage persistence
- **Content Collections**: Type-safe content management for notes and gallery items
- **Responsive Design**: Mobile-first approach that works on all devices
- **View Transitions**: Smooth page navigation with Astro's View Transitions
- **Optimized Performance**: Fast loading times and minimal JavaScript

## 📁 Project Structure

```
├── public/              # Static assets (images, files)
├── src/
│   ├── components/      # Reusable UI components
│   ├── content/        # Content collections
│   │   ├── notes/      # Blog posts and articles
│   │   └── gallery/    # Photography and projects
│   ├── data/           # Site configuration
│   ├── layouts/        # Page layouts
│   ├── pages/          # Route pages
│   └── styles/         # Global styles
├── astro.config.mjs    # Astro configuration
├── tailwind.config.mjs # Tailwind CSS configuration
└── tsconfig.json       # TypeScript configuration
```

## 🛠️ Development

### Prerequisites

- Node.js 20 or higher
- npm

### Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/pavannaidu/pavannaidu.github.io.git
   cd pavannaidu.github.io
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the development server**
   ```bash
   npm run dev
   ```

   The site will be available at `http://localhost:4321`

### Available Commands

| Command | Action |
|---------|--------|
| `npm install` | Install dependencies |
| `npm run dev` | Start local dev server at `localhost:4321` |
| `npm run build` | Build production site to `./dist/` |
| `npm run preview` | Preview built site locally |

## 📝 Content Management

### Adding Notes

Create a new markdown file in `src/content/notes/`:

```markdown
---
title: 'Your Note Title'
date: 2024-01-01
description: 'A brief description'
tags:
  - Tag1
  - Tag2
draft: false
---

Your content here...
```

### Adding Gallery Items

Create a new markdown file in `src/content/gallery/`:

```markdown
---
title: 'Gallery Item Title'
date: 2024-01-01
description: 'Description'
image: '/images/your-image.jpg'
imageAlt: 'Image description'
technologies:
  - Tech1
  - Tech2
---

Additional content...
```

## 🚢 Deployment

The site automatically deploys to GitHub Pages when you push to the `master` branch. The deployment workflow:

1. Builds the Astro site
2. Uploads the build artifact
3. Deploys to GitHub Pages

View the live site at: **https://pavannaidu.github.io/**

## 🎨 Customization

### Site Configuration

Edit `src/data/siteConfig.ts` to update:
- Site metadata (title, description, author)
- Navigation menu items
- Social media links

### Styling

- Global styles: `src/styles/global.css`
- Tailwind config: `tailwind.config.mjs`
- Color scheme: Defined in Tailwind config with CSS variables for dark mode

## 📄 License

This project is built from scratch using modern web technologies. Feel free to fork and customize for your own use.

## 🙏 Acknowledgments

Built with:
- [Astro](https://astro.build) - Static site framework
- [Tailwind CSS](https://tailwindcss.com) - Utility-first CSS framework
- [TypeScript](https://www.typescriptlang.org) - Type safety
