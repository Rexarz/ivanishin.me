# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Personal portfolio site for Sergey Ivanishin (game designer & product director). The entire site lives in a single file: `index.html` — all HTML, CSS, and JavaScript are inline. There is no build step, no package manager, and no external dependencies beyond Google Fonts loaded via CDN.

To preview locally, open `index.html` directly in a browser (`open index.html` on macOS) or serve it with any static server (`python3 -m http.server`).

## Architecture

Everything is in `index.html` in this order:

1. **`<head>`** — SEO meta tags, Open Graph, Twitter Card, Schema.org JSON-LD structured data, Google Fonts `<link>`, and the full `<style>` block.
2. **`<body>`** — Markup for all sections, followed by a single `<script>` block.

### CSS design system

All colors and fonts are defined as CSS custom properties on `:root`:

- Colors: `--bg`, `--bg2`, `--panel`, `--border`, `--text`, `--muted`, `--pink`, `--cyan`, `--yellow`, `--orange`, `--green`, `--purple`
- Fonts: `--pixel` (Press Start 2P), `--jp` (Noto Sans JP), `--mono` (Share Tech Mono)

Body-level pseudo-elements (`body::before`, `body::after`) create the CRT vignette and scanline overlay effects — they sit at `z-index: 9997/9998` and are `pointer-events: none`.

### Page sections

| Section | ID | CSS class pattern |
|---|---|---|
| Hero | `#home` | `.hero`, `.hero-*` |
| About / Character Profile | `#about` | `.about-*`, `.char-*` |
| Experience / Stage Select | `#exp` | `.exp-grid`, `.exp-card` |
| Skills & Tools | `#tools` | `.tools-table`, `.tool-row` |
| Contact | `#contact` | `.contact-*` |

### JavaScript (inline `<script>`)

Three self-contained behaviours, no libraries:

1. **Custom cursor** — tracks `mousemove`, toggles `.active` on hover over `a`/`button`.
2. **Kanji wall** — fills `#kanjiWall` with 300 random chars from a fixed Japanese string on load.
3. **Scroll animations** — `IntersectionObserver` adds `.visible` to `.reveal` elements; a second observer animates `.cstat-fill[data-w]` bar widths when `.char-card` enters the viewport.

### Responsive breakpoint

A single `@media (max-width: 768px)` rule handles mobile: hides `nav`, switches grids to single column, hides cursor, and resets `body { cursor: auto }`.
