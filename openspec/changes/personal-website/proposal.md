# Proposal

## Why

mishrabhinav.com is out of date: it currently serves a bare "Hello!" page (and previously redirected to LinkedIn). The owner wants a modern, minimal personal presence that costs nothing to host and needs essentially no upkeep.

## What Changes

- Add a single-page static site (plain HTML + CSS, no framework, no build step, no JavaScript required) with a hero (name + one-line positioning), a short about blurb (2-3 sentences) and outbound links (LinkedIn, GitHub, email).
- Explicitly **not** a resume: no experience timeline, skills list or CV download.
- Support light and dark appearance via `prefers-color-scheme`, a system font stack, and a responsive, accessible layout.
- Host on Cloudflare Workers static assets (free), deployed automatically on `git push`; DNS is already on Cloudflare.
- Serve the site on one canonical hostname, with the other of apex/`www` redirecting to it via Cloudflare.
- Copy is placeholder text until the owner supplies real content (the LinkedIn profile could not be read).

## Capabilities

### New Capabilities
- `landing-page`: Content, layout, theming, responsiveness, accessibility and performance expectations of the one-page site.
- `site-delivery`: How the site is hosted and served: Cloudflare deploy-on-push, HTTPS, and canonical apex/`www` hostname handling.

### Modified Capabilities

None. There are no existing specs.

## Impact

- New files in this repo: `index.html`, a stylesheet, favicon/social preview assets, and a short README.
- External configuration (outside the repo): Cloudflare Workers project (static assets) connected to the Git repository, with `wrangler.jsonc` in the repo, custom domain binding, and a redirect rule for the non-canonical hostname.
- No runtime dependencies, package manager or build tooling.
- Open input needed from the owner: final tagline, about text, and the exact LinkedIn, GitHub and email values.
