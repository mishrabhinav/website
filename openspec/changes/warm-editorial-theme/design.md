# Design

## Context

The live site (`public/index.html`, `public/style.css`) uses a cool-grey palette and a system font stack, with a 4.2 KB first load against a 100 KB budget. The CSP is `default-src 'self'`, which already allows same-origin fonts. See proposal.md for motivation.

## Goals / Non-Goals

**Goals:**
- A warm, editorial look reminiscent of Claude/Anthropic's design language, built only from original or openly licensed assets.
- Keep zero third-party requests, no JavaScript, AA contrast and the 100 KB budget.

**Non-Goals:**
- Reproducing Anthropic's proprietary typefaces, logos, illustrations or exact brand colors, or implying affiliation.
- New content, sections or interactions.

## Decisions

**Typeface: Source Serif 4 (variable, SIL OFL 1.1) for display, system sans for body.** Anthropic's typefaces are commercial and unavailable for reuse, so a close-in-spirit open serif is used for the name, tagline and `h2`s. Self-hosting the latin-subset variable woff2 (about 50 KB) from the `@fontsource-variable/source-serif-4` package keeps requests same-origin and honors the CSP. Alternatives: Newsreader (similar, 58 KB), Lora (smaller at 38 KB but more calligraphic, less editorial); Google Fonts CDN (third-party request, rejected by the spec). Body stays on the system sans stack to save about 48 KB over bundling Inter and to avoid a second font to load.

**Font loading.** One `@font-face` with `font-display: swap`, `unicode-range` limited to latin, and a `<link rel="preload" as="font" type="font/woff2" crossorigin>` for the file. A metric-adjusted fallback (`Georgia`/`Times New Roman` stack) limits layout shift. `public/_headers` gets `Cache-Control: public, max-age=31536000, immutable` for `/fonts/*`; the font filename carries the version.

**Palette (CSS custom properties, same light/dark structure as today).**

| Token | Light | Dark |
|---|---|---|
| `--bg` | warm off-white, about `#faf9f5` | warm charcoal, about `#1f1e1d` |
| `--fg` | warm near-black, about `#1f1e1d` | warm off-white, about `#f0eee6` |
| `--muted` | warm grey, about `#5e5d59` | about `#b0aea5` |
| `--accent` | deep clay, about `#b0462a` | lighter clay, about `#e08a6d` |
| `--border` | about `#e8e6dc` | about `#3a3936` |

Exact values are tuned during implementation so every accent text pair is at least 4.5:1. A brighter clay (about `#d97757`) may be used only for non-text decoration such as underlines and focus rings, never for body-size text on the light background (it fails AA there).

**Layout refinements.** A larger serif `h1` with tight tracking, a serif tagline in the muted color, a narrower reading measure for the about text, small-caps style section label retained, link pills get a clay border on hover and the existing 3px `:focus-visible` ring in the clay accent.

**Assets and attribution.** Regenerate `og.png` (headless Chrome screenshot of a small HTML card using the new fonts and palette, kept out of the repo as before) and recolor `favicon.svg`. Ship `public/fonts/OFL.txt` beside the font and credit it in the README. No Anthropic marks are used.

## Risks / Trade-offs

- [Look-alike drifts into impersonation or implied affiliation] → New spec requirement forbids brand assets and affiliation claims; palette and typeface are original or OFL.
- [Font adds weight and a render-blocking-ish request] → Latin subset, preload, `font-display: swap`; first load stays near 60 KB, verified against the 100 KB budget and Lighthouse ≥ 95.
- [Clay accent fails contrast on the warm background] → Use a deeper clay for text and verify ratios in both themes; keep the bright clay for decoration only.
- [Cached font filename never changes] → Version in the filename if the font is ever updated.

## Migration Plan

1. Implement and verify locally (Lighthouse, contrast, 320/768/1440 widths, JS disabled).
2. Commit; the owner pushes to `main` and the Worker deploys automatically.
3. Verify live `curl -I` for the font (200, `cache-control`, `content-type: font/woff2`) and re-check link previews.
4. Rollback: `git revert` the commit and push, or roll back in the Worker's Deployments tab.
