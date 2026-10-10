# site-delivery Specification

## Purpose

Defines how the site is hosted and served: free static hosting with automatic deploys, HTTPS, and a single canonical hostname for mishrabhinav.com.

## Requirements

### Requirement: Deploy on push
Changes pushed to the repository's production branch SHALL be published to the live site automatically, without manual build or upload steps.

#### Scenario: Content update
- **WHEN** a commit that edits the page is pushed to the production branch
- **THEN** the live site reflects the change after the host's deploy completes

### Requirement: HTTPS only
The site SHALL be served over HTTPS on its custom domain, and plain HTTP requests SHALL be redirected to HTTPS.

#### Scenario: HTTP request
- **WHEN** a client requests `http://` for the site hostname
- **THEN** it is redirected to the `https://` equivalent

### Requirement: Canonical hostname
The site SHALL be served on one canonical hostname, `mishrabhinav.com`. Requests to `www.mishrabhinav.com` SHALL be permanently redirected (301) to the canonical hostname, preserving path and query.

#### Scenario: Request to www
- **WHEN** a client requests `https://www.mishrabhinav.com/`
- **THEN** it receives a 301 redirect to `https://mishrabhinav.com/`

#### Scenario: Request to apex
- **WHEN** a client requests `https://mishrabhinav.com/`
- **THEN** it receives the page with a 200 response and no further redirects

### Requirement: Zero-cost hosting
Hosting, TLS certificates and DNS for the site SHALL operate within free service tiers and require no recurring maintenance such as certificate renewal or server patching.

#### Scenario: Ongoing operation
- **WHEN** the site has been live for a year with no repository changes
- **THEN** it continues to be served over valid HTTPS with no owner action
