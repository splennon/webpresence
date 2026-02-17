# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hugo static site for **overworld.org** — Stephen Lennon's personal blog/portfolio. Uses the **Beautiful Hugo** theme (git submodule in `themes/beautifulhugo/`).

## Build & Deploy Commands

```bash
# Build the site (output goes to public/)
hugo

# Local development server with live reload
hugo server

# Deploy to production (AWS S3 + CloudFront)
bash upload.sh
```

Hugo version: v0.140.1+extended (installed via Homebrew).

## Architecture

- **config.toml** — Main Hugo configuration: site metadata, menu structure, author info, analytics, theme params
- **content/post/** — Blog posts, each in its own directory with `index.md` + local images. Frontmatter uses YAML (title, date, categories, tags)
- **static/** — Self-hosted assets: CSS (`css/main.css`, `css/fonts.css`), JS (`js/main.js`), 86 font files, and images
- **layouts/** — Custom overrides that take precedence over the theme:
  - `partials/head.html` — Custom `<head>` with SEO, manifest, analytics, font loading, PhotoSwipe
  - `partials/nav.html` — Custom navigation with multi-level dropdown support
  - `shortcodes/dd.html` — Converts `<ul>/<li>` markup into `<dl>/<dt>/<dd>` definition lists
- **themes/beautifulhugo/** — Git submodule; do not edit directly
- **public/** — Generated output (do not edit; rebuilt by `hugo`)

## Key Customizations

- **Dark mode**: CSS `prefers-color-scheme: dark` support in `static/css/main.css`
- **Fonts**: Self-hosted Google Fonts (Fira Sans Extra Condensed, Advent Pro, Hind Madurai, Mate SC, Oswald, Poppins) via `static/css/fonts.css`
- **Bootstrap 3.3.7**: Loaded from CDN with SRI hash in `layouts/partials/head.html`
- **PhotoSwipe**: Image gallery integration loaded in the custom head partial
- **Syntax highlighting**: Pygments/Chroma with `trac` style, class-based (server-side rendered)

## Content Conventions

- New posts go in `content/post/<slug>/index.md` with images alongside
- Use the `dd` shortcode for definition lists
- Posts are organized by tags and categories; menu routes to tag-based filtered views
