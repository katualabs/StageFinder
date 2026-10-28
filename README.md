# StageFinder Nairobi

StageFinder Nairobi is a static website that helps newcomers to Nairobi find
matatu stages, routes and fares in the Central Business District (CBD).

It is built with **HTML and CSS only**: no JavaScript, no frameworks, no build
tools and no CSS preprocessors. All interactivity (mobile menu, FAQ, stage
highlighting) and all animation are done in pure HTML and CSS.

> **Fares are estimates.** Route, stage and fare information on this site is
> placeholder data that is still being verified in the field. Always confirm
> the fare with the conductor before you board.

## Pages

| Page | File | Purpose |
| --- | --- | --- |
| Home | `index.html` | "Where are you going?" hero, the five main directions out of town and a "New to matatus?" call-out |
| Routes | `routes.html` | One section per direction with a table of route numbers, destinations, CBD stages and off-peak / peak fares |
| Stages | `stages.html` | One card per CBD stage with its street location, landmarks and the routes it serves |
| Commuter Guide | `guide.html` | How matatus work, paying the conductor, peak hours, safety, etiquette and an FAQ |
| About | `about.html` | Purpose of the site, how the data was collected, last-updated date and the fare disclaimer |
| Contact | `contact.html` | Accessible feedback form (layout only, no submission handling) |

## Project structure

```
.
├── index.html
├── routes.html
├── stages.html
├── guide.html
├── about.html
├── contact.html
├── css/
│   ├── base.css         reset, custom properties, typography
│   ├── layout.css       header, nav, grid, footer
│   ├── components.css   cards, badges, tables, buttons, form, print styles
│   └── animations.css   all @keyframes and motion rules
├── images/              placeholders and SVG illustrations
└── README.md
```

## Running locally

No installation or build step is needed.

1. Clone or download this repository.
2. Open `index.html` in any modern web browser.

Optionally, serve the folder with any static file server so that links behave
exactly as they would online, for example:

```
python -m http.server 8000
```

then visit <http://localhost:8000>.

## Project rules

- HTML and CSS only. No `<script>` tags, inline event handlers or JS libraries.
- System font stack, no external font downloads.
- Mobile-first, accessible (WCAG AA contrast, keyboard navigable) and every
  page under 500 KB.
- All motion is disabled for users who prefer reduced motion.

## Data status

All stage locations, route-to-stage mappings and fares are **placeholders
awaiting field verification**. Each one is marked with an `<!-- VERIFY -->`
comment in the HTML so it can be found and checked. The "fares are estimates"
disclaimer is shown on `routes.html` and `about.html`.

## Testing

Checks carried out in the quality pass (28 October 2026):

### Validity

| Check | Tool | Result |
| --- | --- | --- |
| HTML, all six pages | W3C Nu HTML Checker | 0 errors. Info notes only: `role="list"` is kept on purpose because Safari/VoiceOver drops list semantics when `list-style: none` is applied |
| `css/base.css` | W3C CSS Validator (CSS3 + SVG) | 0 errors |
| `css/layout.css` | W3C CSS Validator | 0 errors |
| `css/components.css` | W3C CSS Validator | 0 errors |
| `css/animations.css` | W3C CSS Validator | 3 errors, all for `animation-timeline` / `animation-range` (scroll-driven animations). These are valid properties from the CSS Scroll-driven Animations specification that the validator does not support yet. They sit inside `@supports (animation-timeline: view())`, so browsers without support ignore them and show all content |

### Accessibility

- **Contrast:** every text/background pair was calculated with the WCAG
  formula. All pass 4.5:1; the lowest are white on the green stage sign
  (4.83:1) and ink on the route orange (4.66:1). Brand orange (`#E4572E`) is
  never used for text on light backgrounds; the darker `#B83A15` (5.09:1 on
  the page background) is used instead.
- **Peak fares** always carry the word "Peak" or "Off-peak", never colour alone.
- **Alt text:** every `<img>` has descriptive alt text; decorative inline SVGs
  use `aria-hidden="true"`.
- **Headings:** one `<h1>` per page and no skipped heading levels.
- **Landmarks:** `header`, `nav` (labelled Main / Footer / page navigation),
  `main` and `footer` on every page, plus a working "Skip to content" link.
- **Keyboard:** tab order follows the source order (no positive `tabindex`).
  The mobile menu checkbox, ticker pause toggle, FAQ summaries, form controls
  and all links are reachable and show a visible `:focus-visible` outline
  (yellow on dark surfaces, ink on light ones). Direction cards show a focus
  ring around the whole card.
- **Forms:** every control has a `<label>`; the topic radios use
  `<fieldset>`/`<legend>`; hints and error messages are linked with
  `aria-describedby`; the phone field uses `type="tel"` with the pattern
  `0[17][0-9]{2} ?[0-9]{3} ?[0-9]{3}` (e.g. 0712 345 678).
- **Tap targets:** links, buttons, chips and form choices are at least
  44 x 44 px.
- **Motion:** with `prefers-reduced-motion: reduce` all animations and
  transitions are switched off, the matatu is shown parked and the ticker
  becomes a static row that can be scrolled sideways. The moving ticker also
  has its own pause button.

### Responsive layout and print

- Every page was rendered at **320, 375, 768, 1024 and 1440 px** wide and
  measured for horizontal overflow: none at any width. Route tables fit a
  320 px screen without a horizontal scrollbar, so their sticky headers work.
- Grids are 1 column on phones, 2 columns from 40em and 3 columns from 64em.
- **Print:** `routes.html` prints as a one-page, two-column route sheet on both
  A4 and US Letter (checked by printing to PDF in Chrome).

### Other checks

- No `<script>` elements or inline event handlers on any page.
- Page weight (HTML + all CSS + images used) is between 64 KB and 77 KB per
  page, well under the 500 KB limit.
- Tested in Google Chrome (desktop) and headless Chrome at the widths above.
  Scroll-driven reveals are a progressive enhancement: in browsers without
  support (for example older Firefox), content is fully visible.
