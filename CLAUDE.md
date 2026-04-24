# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A static HTML/CSS/JS website for **Kalp & Co**, a creative agency based at Vittal Mallya Rd, Bengaluru. Deployed via GitHub Pages at `kalpandco.com` (CNAME file present). No build system, no package manager, no framework — just files served as-is.

## Previewing the Site

Open any `.html` file directly in a browser, or use a local server to avoid CORS issues with assets:

```bash
python3 -m http.server 8000
# or
npx serve .
```

## Architecture

### Pages

| File | Route | Purpose |
|------|--------|---------|
| `index.html` | `/` | Home — hero, stats, vision, USP, brands, services teaser, work teaser |
| `services.html` | `/services.html` | Full services breakdown (social, digital, offline, design, photo, video, post) |
| `facility.html` | `/facility.html` | In-house studio details and location |
| `work.html` | `/work.html` | Portfolio, case studies, metrics |
| `contact.html` | `/contact.html` | Contact form and agency details |
| `kalp-co-website_1.html` | — | Draft/backup — not linked in nav |

### CSS & JS Architecture

All CSS and JS is **inline within each HTML file** — there are no external `.css` or `.js` files. When making style or script changes, edit the `<style>` block in the `<head>` and the `<script>` block at the bottom of each page individually.

### Design System (CSS Custom Properties)

Defined in `:root` on every page — keep these consistent across all files:

```css
--ink: #0e0d0b          /* near-black background */
--cream: #f5f0e8        /* off-white text */
--gold: #c9a84c         /* primary accent */
--gold-light: #e8ca7a   /* hover state for gold */
--warm-gray: #7a776f    /* secondary text */
--charcoal: #2a2720     /* card/section backgrounds */
--section-pad: 120px    /* standard vertical section padding */
```

### Typography

Three Google Fonts loaded on every page:
- **Cormorant Garamond** — headings, display text (editorial feel)
- **DM Sans** — body copy, nav, labels (light weight 300 default)
- **Bebas Neue** — large decorative numbers and background words

### Shared Patterns Repeated on Every Page

**Navigation active state** — `<body data-page="home">` matches `<li class="nav-item" data-page="home">` via JS at page bottom to add `.active` class.

**Scroll-reveal** — Add class `reveal` to any element; an `IntersectionObserver` adds `visible` when it enters the viewport (threshold 0.1). CSS handles the opacity/translateY transition.

**Custom cursor** — `#cursor` (dot) and `#cursorRing` (ring) are animated via `requestAnimationFrame`. `body { cursor: none }` is set globally.

**Nav hide-on-scroll** — JS adds `nav-hidden` (translateY(-100%)) when scrolling down past 150px, removes it on scroll up. `nav.scrolled` adds frosted-glass background after 50px.

**Responsive breakpoint** — `@media(max-width:900px)` hides `.nav-bottom`, shows hamburger + `.mobile-menu`. Grids collapse to single column.

### Assets

```
assets/
  kalp-logo-black.png          # nav and footer logo
  logos/image0.jpeg–image22.*  # client brand logos (brands grid)
  facility/                    # facility page images
  selected-work/               # work page portfolio images
```

Brand logos in the grid use `filter: grayscale(1) opacity(0.6)` by default, revealing full color on hover.
