# IHAP Website

The public website for **IHAP — the open source Integrated Housing Application
Platform**: a 20-page static site covering the platform, its documentation, and
the project behind it.

No build step, no dependencies, no framework. Every page is plain HTML served
as-is, sharing one stylesheet and one small progressive-enhancement script.

## Running it

Open `index.html` in a browser, or serve the directory over HTTP:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000
```

Any static host will serve it unchanged, including GitHub Pages (set the source
to this branch and the root directory).

## Layout

```
index.html              Home
about.html              About the project
features.html           What the platform does
modules.html            The twelve modules
architecture.html       Layers, data model, technology choices
integrations.html       APIs, events, batch, migration
security.html           Controls, UK GDPR, threat model
accessibility.html      WCAG 2.2 AA commitment and testing
roadmap.html            Release plan and versioning policy
docs.html               Documentation index
getting-started.html    Ten-minute local quick start
api.html                REST API reference
deployment.html         Topologies, sizing, operations
case-studies.html       Illustrative deployment scenarios
community.html          Where development happens
contributing.html       How to contribute
governance.html         Roles, decisions, commitments
faq.html                Frequently asked questions
news.html               Releases and project updates
contact.html            How to reach the project

assets/css/site.css     The whole stylesheet, sectioned and commented
assets/js/site.js       Theme toggle, nav dropdowns, mobile menu
assets/img/favicon.svg  Site icon
```

## Editing

- **Content** lives directly in each `.html` file.
- **Design tokens** — colours, spacing, radii, type — are CSS custom properties
  at the top of `assets/css/site.css`. Change them there rather than in
  individual rules; light and dark values are defined in three matching blocks
  (`:root`, the `prefers-color-scheme: dark` block, and `[data-theme="dark"]`).
- **Navigation** is duplicated in the header, the mobile menu and the footer of
  every page. Adding or renaming a page means updating all three in each file.

## Things worth preserving

The site was built to the standard it describes, so a few properties are worth
keeping intact when editing:

- **Accessibility.** All text meets WCAG 2.2 AA contrast in both themes; every
  link and button has an accessible name; the first tab stop is a skip link;
  the nav dropdowns are click-operated with `aria-expanded` and Escape support.
- **Works without JavaScript.** The script only adds the theme toggle and the
  menu behaviour. Every link is present in the markup regardless.
- **No horizontal scroll** at 390px; tables and diagrams scroll inside their own
  containers rather than stretching the page.
- **Theme-aware.** Pages follow the operating system theme by default and
  remember an explicit choice in `localStorage`.

## Content status

The copy describes IHAP as a pre-release platform and is a first draft for
review rather than approved communications. The deployment scenarios on
`case-studies.html` are explicitly labelled as illustrative composites, not
accounts of named organisations; replace them with real case studies as
providers go live.

## Licence

Licensed under the [Apache License, Version 2.0](LICENSE).
