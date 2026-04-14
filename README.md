# PillRem Website

Marketing website for **PillRem** — the calm medication reminder app for iPhone.
Domain: `https://pillrem.com`

## Stack

Intentionally minimal: **static HTML + embedded CSS + vanilla JS**. No build step, no framework, no npm install. Drop the `website/` folder onto any static host (Netlify, Cloudflare Pages, Vercel, GitHub Pages, S3 + CloudFront, etc.) and it works.

## File structure

```
website/
├── index.html           # Single-page marketing site (all sections, embedded CSS)
├── robots.txt           # Crawler directives
├── sitemap.xml          # Google / Bing sitemap with image sitemap entries
├── README.md            # You are here
└── assets/
    └── screenshots/     # Five iPhone screenshots (copied from /screenshots/final/)
```

## Design system (aligned with iOS app)

The website uses the **Calm Apothecary** palette and typography matched exactly to the SwiftUI `DS` namespace in the iOS app:

| Token | Hex | Use |
|---|---|---|
| `--bg` | `#FAF7F2` | Warm ivory canvas |
| `--bg-dim` | `#F2EEE4` | Section backgrounds |
| `--primary` | `#3B6AA0` | Deep refined blue — primary brand |
| `--primary-dark` | `#2A4E7A` | Hover / dark CTA |
| `--sage` | `#7BA088` | Positive accent (adherence, success) |
| `--peach` | `#E8C4A0` | Warm highlight (morning / family) |
| `--amber` | `#D4A574` | Star ratings, highlights |
| `--rose` | `#C17B7B` | Soft warning / error |
| `--lavender` | `#9B8FB5` | Evening / night moments |
| `--text` | `#2A3142` | Primary text |
| `--text-secondary` | `#7A8094` | Body text |

**Typography**:
- Display: **Fraunces** (variable serif, Google Fonts) — used for all headlines, pull-quotes, and "editorial moments". Italic variant with `SOFT` axis is used for the primary-coloured emphasis in headings.
- Body: **DM Sans** (Google Fonts) — used for all body copy, navigation, and UI text.

This pairing gives the "Editorial Apothecary" aesthetic — part high-end wellness publication, part modern pharmacy.

## SEO strategy

The site is optimised for **Google Search**, **Bing**, and **Apple's App Store web crawlers**. Key tactics in `index.html`:

### 1. On-page SEO
- **`<title>`** leads with primary keyword: `"PillRem — Medication Reminder App for iPhone | Never Miss a Dose"`
- **`<meta name="description">`** packs 3–4 primary keywords naturally (156 chars)
- **`<meta name="keywords">`** listed for Bing/Yandex (Google ignores it, but no harm)
- **Canonical URL** set to `https://pillrem.com/`
- **`hreflang`** ready (currently `en` only; add regional variants if you localise)
- **`robots`** allows `max-image-preview:large` for rich image results

### 2. Structured data (JSON-LD)
Three schema blocks that both Google and Bing read:
1. **`SoftwareApplication`** — tells search engines this is an iOS app (category, price, aggregate rating, operating system). This is what makes the app show up with a rating stars snippet in SERPs.
2. **`FAQPage`** — every FAQ question is structured so Google can render them as FAQ rich results directly in search results (huge for CTR on long-tail queries).
3. **`Organization`** — basic brand entity.

### 3. Open Graph + Twitter Card
Full social preview support so links shared to iMessage, Twitter/X, LinkedIn, Slack render with the hero screenshot and headline.

### 4. Keyword placement (strategic, not stuffed)

| Keyword | Where it appears |
|---|---|
| `medication reminder app` | H1 subtext, features intro, FAQ, footer |
| `pill reminder app` | Problem section, FAQ |
| `medication tracker` | Showcase section, FAQ |
| `best medication reminder app iPhone` | FAQ question (matches exact search query) |
| `caregiver medication management` | FAQ, family-profiles feature |
| `medication adherence tracker` | Adherence feature, stats strip |
| `pill tracker app` | Showcase section |
| `daily pill reminder` | Hero sub |
| `doctor-ready PDF reports` | Feature card, FAQ |
| `elderly medication reminder` | FAQ question |

### 5. Image SEO
- Every `<img>` has descriptive, keyword-rich `alt` text
- `sitemap.xml` includes an **image sitemap extension** — tells Google/Bing about each screenshot with its own title/caption
- `fetchpriority="high"` on the hero screenshot for Core Web Vitals (LCP)
- Other images `loading="lazy"` for performance

### 6. Performance (helps SEO)
- Single HTML file, inline CSS, inline JS — zero render-blocking external stylesheets
- Google Fonts `preconnect` hints
- No framework overhead, no JavaScript bundles
- Subtle noise texture uses inline SVG data URI (no extra request)
- `prefers-reduced-motion` respected
- Expected Lighthouse: 95+ performance, 100 accessibility, 100 SEO, 100 best practices

### 7. Core Web Vitals readiness
- LCP: hero screenshot marked `fetchpriority="high"`
- CLS: explicit `width`/`height` on the hero image
- INP: all interactions (FAQ accordion, nav) use native `<details>` — no JS cost

## Before you ship

1. **Replace placeholders** in `<head>`:
   - `google-site-verification` content (Google Search Console)
   - `msvalidate.01` content (Bing Webmaster Tools)
2. **Update the App Store URL** — replace the `href="#download"` and `href="#"` on App Store buttons with your real App Store link once the app is live.
3. **Create the legal pages** referenced in the footer: `privacy.html`, `terms.html`, `security.html`, `about.html`, `blog.html`, `press.html`. The sitemap already lists privacy.html and terms.html.
4. **Add a favicon**: create `/favicon.ico` and `/apple-touch-icon.png` at the site root and add `<link rel="icon">` tags.
5. **Update sitemap dates** whenever you change content (`<lastmod>`).
6. **Submit to search engines** after launch:
   - Google: <https://search.google.com/search-console> — add property, submit `sitemap.xml`
   - Bing: <https://www.bing.com/webmasters> — add site, submit `sitemap.xml`
7. **Set up analytics** that respects privacy (Plausible, Fathom, or self-hosted Umami). Avoid Google Analytics if privacy is part of your brand story.

## Testing locally

```bash
cd website
python3 -m http.server 8000
# Open http://localhost:8000
```

Or use any static server you like (`npx serve`, `caddy`, etc.).

## Keyword search volume reference

Rough monthly search volumes (US, as a planning guide — verify with Google Keyword Planner or Ahrefs before major decisions):

| Keyword | Est. monthly volume | Intent |
|---|---|---|
| medication reminder app | 14,000 | Commercial — download |
| pill reminder app | 9,900 | Commercial — download |
| medication tracker | 8,100 | Commercial / informational |
| best medication reminder app | 2,400 | Commercial — comparison |
| pill tracker app | 2,100 | Commercial — download |
| medication reminder for elderly | 1,600 | Commercial — caregiver |
| daily pill reminder | 1,300 | Commercial / informational |
| medication adherence app | 880 | Commercial — clinical |

The FAQ section is designed to rank for every question-based variant of these.
