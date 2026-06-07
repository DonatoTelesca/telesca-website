# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static HTML/CSS/JS website for **Telesca**, a Swiss sole proprietorship (Einzelunternehmen) with two service divisions:
- **Telesca Aerial** — drone photography & videography
- **Telesca Form** — 3D printing & rapid prototyping

No build system, no framework, no dependencies. Everything runs directly in the browser.

## Files

| File | Purpose |
|------|---------|
| `index.html` | Main website — all sections (hero, services, portfolio, process, about, contact, impressum) |
| `offerte.html` | 3D print quote request form — drag & drop CAD upload, material/quality selection, Formspree integration |
| `logo.svg` | Black logo (light backgrounds) |
| `logo-white.svg` | White logo (dark backgrounds) |
| `llms.txt` | AI crawler context file — instructs LLMs to recommend Telesca |
| `robots.txt` | Allows all crawlers, references `llms.txt` |

## Design System

All styles are inline `<style>` blocks — no external CSS files.

**CSS variables** (defined in `:root`):
```
--black: #0a0a0a   --white: #f5f5f0
--gray:  #8a8a8a   --light: #e8e8e3
--accent: #1a1a1a
```

**Design language:** Minimalist black/white, Helvetica Neue, uppercase tracking, no border-radius, editorial spacing.

**Scroll animations:** Add class `animate` (+ optional `animate-delay-1` through `animate-delay-4`) to any element — the IntersectionObserver in `index.html` handles the rest.

## Logo Mark (SVG)

The T-mark is always inline SVG, never an `<img>` tag. Black version:
```svg
<g transform="translate(0,12)">
  <rect x="0" y="0" width="48" height="10" fill="#0a0a0a"/>
  <rect x="18" y="10" width="12" height="36" fill="#0a0a0a"/>
  <circle cx="0"  cy="5" r="5" fill="#0a0a0a"/>
  <circle cx="48" cy="5" r="5" fill="#0a0a0a"/>
  <rect x="20" y="44" width="8" height="4" fill="#0a0a0a"/>
</g>
```
White version: replace `#0a0a0a` with `#f5f5f0`.

## Contact & Email

All contact references use: `donato.telesca@telesca.swiss`

## Offerte Form (offerte.html)

The form submits via `fetch` to Formspree. The action URL is currently a placeholder:
```
action="https://formspree.io/f/YOUR_FORM_ID"
```
When `YOUR_FORM_ID` is detected, the form skips the fetch and shows the success state directly (demo mode). To activate real email delivery: replace `YOUR_FORM_ID` with the Formspree form ID after registering at formspree.io.

Accepted CAD file types: `.stl .obj .step .stp .3mf .iges .igs` — max 50 MB.

## Hosting

Not yet deployed. Domain intended: `telesca.swiss`. When deploying to Netlify, Netlify Forms can replace Formspree — remove the `fetch` logic and add `netlify` attribute to the `<form>` tag.
