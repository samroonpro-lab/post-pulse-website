# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/),
and this project adheres to [Semantic Versioning](https://semver.org/).

## [Unreleased]

### Fixed

- Cloudflare deploy was failing (`wrangler: not found`): `wrangler` was never a
  project dependency, only invoked at deploy time. Added it to
  `devDependencies`.
- `wrangler.jsonc` declared `"name": "astro-cloudflare"`, but the actual live
  Cloudflare Worker for this project is `post-pulse-website`. Deploying under
  the wrong name would have created a disconnected Worker instead of updating
  the live site. Renamed to match.
- Removed the `r2_buckets` binding (`R2_MEDIA` / `astro-media`) from
  `wrangler.jsonc` — R2 is not enabled on this Cloudflare account yet, which
  would fail any deploy that declares the binding. The media cleanup endpoint
  (`functions/api/cleanup.ts`) that depends on it is optional and unused
  (0 media references currently); re-add the binding once R2 is enabled and
  the bucket exists.
- Cloudflare dashboard build config: deploy command corrected to
  `npx wrangler pages deploy dist` (was a bare `wrangler pages deploy dist`,
  which failed since `wrangler` wasn't installed globally in the build image).

## [1.0.0] — 2026-06-27

Initial public template release.

### Highlights

- Astro 7 + TypeScript, Tailwind CSS v4, monochrome OKLCH design tokens
- Bilingual content (English / Indonesian) with prefix-based i18n routing
- Git-based content (Markdown) — no CMS or database
- Marketing pages, blog, and Starlight docs with Pagefind search
- Cloudflare Pages hosting with optional R2 media + secret-guarded cleanup worker
- SEO: canonical, hreflang, JSON-LD, Open Graph, sitemap, RSS, dynamic `llms.txt`
- Static contact page (mailto + OpenStreetMap embed)
