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
│   ├── components.css   cards, badges, tables, buttons, form
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
