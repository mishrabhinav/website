# Tasks

## 1. Page structure and content

- [x] 1.1 Create `public/index.html` with semantic landmarks (`header`, `main`, `footer`), one `h1`, `lang="en"`, hero, about (≤3 sentences) and links area (LinkedIn, GitHub, `mailto:`); verify the page renders in a browser and contains no resume sections
- [x] 1.2 Add title, meta description, Open Graph/Twitter tags and favicon link; verify with a local link-preview/meta inspection that each tag is present
- [x] 1.3 Add `public/favicon.svg` and a 1200×630 `public/og.png`; verify both files load from the local server and `og.png` is under 100 KB
- [x] 1.4 Confirm final tagline, about text and link URLs with the owner and replace all placeholders; verify `grep -ri "placeholder\|TODO" public/` returns nothing

## 2. Styling

- [x] 2.1 Create `public/style.css` with system font stack, CSS custom properties, centered max-width column and fluid type; verify the page is legible at 320px, 768px and 1440px with no horizontal scroll
- [x] 2.2 Add `color-scheme: light dark` and `prefers-color-scheme: dark` overrides; verify both themes by toggling the OS/devtools emulation and checking contrast ≥ 4.5:1
- [x] 2.3 Add visible `:focus-visible` styles and sufficient tap targets for links; verify by tabbing through the page with the keyboard

## 3. Quality checks

- [x] 3.1 Run Lighthouse (mobile) against the local site; verify Performance, Accessibility, Best Practices and SEO all score ≥ 95
- [x] 3.2 Verify first load makes only same-origin requests and transfers under 100 KB (devtools Network tab, cache disabled), and that the page works with JavaScript disabled

## 4. Deployment config and docs

- [x] 4.1 Add `public/_headers` with CSP (`default-src 'self'`), `X-Content-Type-Options` and `Referrer-Policy`; verify after deploy with `curl -I` that headers are returned and the page still renders without CSP console errors
- [x] 4.2 Write `README.md` covering how to edit content, preview locally (`python3 -m http.server -d public`), and deploy; verify the documented preview command works as written
- [x] 4.3 Initialize git hygiene (`.gitignore`), commit, and push to a GitHub repository; verify the remote shows the `public/` files on `main`

## 5. Cloudflare Pages and domain cutover

- [x] 5.1 Create the Cloudflare Pages project from the repo (production branch `main`, no build command, output dir `public`); verify the `*.pages.dev` URL serves the site
- [ ] 5.2 Attach `mishrabhinav.com` as the custom domain; verify `curl -I https://mishrabhinav.com/` returns 200 with a valid certificate
- [ ] 5.3 Add a proxied `www` DNS record and a Redirect Rule `www.mishrabhinav.com/*` → `https://mishrabhinav.com/${1}` (301); remove any stale apex → www redirect or page rule; verify `curl -I https://www.mishrabhinav.com/` returns 301 to the apex and the apex does not redirect
- [ ] 5.4 Enable "Always Use HTTPS"; verify `curl -I http://mishrabhinav.com/` redirects to HTTPS
- [ ] 5.5 Verify the push-to-deploy flow: change the tagline, push to `main`, and confirm the live site updates; also verify link previews on the live URL with a preview debugger

## Workflow follow-up

- Archive the change after the live site is verified.
