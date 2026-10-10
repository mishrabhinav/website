# Spec Delta

## MODIFIED Requirements

### Requirement: Lightweight and self-contained
The page SHALL load without third-party requests (fonts, scripts, analytics or trackers). Any web fonts SHALL be self-hosted on the site's own origin and openly licensed, and body text SHALL fall back to a system font stack. Total transfer size of the first load SHALL be under 100 KB.

#### Scenario: First page load
- **WHEN** the page is loaded with an empty cache
- **THEN** every request goes to the site's own origin and total transferred bytes are under 100 KB

#### Scenario: Font fails to load
- **WHEN** the self-hosted web font cannot be fetched
- **THEN** the page remains fully readable using a fallback font with no layout breakage

## ADDED Requirements

### Requirement: Warm editorial visual style
The page SHALL use a warm neutral palette with a single muted clay accent, a serif typeface for the name, tagline and section headings, and a sans-serif typeface for body text and links. The style SHALL be applied in both the light and dark themes.

#### Scenario: Light theme styling
- **WHEN** the page is viewed with a light color scheme preference
- **THEN** it shows a warm off-white background, dark warm text and a clay accent, with the name and headings in a serif face

#### Scenario: Dark theme styling
- **WHEN** the page is viewed with a dark color scheme preference
- **THEN** it shows a warm charcoal background, light warm text and a lighter clay accent, with the same typefaces

#### Scenario: Accent contrast
- **WHEN** accent-colored text is rendered in either theme
- **THEN** it meets WCAG AA contrast against its background

### Requirement: No third-party brand assets
The page SHALL NOT include Anthropic or Claude logos, marks or proprietary fonts, and SHALL NOT state or imply any affiliation with or endorsement by Anthropic. All bundled fonts SHALL ship with their license text.

#### Scenario: Asset review
- **WHEN** the published files are inspected
- **THEN** no Anthropic or Claude logo, mark or proprietary typeface file is present, and each bundled font has its license file alongside it

#### Scenario: Copy review
- **WHEN** the page text and metadata are read
- **THEN** nothing claims or suggests affiliation with Anthropic
