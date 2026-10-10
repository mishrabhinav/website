# Design

## Context

The repo is empty apart from OpenSpec scaffolding. The domain's DNS is already on Cloudflare, and `mishrabhinav.com` currently 301s to `www.mishrabhinav.com`, which serves a stub "Hello!" page. See proposal.md for motivation.

## Goals / Non-Goals

**Goals:**
- Zero build tooling and zero runtime dependencies: the repo's deployable output is the source files themselves.
- Fast, accessible, dark-mode-aware page that is easy to edit by hand.

**Non-Goals:**
- Blog, CMS, analytics, contact form, or any server-side logic.
- Resume/CV content.

## Decisions

**Plain HTML + CSS, no framework or build step.** A single `public/index.html` plus `public/style.css`. Alternatives: Astro/Next (adds Node toolchain and dependency upkeep, contradicting "low maintenance"); a single file with inline CSS (fewer requests, but a separate stylesheet keeps editing simple and the size is negligible).

**Cloudflare Workers static assets with Git integration.** Cloudflare now steers new static sites to Workers rather than Pages, so the site is a Worker with no code, serving `public/` as static assets (config in `wrangler.jsonc`). Production branch `main`, no build command. Alternative: Pages (legacy, same features for this use). DNS is already on Cloudflare, so the custom domain attaches with automatic records and managed TLS. Alternative: GitHub Pages (also free, but DNS/redirect rules would be split across two vendors).

**Canonical host: apex `mishrabhinav.com`.** Cloudflare Redirect Rule sends `www` to apex with 301 preserving path and query. `www` needs a proxied DNS record (e.g. a dummy `AAAA 100::`) so the rule can fire. Alternative: `www` canonical (apex needs CNAME flattening, which Cloudflare supports, but shorter URL is nicer for a personal domain). The old registrar/redirect configuration that produces the current apex → www 301 must be removed or overridden.

**Styling.** System font stack, CSS custom properties for colors, `@media (prefers-color-scheme: dark)` overrides, `color-scheme: light dark`, fluid type via `clamp()`, a centered max-width column. No JS, no web fonts, so zero third-party requests.

**Metadata and assets.** Inline SVG favicon (`public/favicon.svg`), a static 1200×630 `public/og.png` for link previews, plus title, description, OG and Twitter meta tags. Security headers via `public/_headers` (CSP `default-src 'self'`, `X-Content-Type-Options`, `Referrer-Policy`).

**Placeholder content.** Copy ships as clearly marked placeholders (name known, tagline/about/links to be confirmed) and is finalized by the owner before go-live.

## Risks / Trade-offs

- [Placeholder copy goes live] → Task list gates DNS cutover on the owner confirming the content.
- [Existing apex → www redirect conflicts with new rules] → Inspect current Cloudflare redirect/page rules and registrar forwarding before cutover; remove stale ones.
- [Strict CSP blocks a future inline script/style] → Keep CSS external and note the constraint in the README.
- [Old `www` cached 301s in browsers] → Low impact; the new `www` → apex 301 is the same family of redirect.

## Migration Plan

1. Build and verify the site locally.
2. Push to GitHub; create the Workers project and verify on the `*.workers.dev` URL.
3. Attach `mishrabhinav.com` as the custom domain, add the `www` record and redirect rule, remove stale redirects.
4. Verify HTTPS, the redirect behavior and the previews on the live domain.
5. Rollback: roll back to the previous deployment in the Worker's Deployments tab (instant), or remove the custom domain binding.
