---
date: 2026-03-16
project: "M Essack & Associates Website"
status: draft
---

# Design: M Essack & Associates Website

## Problem Statement

M Essack & Associates is a law firm based in Westville, Durban, South Africa offering property law, rental law, estates & wills, family law, and civil litigation services. The firm currently lacks a professional web presence to attract and convert potential clients searching online for legal services in the Durban area.

Over 70% of South African web traffic is mobile, and local search ("property lawyer Westville", "divorce attorney Durban") is the primary discovery channel for small law firms. Without a website, the firm relies entirely on word-of-mouth and direct WhatsApp referrals, missing a large segment of potential clients.

The goal is a professional, fast-loading static website that establishes credibility, clearly communicates practice areas, and converts visitors into enquiries via WhatsApp and a contact form.

## Solution Overview

A single-page static website faithfully reproducing the approved sample UI design — dark theme with gold (#d4af35) accents, Inter typeface, and a bold, modern legal aesthetic. The site will be hosted on GitHub Pages with the custom domain `messacklaw.co.za`.

The site is intentionally minimal in scope: one page with anchor-linked sections (Hero, About, Services, Contact, Footer), WhatsApp as the primary CTA, and a contact form powered by Formspree for email-based enquiries. No CMS, no blog, no multi-page navigation — just a fast, professional landing page that converts.

This approach prioritizes speed to launch, low maintenance burden, and zero hosting cost.

## Target Users

- **Primary**: Individuals in the Durban/Westville area searching for legal services (property transfers, divorce, wills, evictions, debt recovery). Non-technical, often searching on mobile via Google.
- **Secondary**: Business clients needing contract dispute resolution, property agreements, or civil litigation. More likely to use the contact form than WhatsApp.
- **Scale**: Low traffic — expected hundreds of visits per month. Well within GitHub Pages' 100 GB/month bandwidth limit.

## Key Design Decisions

### Plain HTML/CSS/JS — No Build Tools
The site will be a single `index.html` file with Tailwind CSS via CDN, matching the sample UI approach. No static site generator (Jekyll, Hugo), no bundler, no npm dependencies. For a single-page site that changes infrequently, build tools add complexity with no benefit. Anyone can edit the HTML directly.

### Formspree for Contact Form
GitHub Pages cannot process form submissions server-side. Formspree provides a free tier (50 submissions/month) that sends form data directly to the firm's email. No backend, no API keys in client code — just a form `action` URL. Alternatives considered: Netlify Forms (requires Netlify hosting), mailto links (poor UX, no tracking), Google Forms embed (breaks design consistency).

### Self-Hosted Images
The sample UI references external `lh3.googleusercontent.com` URLs which are unreliable for production. All images will be stored in the repository under an `assets/images/` directory. This ensures availability and keeps the site fully self-contained. Placeholder images will be used until the firm provides real photography.

### Tailwind CSS via CDN
The sample UI already uses the Tailwind CDN with a custom config. This will be retained for simplicity. The trade-off is a ~300KB CDN dependency on page load, but Tailwind's CDN is fast and cached globally. For a site this size, a custom CSS build would be premature optimization.

### Dark Mode Default
The sample UI uses `class="dark"` on the HTML element, making dark mode the default presentation. This matches the firm's brand aesthetic (dark backgrounds, gold accents). Light mode styles exist in the Tailwind classes but are secondary. No theme toggle will be implemented — the site is dark-first by design.

## Architecture

### System Overview
```
┌─────────────────────────────────────┐
│         GitHub Repository           │
│                                     │
│  index.html    (single page)        │
│  assets/                            │
│    images/     (logo, hero, about)  │
│    favicon.ico                      │
│  CNAME         (messacklaw.co.za)   │
│  404.html      (custom error page)  │
│  robots.txt                         │
│  sitemap.xml                        │
│                                     │
│  GitHub Pages deploys from main     │
└──────────────┬──────────────────────┘
               │
               ▼
┌──────────────────────────────────────┐
│  GitHub Pages CDN                    │
│  messacklaw.co.za (HTTPS via LE)     │
└──────────────┬───────────────────────┘
               │
               ▼
┌──────────────────────────────────────┐
│  External Services                   │
│                                      │
│  Tailwind CDN  — styling             │
│  Google Fonts  — Inter typeface      │
│  Material Symbols — icons            │
│  Formspree     — contact form        │
│  WhatsApp API  — wa.me deep links    │
│  Google Maps   — embedded map        │
└──────────────────────────────────────┘
```

### Page Structure
```
Header (sticky nav)
  ├── Logo + firm name
  ├── Nav links: Home | About | Services | Contact
  └── WhatsApp CTA button

Hero Section
  ├── Background image with gradient overlay
  ├── Tagline: "Justice with Integrity"
  ├── Subtitle
  └── CTAs: WhatsApp Us | Our Practice Areas

About Section
  ├── Firm photo
  ├── Description quote
  └── Contact link

Services Section (3x2 grid)
  ├── Property Law
  ├── Rental Law
  ├── Estates & Wills
  ├── Family Law
  ├── Civil Litigation
  └── WhatsApp CTA card

Contact Section
  ├── Office address, phone, email
  ├── Contact form (Name, Email, Phone, Message)
  ├── WhatsApp CTA
  └── Google Maps embed

Footer
  ├── Logo + firm name
  ├── Nav links
  ├── WhatsApp icon link
  └── Copyright + legal links
```

### Data Model
Not applicable — no database, no user data stored. Formspree handles form submissions externally.

### API Surface
Not applicable — static site. The only external API interaction is the Formspree form POST endpoint.

### Security Model
- **HTTPS**: Enforced via GitHub Pages + Let's Encrypt (automatic with custom domain).
- **Form submissions**: Handled by Formspree (no credentials stored in repository). Formspree provides spam filtering (reCAPTCHA/honeypot).
- **No user authentication**: Public informational site, no login.
- **No cookies/tracking**: Unless the firm explicitly requests analytics (out of scope for MVP).

## Technology Stack

| Component | Choice | Rationale |
|-----------|--------|-----------|
| Markup | HTML5 | Single-page, no templating needed |
| Styling | Tailwind CSS (CDN) | Matches sample UI, rapid development, no build step |
| Icons | Material Symbols (Google) | Already used in sample UI |
| Font | Inter (Google Fonts) | Already used in sample UI |
| Contact Form | Formspree (free tier) | No backend needed, 50 submissions/month free |
| Maps | Google Maps Embed | Free, no API key required for simple embeds |
| Hosting | GitHub Pages | Free, reliable, custom domain + HTTPS |
| Domain | messacklaw.co.za | Existing custom domain |

### Libraries

| Library | Purpose |
|---------|---------|
| Tailwind CSS 3.x (CDN) | Utility-first CSS framework |
| Google Material Symbols | Icon set for service cards and contact details |
| Inter (Google Fonts) | Primary typeface |

## Capabilities (ordered by milestone)

### Milestone 1: Core Website
- **C1: Page structure and navigation**: Sticky header with logo, nav links (Home, About, Services, Contact) with smooth scroll to anchors, and WhatsApp CTA button. Mobile hamburger menu with slide-out nav for screens below `md` breakpoint.
- **C2: Hero section**: Full-viewport hero with background image, gradient overlay, tagline "Justice with Integrity", subtitle, and dual CTAs (WhatsApp, Our Practice Areas). Acceptance: visually matches sample UI on desktop and mobile.
- **C3: About section**: Two-column layout (image left, text right) with firm description, quote styling with gold left border, and contact link. Stacks vertically on mobile.
- **C4: Services grid**: 3x2 responsive grid with 5 practice area cards (Property Law, Rental Law, Estates & Wills, Family Law, Civil Litigation) and 1 WhatsApp CTA card. Each card has icon, title, and bullet list. Grid collapses to single column on mobile.
- **C5: Contact section with form**: Two-column layout — left side has contact details (address, phone, email) plus a contact form (Name, Email, Phone, Message, Submit button) integrated with Formspree; right side has embedded Google Map of office location. WhatsApp CTA below the form.
- **C6: Footer**: Firm logo, nav links, WhatsApp icon, copyright notice, Privacy Policy and Terms of Service placeholder links.

**Testable at this milestone:**
- Unit: N/A (no JS logic beyond mobile menu toggle)
- Integration: Formspree form submission delivers email to messacklaw@gmail.com. WhatsApp links open correctly on mobile and desktop.
- E2E: Full page loads under 3 seconds on 3G throttle. All nav anchor links scroll to correct sections. Mobile menu opens/closes. Form validates required fields. Site renders correctly at 320px, 768px, and 1280px widths.

### Milestone 2: Deployment & SEO
- **C7: GitHub Pages deployment**: Repository configured for GitHub Pages serving from `main` branch. CNAME file for `messacklaw.co.za`. HTTPS enforced. Custom 404 page.
- **C8: SEO fundamentals**: Meta title, description, and Open Graph tags targeting local search terms ("M Essack & Associates | Attorneys in Westville Durban | Property Law, Family Law, Civil Litigation"). `robots.txt` and `sitemap.xml` for search engine indexing. Structured data (LocalBusiness JSON-LD) for Google rich results.
- **C9: Performance and accessibility**: All images optimised (WebP format where possible, appropriate sizing). Alt text on all images. Semantic HTML landmarks. Sufficient colour contrast ratios. Lighthouse score targets: Performance > 90, Accessibility > 90, SEO > 90.
- **C10: Asset replacement**: Placeholder images replaced with real firm logo, office photos, and hero image (dependent on firm providing assets). Favicon set.

**Testable at this milestone:**
- Unit: N/A
- Integration: DNS resolves `messacklaw.co.za` to GitHub Pages. HTTPS certificate valid. Formspree still functional on production domain.
- E2E: Google Lighthouse audit passes targets. Site appears in Google Search Console. Open Graph preview renders correctly when URL shared on WhatsApp/social media. 404 page displays for invalid URLs.

## Constraints & Requirements

- **Performance**: Page must load under 3 seconds on a South African mobile connection (3G). Total page weight target: under 1.5 MB.
- **Hosting cost**: Zero — GitHub Pages free tier. Formspree free tier (50 submissions/month).
- **Browser support**: Chrome, Safari, Firefox, Samsung Internet (covers 95%+ of SA mobile browsers). No IE11 support.
- **Content**: All copy taken directly from the sample UI unless the firm provides updates.
- **Legal compliance**: Copyright year updated to 2025. Privacy Policy and Terms of Service pages are placeholder links (content to be provided by the firm).

## Risks

| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| External CDN failure (Tailwind, Google Fonts) | Site loses styling/icons | Low | Tailwind CDN is highly reliable; could self-host CSS as fallback in future |
| Formspree free tier limit exceeded (50/month) | Form submissions rejected | Low | Monitor usage; upgrade to paid tier ($10/month) if needed |
| Firm does not provide real images | Site looks unprofessional with placeholders | Medium | Use high-quality stock legal images as interim; flag to firm as blocker |
| Google Maps embed blocked or rate-limited | Map section shows blank | Low | Use a static map image as fallback |
| messacklaw.co.za DNS misconfiguration | Site unreachable on custom domain | Low | Document DNS setup steps; test with `dig` before going live |

## AI-Buildability Notes

- **Straightforward for AI**: The entire build. This is a single HTML file reproducing an existing sample with well-defined additions (mobile menu, contact form, map embed, SEO tags). No complex state, no authentication, no data model. An agent can build this end-to-end.
- **Needs human input**: Real image assets (logo, photos) must come from the firm. DNS configuration for the custom domain requires access to the domain registrar.
- **Low risk**: No novel algorithms, no complex integrations, no real-time features. The hardest part is pixel-matching the sample UI, which is straightforward given the HTML source is provided.


