# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the site

No build step required. Open `index.html` directly in a browser, or serve it locally:

```
npx serve .
# or
python -m http.server 8080
```

## Architecture

Single-file static site — all HTML, CSS, and JavaScript live in `index.html`. No framework, no bundler, no npm.

**External dependencies (CDN only):**
- Tailwind CSS — utility classes for layout and spacing
- Google Fonts — Playfair Display (headings), Noto Sans KR (body)

**Page sections (in order):** Navbar → Hero → Intro Strip → About → Skills → Portfolio → Contact → Footer

All scroll animations, the mobile menu, and the typing effect are implemented in the inline `<script>` block at the bottom of `index.html`.

## CSS conventions

Custom styles live in the `<style>` block in `<head>`. Tailwind utilities handle layout; custom classes handle animations and non-utility patterns.

**Color palette:**
- Deep forest green: `#122a1c` (dark backgrounds, headings)
- Medium green: `#4a7c59` (accents, CTAs)
- Light sage: `#a5c4a0` (highlights on dark backgrounds)
- Cream: `#f8f5f0` (light section backgrounds)

**Key custom classes:**
- `.fade-up` / `.fade-up.visible` — scroll-triggered entrance animation via IntersectionObserver
- `.card-lift` — hover translate + shadow transition
- `.hero-fade` — staggered entrance animation on hero elements (nth-child delays)
- `.skill-tag` — pill badge for tech tags
- `.navbar-scrolled` — applied on scroll > 60px to solidify transparent navbar

## JavaScript patterns

- **Navbar**: `scroll` event toggles `.navbar-scrolled`
- **Mobile menu**: `#hamburger` toggles `.open` on `#mobile-menu`; closing also resets hamburger lines
- **Typing animation**: cycles through `phrases[]` array with typewriter effect (no library)
- **Scroll fade**: single `IntersectionObserver` watches all `.fade-up` elements; `transitionDelay` staggers by `(index % 4) * 0.08s`
