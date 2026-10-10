# mishrabhinav.com

A one-page static personal site. Plain HTML and CSS, no build step, no dependencies.

## Edit

- Content: `public/index.html` (search for `TODO`).
- Styling: `public/style.css` (light/dark via `prefers-color-scheme`).
- Headers: `public/_headers` (CSP is `default-src 'self'`, so keep CSS external and avoid inline scripts or third-party resources).

## Preview locally

```sh
python3 -m http.server -d public 8000
# open http://localhost:8000
```

## Deploy

Hosted on Cloudflare Workers (static assets, config in `wrangler.jsonc`): production branch `main`, no build command, assets served from `public`.
Pushing to `main` deploys automatically. `www.mishrabhinav.com` 301-redirects to `mishrabhinav.com` via a Cloudflare Redirect Rule.

## Credits

Headings use [Source Serif 4](https://github.com/adobe-fonts/source-serif) (Copyright Adobe), licensed under the SIL Open Font License 1.1. The self-hosted latin subset and license text are in `public/fonts/` (see [`public/fonts/OFL.txt`](public/fonts/OFL.txt)). The visual style is original; it does not use any Anthropic or Claude logos, marks or fonts and is not affiliated with Anthropic.
