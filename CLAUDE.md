# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static single-page website for **M Essack & Associates**, a law firm in Westville, Durban, South Africa. Hosted on GitHub Pages at `messacklaw.co.za`.

## Architecture

- **Plain HTML/CSS/JS** — no build tools, no static site generator, no npm
- **Tailwind CSS via CDN** with custom config (primary: `#d4af35`, dark theme default)
- **Google Fonts** (Inter) and **Material Symbols** for icons
- **Formspree** for contact form submissions
- Sample UI reference in `Sample UI/` (code.html + screen.png)
- Design document in `DESIGN.md`

## Key Files

- `index.html` — the entire website (single page with anchor sections)
- `assets/images/` — self-hosted images (logo, hero, about, map)
- `CNAME` — custom domain config for GitHub Pages
- `robots.txt`, `sitemap.xml` — SEO files
- `404.html` — custom error page

## Brand

- **Primary color**: `#d4af35` (gold)
- **Dark background**: `#201d12`
- **Light background**: `#f8f7f6`
- **Font**: Inter (300–900 weights)
- **Tone**: Professional, bold, uppercase tracking throughout
- Dark mode is the default (`class="dark"` on html element)

## Deployment

GitHub Pages serves from `main` branch. HTTPS enforced via Let's Encrypt. Custom domain: `messacklaw.co.za`.
