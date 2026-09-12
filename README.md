# GovHelm Housing Website

The public website for **GovHelm Housing**, the housing management platform from Muneris:
a 17-page static site covering the platform, its documentation, and the
commercial model behind it.

GovHelm Housing is commercial software under a low-cost licence. The site says
so plainly rather than implying openness.

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
api.html                REST API reference
deployment.html         Topologies, sizing, operations
comparison.html         How GovHelm Housing compares, with maturity markers
case-studies.html       Illustrative deployment scenarios
faq.html                Licensing, cost, technical fit, risk
news.html               Releases and product updates
contact.html            Pricing, demonstrations, support, security

assets/css/site.css     The whole stylesheet, sectioned and commented
assets/js/site.js       Theme toggle, nav dropdowns, mobile menu
assets/img/favicon.svg  Site icon
```

## Brand

Applied from **GovHelm Housing sub-brand pack v1.0**. GovHelm Housing is an
*edition* of GovHelm, not a separate identity: it uses the GovHelm mark, wordmark
and typefaces, and owns only the `Housing` descriptor, Community Green as an
accent, and the product icon.

### Rules the pack states, and this site obeys

- **The lockup is artwork, never live text.** `assets/brand/lockup-horizontal.svg`
  on light, `lockup-horizontal-reversed.svg` on dark — the full-colour artwork must
  never go on a dark surface. Both are in the markup and CSS swaps them by theme.
  The link's accessible name comes from a visually hidden span, so it survives
  either state.
- **Community Green `#3FA46A` never carries text on a light surface** — it is
  2.83:1 and fails AA. Text green is always `#2E7D52` (`--brand`); the accent is
  confined to fills and marks (`--brand-fill`).
- **Minimum lockup width is 150px.** The header renders it at 187px, dropping to
  155px under 560px wide — never below the minimum.
- **Blue and green do different jobs.** Helm Blue `#2457D6` marks platform-level
  affordances (focus rings); Community Green marks housing-domain state. No
  element uses both for the same job.
- **Only the loaded weights are used.** Familjen Grotesk 500/600/700 for display,
  Archivo 400/500 for body, IBM Plex Mono 400/500 for data. `--w-bold`,
  `--w-semi` and `--w-med` exist so no rule can ask for a weight that would be
  synthesised.

### Colour tokens

The ten brand tokens are declared verbatim as `--gh-*` at the top of
`site.css` and mapped onto the site's roles. A handful of neutral steps are
derived where a UI needs more than ten values; each is commented as derived.
**The edition palette has no amber**, so the caution treatment uses Deep Teal
rather than an invented colour — worth a decision if you want a true warning hue.

### Typography is self-hosted

The pack's `fonts.css` points at Google Fonts. This site instead serves the
woff2 files from `assets/fonts/` (Latin and Latin Extended, 14 files, ~288 KB),
so no visitor request leaves the site to fetch a typeface — which also avoids the
third-party-transfer question a public sector buyer will ask. All three faces are
SIL OFL; `assets/fonts/OFL.txt` carries the licence.

Because font fetches are CORS-scoped, **the fonts do not load from `file://`** —
opening `index.html` directly falls back to Arial. Serve the folder over HTTP
(`python3 -m http.server`) to see it as deployed.

### Still placeholders

`govhelmctl`, `GOVHELM_ENV`, `X-GovHelm-*`, `registry.govhelm.dev`,
`charts.govhelm.dev` and the `govhelm-*` container names were invented before the
brand pack arrived. They need confirming against what you actually register.

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

## Maturity markers

Capability claims are marked with one of three words, used precisely and
defined on `comparison.html`:

- **Deployed** — running in a live service, handling real cases.
- **Built** — code complete and in a released version you can run today.
- **Designed** — specified and scheduled, not yet written.

GovHelm Housing currently has **no Deployed capabilities**: it is pre-release, running in
pilot and evaluation environments only. `comparison.html` says so prominently
and `modules.html` marks each module. Keep these in step — a capability that
moves from Designed to Built must be changed in both places, and the roadmap
must agree.

## Content status

The copy describes GovHelm Housing as a pre-release product and is a first draft for
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

`comparison.html` compares GovHelm Housing against four **archetypes** of housing system,
not four named vendors. No competitive analysis was supplied when the page was
written, and a supplier publishing invented capability claims about named
competitors is both unreliable and legally exposed. If you want named columns,
supply the verified analysis and the archetype columns can be replaced with
it — the page structure takes named vendors without change.

## Copyright

© 2026 Muneris. GovHelm and GovHelm Housing are trademarks of Muneris.
This website and its content are not licensed for reuse.
