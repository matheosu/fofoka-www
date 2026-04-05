# Fofoka Website

## Context
Read these files before any changes:
- docs/FOFOKA-DESIGN-SYSTEM.md — brand identity, colors, typography, logo specs
- docs/FOFOKA-LANDING-SPEC.md — page structure, sections, i18n, components
This is the landing page for fofoka.com — an anonymous geolocation gossip app.

## Brand assets
SVG logos, icons and pins are in public/assets/. Copy from the app project if not present.

## Stack
Astro (SSG) with i18n (pt + en), deploy to Cloudflare Pages.

## Key rules
- All text comes from src/i18n/pt.json and en.json — never hardcode strings
- Landing is always dark mode (#0F0F0E background)
- Portuguese is the default language
- Responsive: mobile-first (320px → 1200px)

## Deploy
This project deploys to Cloudflare Pages.
- Use @astrojs/cloudflare adapter
- Output: static (SSG, not SSR)
- Build command: npm run build
- Output directory: dist/
- Put _redirects and _headers in public/ (Cloudflare reads them from the build output root)
- Domain: fofoka.com
