# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static website hosted on Cloudflare Workers. The project serves HTML/CSS content from the `public/` directory using Cloudflare's Assets feature. There is no backend Worker logic - just static file serving with custom domain routing.

## Technology Stack

- **Runtime**: Cloudflare Workers
- **Package Manager**: Bun 1.3.0 (required)
- **Build Tool**: Wrangler (Cloudflare's CLI)
- **Formatting**: Prettier

## Development Commands

Install dependencies:

```bash
bun install
```

Start local development server:

```bash
bun run dev
# or
wrangler dev
```

Format code:

```bash
bun run fix        # Auto-fix formatting issues
bun run check      # Check for formatting issues without fixing
```

Build for production:

```bash
bun run build
# or
wrangler build
```

Deploy to Cloudflare:

```bash
bun run deploy
# or
wrangler deploy
```

## Architecture

### Static Assets

- All static content lives in `public/`
- `index.html` - Main homepage with hero section featuring logo and GitHub link
- `boringbin.svg` - Icon
- `main.css` - Global styles using Inter font and a minimal color system

### Cloudflare Configuration

- Configuration is in `wrangler.jsonc`
- Assets are served from `./public` directory
- Custom domain: `boringbin.com`
- Observability is enabled for monitoring

### CI/CD

Two GitHub Actions workflows run on push/PR to main:

- `build.yaml` - Runs `bun run build` to verify the project builds
- `check.yaml` - Runs `bun check` to verify Prettier formatting
- `typos.yaml` - Checks for typos in specific files (LICENSE, README.md, package.json, public/)

## File Structure

```
.
├── public/           # Static assets served by Cloudflare Workers
│   ├── index.html
│   ├── boringbin.svg
│   └── main.css
├── wrangler.jsonc   # Cloudflare Workers configuration
├── package.json     # Project dependencies and scripts
└── typos.toml       # Typo checker configuration
```

## Design System

The site uses a minimal design system with CSS custom properties that adapt to color scheme preferences:

- **Fonts**: Inter (sans-serif) loaded from Google Fonts, with system font fallbacks
- **Colors**: Three semantic color variables (`--foreground-color`, `--background-color`, `--accent-color`)
- **Dark Mode**: Automatically adapts based on `prefers-color-scheme`
- **Layout**: Flexbox-based centered hero layout with responsive padding
