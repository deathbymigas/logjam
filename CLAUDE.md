# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev       # Start dev server at localhost:4321
npm run build     # Build production site to ./dist/
npm run preview   # Preview the production build locally
```

No linting or test runners are configured yet.

## Architecture

**Logjam** is an [Astro](https://astro.build) static site (v5). The project uses Astro's file-based routing and component model with vanilla CSS scoped to each component.

- `src/pages/` — File-based routes. Each `.astro` file becomes a URL path.
- `src/layouts/` — Reusable HTML shell templates (e.g., `Layout.astro` wraps pages with `<html>`, `<head>`, global styles).
- `src/components/` — Reusable UI components with scoped `<style>` blocks.
- `src/assets/` — Images/SVGs imported as ES modules (Astro optimizes these at build time).
- `public/` — Static files copied verbatim to `dist/` (favicons, etc.).

TypeScript is configured with Astro's strict preset (`tsconfig.json` extends `astro/tsconfigs/strict`).

No content collections, integrations, or UI framework adapters are configured yet—the project is a clean baseline ready to extend.
