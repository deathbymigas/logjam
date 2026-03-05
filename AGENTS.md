# AGENTS.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Commands

```bash
npm run dev       # Start dev server at localhost:4321
npm run build     # Build production site to ./dist/
npm run preview   # Preview the production build locally
```

No linting or test runners are configured.

## Architecture

**Logjam** is an Astro v5 static site — a contact/landing page with a textured, glitch-aesthetic visual style. It uses Astro's file-based routing and component model with vanilla CSS (no UI framework adapters or content collections).

### Routing & Pages

- `src/pages/index.astro` — Landing page with the Logo and ContactForm.
- `src/pages/confirmation.astro` — Post-submission confirmation page.

### Layout

`src/layouts/Layout.astro` wraps all pages. It defines global CSS custom properties (colors, shadows, fonts, texture size) on `:root` and loads the Google Font "Gasoek One" used for display headings.

### Components

All components use scoped `<style>` blocks. The visual style relies on grain texture overlays (`public/textures/`) applied via `::after` pseudo-elements or dedicated `<span>` elements with `mix-blend-mode: screen`.

- **ContactForm** — A Netlify Forms–powered `<form>` (`data-netlify="true"`) that POSTs to `/confirmation`. Contains a `<script>` block for client-side email validation and field state management (CSS classes `field--inactive`, `field--active`, `field--error`).
- **FormField** — Email input with three visual states (`active`, `inactive`, `error`) driven by CSS classes.
- **TextBox** — Textarea with a live character counter (client-side `<script>`).
- **Button** — Renders as `<a>` when `href` is provided, `<button>` otherwise. Has three variants: `enabled`, `disabled`, `small`.
- **Logo** — Purely presentational; large "L" block + "LOGJAM" wordmark.

### Key Conventions

- TypeScript is configured with Astro's strict preset (`astro/tsconfigs/strict`).
- Component props are typed with `interface Props` in the frontmatter.
- CSS custom properties in `Layout.astro` (e.g. `--color-dark`, `--font-display`, `--shadow-glitch`, `--texture-size`) are the single source of truth for theming. Use these rather than hardcoding values.
- Client-side interactivity is done with inline `<script>` blocks in components (no JS framework), querying the DOM directly.
- Fixed-width layout: components are sized to 390px.
