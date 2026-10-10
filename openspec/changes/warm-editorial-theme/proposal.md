# Proposal

## Why

The site works but looks generic (cool grey, system font only). The owner wants a warmer, editorial look in the spirit of Claude/Anthropic's design language: warm neutrals, a serif display face and a restrained clay accent. Anthropic's own typefaces are proprietary commercial fonts and its logos and marks are trademarks, so the goal is a similar feel built from openly licensed parts, not a copy.

## What Changes

- Replace the cool-grey palette with a warm paper-like light theme and a warm charcoal dark theme, plus a muted terracotta/clay accent. Accent text colors are chosen to keep WCAG AA contrast.
- Use a self-hosted, openly licensed serif (Source Serif 4, SIL OFL 1.1) for the name, tagline and section headings; keep a system sans-serif stack for body and links.
- Refine layout: larger editorial hero, calmer spacing, softer link "pills" with a clay hover/focus treatment.
- **MODIFIED** the self-contained/lightweight requirement: the "system font stack only" rule becomes "same-origin fonts only", keeping the no third-party requests rule and the 100 KB first-load budget.
- Add a requirement that the page does not use Anthropic or Claude logos, marks, proprietary fonts or wording that implies affiliation.
- Regenerate `og.png` and `favicon.svg` in the new palette, and include the license text for the bundled font.
- Out of scope: new sections, JavaScript, animation, analytics, and any change to content or hosting.

## Capabilities

### New Capabilities

None.

### Modified Capabilities
- `landing-page`: "Lightweight and self-contained" is modified to allow same-origin self-hosted web fonts; new requirements added for the warm editorial visual style and for no use of third-party brand assets.

## Impact

- Files: `public/style.css`, `public/index.html` (font preload only), `public/favicon.svg`, `public/og.png`, new `public/fonts/` (woff2 plus OFL license file), `README.md` (font credits).
- `public/_headers`: existing CSP (`default-src 'self'`) already permits same-origin fonts; add long-lived caching for `/fonts/*`.
- First-load size rises by roughly 50 KB (one variable font subset), still under the 100 KB budget.
- No hosting, DNS or deployment changes.
