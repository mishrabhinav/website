# Tasks

## 1. Font assets and licensing

- [x] 1.1 Download the Source Serif 4 latin variable woff2 (from `@fontsource-variable/source-serif-4`) into `public/fonts/` and add its `OFL.txt`; verify both files exist, the woff2 is under 60 KB, and `OFL.txt` names Source Serif 4
- [x] 1.2 Add the font credit and license note to `README.md`; verify the README names the font, its license and links to the license file

## 2. Styling

- [x] 2.1 Add the `@font-face` (swap, latin `unicode-range`) and a Georgia/Times fallback stack to `public/style.css`, and add the preload link to `public/index.html`; verify in devtools that the font loads from the same origin and the page remains readable with the font request blocked
- [x] 2.2 Replace the palette tokens with the warm light and dark values from design.md, using a deeper clay for accent text; verify every text/background pair is at least 4.5:1 in both themes with a contrast check script or Lighthouse
- [x] 2.3 Apply the serif to `h1`, tagline and `h2`s, refine hero size, reading measure, spacing and link pill hover/focus in clay; verify visually at 320px, 768px and 1440px in light and dark with no horizontal overflow (puppeteer scrollWidth equals clientWidth)
- [x] 2.4 Add `Cache-Control: public, max-age=31536000, immutable` for `/fonts/*` to `public/_headers`; verify the file parses (a path block with the header) and that the CSP line is unchanged

## 3. Assets

- [x] 3.1 Recolor `public/favicon.svg` to the clay accent; verify it renders in a browser tab and uses no Anthropic or Claude mark
- [x] 3.2 Regenerate `public/og.png` (1200×630, new palette and serif, rendered from a temporary HTML card via headless Chrome); verify dimensions are 1200×630 and the file is under 100 KB

## 4. Verification

- [x] 4.1 Run Lighthouse (mobile) on the local site; verify Performance, Accessibility, Best Practices and SEO are all at least 95
- [x] 4.2 Verify the first load makes only same-origin requests, transfers under 100 KB with an empty cache, and works with JavaScript disabled
- [x] 4.3 Review published files and copy for brand-asset compliance; verify `grep -ri "anthropic\|claude" public/` returns nothing and no font other than Source Serif 4 is bundled
- [ ] 4.4 Commit locally; after the owner pushes, verify live `curl -I https://mishrabhinav.com/fonts/` font URL returns 200 with `content-type: font/woff2` and the long-lived `cache-control`, and the live page renders the serif

## Workflow follow-up

- Archive the change after the live site is verified.
