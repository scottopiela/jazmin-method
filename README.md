# Jazmín Method — Landing Page

A landing page for the Jazmín Method Spanish learning program, featuring 7 color themes, rotating hero images, and a Kit.com email signup integration.

## Project Structure

```
jazmin-site/
├── index.html      ← The complete site (all 7 themes, all assets embedded)
├── vercel.json     ← Vercel deployment config
├── .gitignore
└── README.md
```

## Color Themes

The site includes 7 selectable color variants accessible via the top nav:

| Theme | Description |
|-------|-------------|
| C1 · Cream Canvas | Warm Cream hero, Aubergine nav, Marigold accents |
| C2 · Aubergine Night | Aubergine hero, deep purple nav, gold accents |
| C3 · Marigold Bloom | Marigold hero, Espresso nav, Cream card |
| C4 · Espresso & Cream | Dark Espresso hero, Marigold gold accents |
| A1 · Coral Fuego | Bold coral hero, chartreuse accents, cobalt card |
| A4 · Cenote | Deep teal hero, electric turquoise + hot pink |
| B1 · Medianoche | Near-black hero, neon magenta + gold |

## Features

- **Rotating hero photos** — 3 images cross-fade every 3.5s with dot navigation
- **Bilingual headline** — cycles between *¡Habla Español Hoy!* and *Learn Spanish Today!*
- **Kit.com email signup** — wired to form ID `e59f04d7a6`
- **Scrolling ticker** — animated marquee between hero and features
- **Fully self-contained** — single HTML file, no external dependencies except Google Fonts

## Email Integration

Forms submit to Kit (ConvertKit):
```
https://app.convertkit.com/forms/e59f04d7a6/subscriptions
```

To change the Kit form, search for `e59f04d7a6` in `index.html` and replace with your form UID.

## Deploy to Vercel

### Option 1 — Drag & Drop
1. Go to [vercel.com/new](https://vercel.com/new)
2. Drag this entire folder onto the deploy zone
3. Name the project → Deploy

### Option 2 — Vercel CLI
```bash
npm install -g vercel
cd jazmin-site
vercel
```

### Option 3 — GitHub Auto-Deploy (recommended)
1. Push this repo to GitHub
2. Go to [vercel.com/new](https://vercel.com/new) → Import Git Repository
3. Select this repo → Deploy
4. Every push to `main` auto-deploys

## Local Preview

No build step needed — just open `index.html` in any browser:
```bash
open index.html
# or
python3 -m http.server 8080
# then visit http://localhost:8080
```

## Updating Content

All content is in `index.html`. Key sections to update:

- **Headlines** — search for `¡Habla` to find the hero h1 spans
- **Kit form ID** — search for `e59f04d7a6`
- **Waitlist count** — search for `000+` and replace with real number
- **Frank quote** — search for `Frank` to find the testimonial
- **Photos** — base64-encoded inline; replace by encoding new images and swapping the `src` values on `.photo-slide` img tags

## Brand Colors

| Name | Hex | Usage |
|------|-----|-------|
| Espresso | `#1A1209` | Primary text, CTA buttons |
| Aubergine | `#4A2C52` | Secondary accent, section backgrounds |
| Marigold | `#C8973A` | Gold accent, highlights |
| Warm Cream | `#FBF5E6` | Page background, light surfaces |
| Tobacco | `#6B5B3E` | Body copy, supporting text |
