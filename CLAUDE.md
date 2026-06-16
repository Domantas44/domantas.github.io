# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-file static marketing website for **Domantas Media**, an AI video production service. The entire site lives in `index.html` — there is no build system, no package manager, and no frameworks.

Custom domain: `domantasmedia.lt` (configured via `CNAME`)
Hosted on: GitHub Pages

## Running Locally

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

No build step. Changes to `index.html` are immediately visible on reload.

## Architecture

All CSS, JavaScript, and HTML are embedded in `index.html` (~1,800 lines). Structure:

1. `<head>` — CSS variables, all styles, Google Fonts (Space Grotesk, Inter)
2. `<body>` — Sections: `#hero`, `#services`, `#portfolio`, `#photos`, `#process`, `#free-sample`, `#pricing`, `#contact`, footer
3. `<script>` at bottom — all interactivity

## Bilingual System (EN/LT)

Translations use HTML data attributes on every text element:

```html
<span data-en="English text" data-lt="Lietuviškas tekstas">English text</span>
```

The JS `setLanguage(lang)` function swaps `textContent` from the appropriate attribute and toggles `.active` on the language buttons. When editing copy, always update **both** `data-en` and `data-lt` attributes.

## Key JavaScript Features

- **Language switching**: `setLanguage('en'|'lt')` — persists to `localStorage`
- **3D card tilt**: `mousemove` on `.glass-card` updates CSS `--rotateX/Y` vars
- **Magnetic buttons**: Pointer events shift `.magnetic-btn` toward cursor within 100px radius
- **Stat counters**: `IntersectionObserver` triggers animated number counts on scroll
- **Cursor glow**: `mousemove` on `body` updates `--cursor-x/Y` CSS vars used in a `::before` radial gradient

## External Services

- **Formspree** (`https://formspree.io/f/...`) — contact form POST target; no backend needed
- **WhatsApp** — floating button links to `https://wa.me/...`
- **Google Fonts** — loaded via `<link>` in `<head>`; no local font files

## Static Assets

- `video1.mp4` – `video4.mp4`: Portfolio showcase videos (referenced in `#portfolio` section)
- `before.png`, `after.png`: AI photo comparison images (referenced in `#photos` section)
