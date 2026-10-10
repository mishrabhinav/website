# landing-page Specification

## Purpose

Defines the content, appearance and quality bar of the single-page personal site at mishrabhinav.com, so visitors quickly learn who the owner is and where to reach them.

## Requirements

### Requirement: Single page with essential sections
The site SHALL consist of one page containing a hero (name and one-line positioning), a short about blurb of at most three sentences, and a links area. It SHALL NOT present resume content such as an experience timeline, skills inventory or CV download.

#### Scenario: Visitor opens the site
- **WHEN** a visitor loads the root URL
- **THEN** they see the owner's name, a one-line positioning statement, an about blurb and the links area on a single page

#### Scenario: No resume content
- **WHEN** the page content is reviewed
- **THEN** it contains no work-history list, skills list or CV download link

### Requirement: Outbound contact links
The links area SHALL provide links to the owner's LinkedIn profile, GitHub profile and an email address. External profile links SHALL open the correct destination and the email link SHALL use a `mailto:` address.

#### Scenario: Visitor follows a profile link
- **WHEN** a visitor activates the LinkedIn or GitHub link
- **THEN** the browser navigates to the corresponding profile

#### Scenario: Visitor emails the owner
- **WHEN** a visitor activates the email link
- **THEN** their mail client opens with the owner's address pre-filled

### Requirement: Light and dark appearance
The site SHALL follow the visitor's operating-system color scheme preference, rendering a light theme or a dark theme accordingly, with sufficient text contrast in both.

#### Scenario: Dark mode preference
- **WHEN** the visitor's system prefers a dark color scheme
- **THEN** the page renders with a dark background and light text

#### Scenario: Light mode preference
- **WHEN** the visitor's system prefers a light or unspecified color scheme
- **THEN** the page renders with a light background and dark text

### Requirement: Responsive layout
The page SHALL be readable and usable from 320px to wide desktop viewports without horizontal scrolling.

#### Scenario: Small phone viewport
- **WHEN** the page is viewed at a 320px-wide viewport
- **THEN** all content is visible without horizontal scrolling and links remain tappable

### Requirement: Accessibility baseline
The page SHALL use semantic HTML landmarks, a single top-level heading, a document language, visible keyboard focus on interactive elements, and WCAG AA text contrast. It SHALL be fully usable without JavaScript.

#### Scenario: Keyboard navigation
- **WHEN** a visitor tabs through the page
- **THEN** each link receives a visible focus indicator in a logical order

#### Scenario: JavaScript disabled
- **WHEN** the page is loaded with JavaScript disabled
- **THEN** all content and links work normally

### Requirement: Lightweight and self-contained
The page SHALL load without third-party requests (fonts, scripts, analytics or trackers). Any web fonts SHALL be self-hosted on the site's own origin and openly licensed, and body text SHALL fall back to a system font stack. Total transfer size of the first load SHALL be under 100 KB.

#### Scenario: First page load
- **WHEN** the page is loaded with an empty cache
- **THEN** every request goes to the site's own origin and total transferred bytes are under 100 KB

#### Scenario: Font fails to load
- **WHEN** the self-hosted web font cannot be fetched
- **THEN** the page remains fully readable using a fallback font with no layout breakage

### Requirement: Link previews and metadata
The page SHALL provide a title, meta description, favicon and Open Graph/Twitter card metadata so shared links render a meaningful preview.

#### Scenario: Link shared in a chat or social app
- **WHEN** the site URL is pasted into an app that fetches link previews
- **THEN** the preview shows the site title, description and preview image

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
