# My Astro Blog

> A production-ready personal blog built with Astro, Content Collections, Pagefind search, and Giscus comments.

## 🚀 Features

- **⚡ Fast Static Site**: Built with Astro for optimal performance
- **📝 Type-Safe Content**: Content Collections with Zod schema validation
- **🔍 Full-Text Search**: Pagefind integration for instant search
- **💬 Comments System**: Giscus powered by GitHub Discussions
- **🎨 Modern Styling**: Tailwind CSS with typography plugin
- **📱 Responsive Design**: Mobile-first responsive layout
- **🔧 Developer Experience**: TypeScript, ESLint, Prettier, and hot reload
- **📊 SEO Optimized**: RSS feeds, sitemaps, and meta tags
- **🚀 Easy Deployment**: One-click deploy to Vercel or Cloudflare Pages

## 🛠️ Tech Stack

- **Framework**: [Astro](https://astro.build/) - Static Site Generator
- **Content**: [Content Collections](https://docs.astro.build/en/guides/content-collections/) with [Zod](https://zod.dev/) validation
- **Styling**: [Tailwind CSS](https://tailwindcss.com/) + [@tailwindcss/typography](https://tailwindcss.com/docs/typography-plugin)
- **Search**: [Pagefind](https://pagefind.app/) - Static site search
- **Comments**: [Giscus](https://giscus.app/) - GitHub Discussions integration
- **Language**: [TypeScript](https://www.typescriptlang.org/) (strict mode)
- **Code Quality**: [ESLint](https://eslint.org/) + [Prettier](https://prettier.io/)
- **SEO**: [@astrojs/rss](https://docs.astro.build/en/guides/rss/) + [@astrojs/sitemap](https://docs.astro.build/en/guides/integrations-guide/sitemap/)

## 📦 Quick Start

### Prerequisites

- Node.js 18+ and pnpm
- GitHub account (for Giscus comments)

### Installation

1. **Create the project**:
   ```bash
   pnpm create astro@latest wiserabbit --template minimal
   cd wiserabbit
   ```

2. **Install dependencies**:
   ```bash
   # Core dependencies
   pnpm add @astrojs/mdx @astrojs/tailwind @astrojs/rss @astrojs/sitemap
   
   # Dev dependencies
   pnpm add -D typescript zod @types/node eslint prettier @tailwindcss/typography pagefind
   ```

3. **Add Tailwind integration**:
   ```bash
   pnpm astro add tailwind
   ```

4. **Copy the provided configuration files** (see Configuration section below)

5. **Start development server**:
   ```bash
   pnpm dev
   ```

## ⚙️ Configuration

### Core Configuration Files

**astro.config.mjs**:
```javascript
import { defineConfig } from 'astro/config';
import mdx from '@astrojs/mdx';
import tailwind from '@astrojs/tailwind';
import rss from '@astrojs/rss';
import sitemap from '@astrojs/sitemap';

export default defineConfig({
  site: 'https://example.com', // Update with your domain
  integrations: [mdx(), tailwind(), rss(), sitemap()],
  markdown: {
    shikiConfig: { theme: 'github-dark' }
  },
  experimental: {
    contentCollectionCache: true
  }
});
```

**package.json scripts**:
```json
{
  "scripts": {
    "dev": "astro dev",
    "build": "astro build",
    "postbuild": "pagefind --source dist",
    "preview": "astro preview",
    "lint": "eslint .",
    "format": "prettier -w .",
    "check": "astro check"
  }
}
```

**tsconfig.json**:
```json
{
  "extends": "astro/tsconfigs/strict",
  "compilerOptions": {
    "baseUrl": ".",
    "paths": { "@/*": ["src/*"] }
  }
}
```

### Giscus Setup

1. **Enable GitHub Discussions** on your repository
2. **Visit [giscus.app](https://giscus.app/)** to generate your configuration
3. **Update the Giscus component** with your settings:

```astro
<!-- src/components/Giscus.astro -->
<script
  src="https://giscus.app/client.js"
  data-repo="yourname/yourrepo"
  data-repo-id="REPO_ID_HERE"
  data-category="General"
  data-category-id="CATEGORY_ID_HERE"
  data-mapping="pathname"
  data-strict="0"
  data-reactions-enabled="1"
  data-emit-metadata="0"
  data-input-position="bottom"
  data-theme="dark"
  data-lang="en"
  crossorigin="anonymous"
  async>
</script>
```

## 📁 Project Structure

```
/
├── public/                 # Static assets
├── src/
│   ├── components/         # Reusable Astro components
│   │   ├── Header.astro
│   │   ├── Footer.astro
│   │   ├── PostCard.astro
│   │   ├── Search.astro
│   │   └── Giscus.astro
│   ├── content/           # Content Collections
│   │   ├── blog/          # Blog posts (MD/MDX)
│   │   └── config.ts      # Content schema
│   ├── layouts/           # Page layouts
│   │   ├── BaseLayout.astro
│   │   └── PostLayout.astro
│   ├── pages/             # File-based routing
│   │   ├── index.astro    # Homepage
│   │   ├── about.astro    # About page
│   │   ├── rss.xml.ts     # RSS feed
│   │   └── blog/
│   │       ├── index.astro     # Blog listing
│   │       └── [slug].astro    # Individual posts
│   └── styles/
│       └── global.css     # Global styles
├── astro.config.mjs       # Astro configuration
├── tailwind.config.mjs    # Tailwind configuration
├── tsconfig.json          # TypeScript configuration
├── .eslintrc.cjs          # ESLint configuration
├── .prettierrc            # Prettier configuration
└── package.json
```

## ✍️ Writing Content

### Creating Blog Posts

1. **Create a new file** in `src/content/blog/` with `.md` or `.mdx` extension
2. **Add frontmatter** with required fields:

```markdown
---
title: "Your Post Title"
description: "A compelling description for SEO and previews"
pubDate: 2024-01-15
tags: ["astro", "web-development"]
heroImage: "/images/hero.jpg" # Optional
draft: false # Set to true to hide from production
---

Your content goes here...
```

### Frontmatter Schema

All frontmatter is validated using Zod:

- `title`: string (required)
- `description`: string, min 10 characters (required)
- `pubDate`: date (required)
- `updatedDate`: date (optional)
- `tags`: array of strings (optional, defaults to [])
- `heroImage`: string (optional)
- `draft`: boolean (optional, defaults to false)

## 🚀 Deployment

### Vercel Deployment

1. **Push your code** to GitHub
2. **Connect your repository** to Vercel
3. **Configure build settings**:
   - Build Command: `pnpm build`
   - Output Directory: `dist`
   - Install Command: `pnpm install`
4. **Add environment variables** if needed
5. **Deploy** - Vercel will automatically run the postbuild script

### Cloudflare Pages Deployment

1. **Push your code** to GitHub
2. **Connect your repository** to Cloudflare Pages
3. **Configure build settings**:
   - Build Command: `pnpm build && pnpm postbuild`
   - Build Output Directory: `dist`
   - Root Directory: `/`
4. **Deploy**

### GitHub Actions CI/CD

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to Production

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: pnpm/action-setup@v2
        with:
          version: 8
      - uses: actions/setup-node@v4
        with:
          node-version: 18
          cache: 'pnpm'
      
      - name: Install dependencies
        run: pnpm install
      
      - name: Run linting
        run: pnpm lint
      
      - name: Run type checking
        run: pnpm check
      
      - name: Build site
        run: pnpm build
      
      - name: Generate search index
        run: pnpm postbuild
```

## 🔧 Development

### Available Scripts

- `pnpm dev` - Start development server with hot reload
- `pnpm build` - Build for production
- `pnpm postbuild` - Generate Pagefind search index
- `pnpm preview` - Preview production build locally
- `pnpm lint` - Run ESLint
- `pnpm format` - Format code with Prettier
- `pnpm check` - Run Astro type checking

### Development Workflow

1. **Start the dev server**: `pnpm dev`
2. **Write your content** in `src/content/blog/`
3. **Test search functionality** by running `pnpm build && pnpm postbuild && pnpm preview`
4. **Lint and format** before committing: `pnpm lint && pnpm format`
5. **Type check** your code: `pnpm check`

## 🎨 Customization

### Styling

- **Colors**: Modify `tailwind.config.mjs` to change the color scheme
- **Typography**: Customize the `@tailwindcss/typography` plugin settings
- **Components**: Edit Astro components in `src/components/`
- **Layouts**: Modify layouts in `src/layouts/`

### Site Metadata

Update these placeholders throughout the codebase:

- **Site Title**: "My Astro Blog" → Your site name
- **Site Description**: "Thoughts, guides, and notes" → Your description
- **Site URL**: `https://example.com` → Your domain
- **Author**: "Your Name" → Your name
- **Giscus Config**: Update with your repository details

## 📚 Key Components

### Search Component (`src/components/Search.astro`)

Integrates Pagefind for client-side search:

```astro
---
const { placeholder = 'Search posts…' } = Astro.props;
---
<link rel="stylesheet" href="/pagefind/pagefind-ui.css" />
<div id="search" class="my-6" />
<script src="/pagefind/pagefind-ui.js" defer></script>
<script>
  document.addEventListener('DOMContentLoaded', () => {
    new PagefindUI({
      element: '#search',
      showSubResults: true,
      showImages: true,
      translations: {
        search_placeholder: { default: placeholder }
      }
    });
  });
</script>
```

### Post Card Component (`src/components/PostCard.astro`)

Reusable component for displaying post previews:

```astro
---
interface Props {
  href: string;
  title: string;
  description: string;
  date: Date;
  tags?: string[];
}
const { href, title, description, date, tags = [] } = Astro.props;
---
<li class="group">
  <a href={href} class="block">
    <h2 class="text-xl font-semibold group-hover:underline">{title}</h2>
    <p class="text-sm text-zinc-400">{date.toDateString()}</p>
    <p class="mt-1 text-zinc-300">{description}</p>
    {tags.length > 0 && (
      <div class="mt-2 flex flex-wrap gap-2 text-xs text-zinc-300">
        {tags.map((t) => <span class="rounded bg-zinc-800 px-2 py-1">{t}</span>)}
      </div>
    )}
  </a>
</li>
```

## 🐛 Troubleshooting

### Common Issues

**Search not working after build**:
- Ensure `postbuild` script runs after `build`
- Check that `/pagefind/` directory exists in `dist/`
- Verify Pagefind CLI is installed: `pnpm add -D pagefind`

**Giscus comments not loading**:
- Verify GitHub Discussions is enabled on your repository
- Double-check your Giscus configuration values
- Ensure the repository is public or you have proper permissions

**TypeScript errors**:
- Run `pnpm check` to see detailed type errors
- Ensure all frontmatter follows the Zod schema
- Check that Content Collections are properly configured

**Build failures**:
- Clear cache: `rm -rf node_modules/.astro`
- Reinstall dependencies: `rm -rf node_modules && pnpm install`
- Check for syntax errors in `.astro` files

## 📄 License

MIT License - feel free to use this template for your own projects!

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

**Happy blogging!** 🎉