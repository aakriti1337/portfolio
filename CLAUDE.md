# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static single-page portfolio site for Aakriti Pandit (Computer Teacher & Fullstack Developer). No build system, no package manager, no JavaScript framework — plain HTML/CSS only.

- `index.html` — entire page content, structured as stacked `<section>` elements (hero, about, experience, education, skills, certifications, contact), each linked from the nav via anchor IDs.
- `style.css` — all styling, using CSS custom properties for theming.
- `profile.png` / `profile.jpeg` — hero portrait images.

## Running locally

No build step. Open `index.html` directly in a browser, or serve the directory with any static file server, e.g.:

```
python -m http.server 8000
```

There is no test suite, linter, or bundler configured.

## Architecture notes

- **Theming (light/dark) is pure CSS, no JS.** A hidden checkbox `#theme-toggle` sits as the first child of `<body>`, before `.site-wrapper`. Dark-theme variable overrides are applied via the sibling combinator `#theme-toggle:checked ~ .site-wrapper { ... }` in [style.css](style.css). All colors are driven by CSS custom properties defined on `:root` (light) and re-declared inside that selector (dark) — new colors must be added as variables in both places to remain theme-aware.
- **Mobile nav is also pure CSS**, using the same checkbox-hack pattern via `#nav-toggle` and `.nav-toggle-input:checked ~ .nav-links` (max-height transition).
- Responsive breakpoints: 992px (tablet — grids collapse to 1 column), 768px (mobile nav switches to the checkbox-driven dropdown), 480px (spacing/stacking tweaks).
- Sections follow a repeated pattern: `.section` / `.section-alt` (alternating background) > `.section-inner` (max-width wrapper) > `.section-title` with a gradient underline pseudo-element. New sections should follow this same nesting to inherit consistent spacing/typography.
