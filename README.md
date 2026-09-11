# IHAP Website

The public website for **IHAP — the Integrated Housing Application Platform**:
a 17-page static site covering the platform, its documentation, and the
commercial model behind it.

IHAP is commercial software under a low-cost licence. The site says so plainly
rather than implying openness.

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
faq.html                Licensing, cost, technical fit, risk
news.html               Releases and product updates
contact.html            Pricing, demonstrations, support, security

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

The copy describes IHAP as a pre-release product and is a first draft for
review rather than approved communications. Two things need a decision before
this is published:

- **No prices appear anywhere.** The site says the licence is low cost, scales
  with provider size rather than seats, and that a figure is given on the first
  call. Whether to publish an actual number is a commercial decision that has
  not been taken.
- **No contact details appear anywhere.** `contact.html` describes the routes
  in — sales, evaluation, support, security, accessibility — but carries a note
  where the addresses and phone numbers belong.

The deployment scenarios on `case-studies.html` are explicitly labelled as
illustrative composites, not accounts of named organisations; replace them with
real case studies as providers go live.

Commercial claims made on the site that need signing off: the annual
subscription model, statutory changes delivered under the licence, source code
review under NDA, source code escrow, non-production environments not being
separately licensed, and the 60-day evaluation.

## Copyright

© 2026 Muneris. All rights reserved. This website and its content are not
licensed for reuse.
