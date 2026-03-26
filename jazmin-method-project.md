# Jazmín Method — Project Documentation

> Last updated: March 25, 2026  
> Live site: [jazmin-method.vercel.app](https://jazmin-method.vercel.app)  
> GitHub repo: `scottopiela/jazmin-method`  
> Vercel project ID: `prj_JC63RmLaDmI9NAEdcFNBMJ7p5gbg`  
> Vercel team: `scott-1869s-projects` (`team_03GkIOpCigaTDKyjL6c2a0Jg`)

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [File Structure](#2-file-structure)
3. [Brand Palette](#3-brand-palette)
4. [Typography](#4-typography)
5. [Main Landing Page — `index.html`](#5-main-landing-page--indexhtml)
6. [Thank You Page — `thank-you.html`](#6-thank-you-page--thank-youhtml)
7. [Page Section Reference](#7-page-section-reference)
8. [CSS Architecture](#8-css-architecture)
9. [JavaScript Behaviours](#9-javascript-behaviours)
10. [Assets](#10-assets)
11. [Email Integration](#11-email-integration)
12. [Deployment](#12-deployment)
13. [Content Inventory](#13-content-inventory)
14. [Design Decisions & Rationale](#14-design-decisions--rationale)
15. [Pending / Placeholder Items](#15-pending--placeholder-items)

---

## 1. Project Overview

A single-brand landing page and thank you page for the **Jazmín Method** — a sound-first Spanish language learning course by Jazmín, a Spanish Language Coach.

**Core proposition:** Learn Spanish through sound acquisition before grammar, with a Day 30 money-back guarantee of a real, unscripted conversation.

**Tech stack:**
- Pure HTML/CSS/JS — no framework, no build step
- Single self-contained HTML files (all assets base64-embedded)
- Google Fonts via CDN (`DM Sans`, `DM Serif Display`, `Unbounded`)
- Kit.com (ConvertKit) for email capture
- Vercel for hosting, auto-deployed from GitHub on push to `main`

---

## 2. File Structure

```
jazmin-method/
├── index.html          ← Main landing page (Cream Canvas theme)
├── thank-you.html      ← Post-signup confirmation page
├── vercel.json         ← Vercel routing config
├── .gitignore
└── README.md
```

### vercel.json

```json
{
  "version": 2,
  "builds": [
    { "src": "*.html", "use": "@vercel/static" }
  ],
  "routes": [
    { "src": "/thank-you", "dest": "/thank-you.html" },
    { "src": "/(.*)", "dest": "/index.html" }
  ],
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "Cache-Control", "value": "public, max-age=3600, stale-while-revalidate=86400" }
      ]
    }
  ]
}
```

**Routes:**
- `/` → `index.html`
- `/thank-you` → `thank-you.html`

---

## 3. Brand Palette

### Cream Canvas — Primary Theme

| Name | Hex | CSS Variable | Usage |
|------|-----|--------------|-------|
| Warm Cream | `#FBF5E6` | `--cream` | Hero background, page background, light surfaces |
| Espresso | `#1A1209` | `--espresso` | Primary text, CTA buttons, logo mark, features section bg |
| Aubergine | `#4A2C52` | `--aubergine` | Nav bar, quote section bg, hover states, thank you hero bg |
| Marigold | `#C8973A` | `--marigold` | Gold accent, ticker bar, highlights, logo colour, eyebrows |
| Tobacco | `#6B5B3E` | `--tobacco` | Body copy, muted text, supporting text |
| Deep Espresso | `#0E0A05` | `--deep` | Footer background |
| Cream Dark | `#F0E6D0` | `--cream-dark` | Alternate light surface (declared, available) |

### CSS Variable Declaration

```css
:root {
  --espresso:   #1A1209;
  --aubergine:  #4A2C52;
  --marigold:   #C8973A;
  --cream:      #FBF5E6;
  --tobacco:    #6B5B3E;
  --deep:       #0E0A05;
  --cream-dark: #F0E6D0;
}
```

### Section Background Mapping

| Section | Background |
|---------|------------|
| Nav | `--aubergine` (#4A2C52) |
| Hero | `--cream` (#FBF5E6) |
| Ticker bar | `--marigold` (#C8973A) |
| Features (01/02/03 cards) | `--espresso` (#1A1209) |
| Quote | `--aubergine` (#4A2C52) |
| Promise / Guarantee | `--espresso` (#1A1209) |
| CTA Closer | `--cream` (#FBF5E6) |
| Footer | `--deep` (#0E0A05) |

---

## 4. Typography

### Google Fonts Used

```html
<link href="https://fonts.googleapis.com/css2?family=Unbounded:wght@400;700;900&family=DM+Sans:ital,wght@0,300;0,400;0,600;0,700;1,400&family=DM+Serif+Display:ital@0;1&display=swap" rel="stylesheet">
```

### Font Usage Map

| Font | Weight/Style | Used For |
|------|-------------|----------|
| `Unbounded` | 900 | Logo/wordmark, hero headline (h1), feature numbers, nav CTA |
| `Unbounded` | 700 | Ticker bar text, resource card titles |
| `Unbounded` | 400 | General UI labels |
| `DM Serif Display` | italic | Section headings ("Why everything you've tried didn't work", quote text, promise h2, CTA h2) |
| `DM Serif Display` | regular | Available, not currently in use |
| `DM Sans` | 700 | Subheadings, button text, tagline, nav links |
| `DM Sans` | 600 | Compare eyebrow labels, step titles |
| `DM Sans` | 400 | Body copy, form inputs, footnotes |
| `DM Sans` | italic | Minor decorative use |

### Type Scale (Main Page)

```css
/* Hero headline */
.hero-h1  { font: Unbounded 900, clamp(46px, 7.5vw, 100px) }

/* Hero tagline */
.hero-tagline { font: DM Sans 700, 20px }

/* Hero sub-copy */
.hero-sub { font: DM Sans 400, 16px }

/* Section headings */
.features-h2 { font: DM Serif Display italic, clamp(28px, 3.5vw, 44px) }
.compare-h2  { font: DM Serif Display italic, clamp(26px, 3.2vw, 42px) }
.promise-h2  { font: DM Serif Display italic, clamp(24px, 3vw, 40px) }
.cta-h2      { font: DM Serif Display italic, clamp(28px, 4vw, 52px) }

/* Quote */
.quote-text  { font: DM Serif Display italic, clamp(16px, 2vw, 22px) }

/* Feature card titles */
.feat-title  { font: Unbounded 700, 13px }
.feat-num    { font: Unbounded 900, 48px (opacity .13) }

/* Eyebrows */
.features-eyebrow { font: DM Sans 700, 11px, letter-spacing .16em, uppercase }
```

---

## 5. Main Landing Page — `index.html`

### Page Title
`The Jazmín Method — Learn Spanish Today`

### Meta Description
`Jazmín's sound-first method puts you inside the language from Day 1. No grammar drills. Real conversation by Day 30 — guaranteed.`

### Section Flow

```
NAV
 └─ Aubergine bar · Logo "Jazmín" (Marigold) · Links: The Method, The Promise, Get Started · CTA button

HERO
 └─ Cream bg · Dot texture overlay · Warm radial glow
    LEFT COLUMN:
      Eyebrow: "El método que sí funciona"
      H1 (bilingual, rotating): "Learn / Spanish / Today!" ↔ "¡Habla / Español / Hoy!"
      Tagline: "Hear Spanish. Speak Spanish. Live Spanish."
      Sub-copy: "Jazmín's sound-first method puts you inside..."
      Form: email input + "Start Free →" (Aubergine button)
      Footnote: "🇲🇽 No credit card · Real conversation by Day 30 · Cancel anytime"
    RIGHT COLUMN:
      Photo card (1:1 aspect ratio, Marigold border, Espresso footer)
      Rotating photos: thumbs up → pointing (3.5s crossfade)
      Dot nav indicators

TICKER (Marigold bg)
 └─ "Sound before grammar ✦ Spanish has 5 vowels ✦ Day 30 Guarantee ✦ No grammar drills ✦ Real conversation by Day 30 ✦ Start today · It's free"

FEATURES (Espresso bg, id="method")
 └─ Eyebrow: "The Method"
    H2: "Why everything you've tried didn't work." (DM Serif Display italic)
    Intro: "Most courses teach you about Spanish..."
    Grid (3 cards):
      01 — Sound before grammar
      02 — Spanish has 5 vowels. English has 15.
      03 — The Day 30 Promise

QUOTE (Aubergine bg)
 └─ Eyebrow: "Student Testimonial"
    Quote: Maria T., Miami FL (full testimonial)
    Cite: "— Maria T. · Miami, FL"

PROMISE (Espresso bg, id="promise")
 └─ Eyebrow: "The Guarantee"
    H2: "The Day 30 Promise." (DM Serif Display italic)
    Body: "By Day 30 of this course you will have a real, unscripted conversation..."
    Closing line (Marigold italic): "We have never had to honour this refund..."
    Badge: "30 / Day Promise" (circular, Marigold border)

CTA CLOSER (Cream bg, id="start")
 └─ Eyebrow: "Start today · It's free"
    H2: "Ready to actually speak Spanish?" (DM Serif Display italic)
    Body copy
    Form: email input + "Get Day 1 Free →"
    Footnote: "No spam · Unsubscribe anytime · Founding student pricing locked in"
    Sig block: circular headshot + Jazmín signature + "Spanish Language Coach"

FOOTER (Deep Espresso bg)
 └─ Logo "Jazmín" (Marigold) · Links: The Method, The Promise, Get Started, Privacy · © 2025
```

---

## 6. Thank You Page — `thank-you.html`

**URL:** `/thank-you`

### Page Title
`¡Bienvenida! — The Jazmín Method`

### Purpose
Post-signup confirmation page shown after email form submission. Congratulatory tone, Day 1 onboarding guidance, educational resource placeholders.

### Section Flow

```
NAV
 └─ Aubergine bar · Logo + tagline "El método que sí funciona"

HERO (Aubergine bg, text-centred)
 └─ Circular headshot (new sofa photo, face/shoulders crop, Marigold border)
    "¡Hola!" (Unbounded 900, Marigold)
    Flag: "🇲🇽 Welcome to Day 1 of your Spanish journey"
    H1: "You just took the most important step. Let's make it count." (DM Serif Display italic)
    Body: "Your first lesson is on its way to your inbox..."
    Badge: "✓ You're on the list — check your inbox for Day 1"
    Jazmín signature (transparent PNG, white on Aubergine)

TICKER (Marigold bg)
 └─ "You belong here ✦ Sound before grammar ✦ Spanish has 5 vowels ✦ Day 30 Guarantee ✦ No grammar drills ✦ Your ear will wake up ✦ Speak from Day 1"

WHAT HAPPENS NEXT (Cream bg)
 └─ Eyebrow: "Your journey starts now"
    H2: "What happens in the next 30 days."
    4 numbered steps:
      1 — Check your inbox · tag: "Do this today"
      2 — 10 minutes a day, same time every day · tag: "This week"
      3 — Don't try to speak yet — just listen · tag: "Days 1–7"
      4 — By Day 30 — a real, unscripted conversation · tag: "The guarantee"

RESOURCES (Espresso bg)
 └─ Eyebrow: "Day 1 toolkit"
    H2: "Resources to explore while you wait."
    6 resource cards (all placeholder links):
      🎧 Audio Lesson — The 5 Spanish Vowels (coming in Day 1 email)
      📖 Quick Read — Why Your Brain Hasn't Been Ready for Spanish
      🎙️ Podcast Recommendation — Slow Spanish Podcasts for Beginners
      ✍️ Free Download — The 50 Most Useful Spanish Phrases in Context
      📺 Video — Jazmín Explains the Method in 8 Minutes
      💬 Community — Join the Student Community

ENCOURAGEMENT (Aubergine bg)
 └─ Jazmín quote: "The students who get to Day 30 aren't the ones with the most time..."
    Cite: "— Jazmín · Spanish Language Coach"

CTA (Cream bg)
 └─ H2: "Your inbox is waiting. ¡Vámonos!"
    Body copy
    Button: "← Back to jazminmethod.com"
    Note: "Questions? Reply to your welcome email and Jazmín reads every one."

FOOTER (Deep Espresso bg)
 └─ Logo + © 2025
```

---

## 7. Page Section Reference

### CSS Class → Section Mapping

#### Main Page (`index.html`)

| CSS Class | Section | Background |
|-----------|---------|------------|
| `.nav` | Navigation bar | `--aubergine` |
| `.hero` | Hero panel | `--cream` |
| `.ticker` | Scrolling ticker | `--marigold` |
| `.features` | Method + 3 cards | `--espresso` (#1A1209 hardcoded) |
| `.quote-section` | Testimonial | `--aubergine` |
| `.promise` | Day 30 Guarantee | `--espresso` |
| `.cta-closer` | Final CTA + signature | `--cream` |
| `footer` | Site footer | `--deep` |

#### Thank You Page (`thank-you.html`)

| CSS Class | Section | Background |
|-----------|---------|------------|
| `.nav` | Navigation bar | `--aubergine` |
| `.hero` | ¡Hola! celebration | `--aubergine` |
| `.ticker` | Scrolling ticker | `--marigold` |
| `.next` | 30-day roadmap | `--cream` |
| `.resources` | 6 resource cards | `--espresso` |
| `.encouragement` | Jazmín quote | `--aubergine` |
| `.cta-section` | Back to site | `--cream` |
| `footer` | Footer | `--deep` |

---

## 8. CSS Architecture

All CSS is inline within each HTML file inside a single `<style>` block. No external stylesheets.

### Key Layout Patterns

```css
/* Hero — 2-column grid */
.hero-inner {
  display: grid;
  grid-template-columns: 1fr 400px;
  gap: 52px;
  align-items: center;
}

/* Feature cards — 3-column grid */
.features-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 18px;
}

/* CTA closer — 2-column (copy + sig) */
.cta-closer-inner {
  display: grid;
  grid-template-columns: 1fr auto;
  gap: 60px;
}

/* Promise — 2-column (copy + badge) */
.promise-inner {
  display: grid;
  grid-template-columns: 1fr auto;
  gap: 48px;
}
```

### Responsive Breakpoints

```css
/* Tablet / small desktop */
@media (max-width: 900px) {
  .hero-inner           → grid-template-columns: 1fr
  .cta-closer-inner     → grid-template-columns: 1fr
  .features-grid        → grid-template-columns: 1fr
  .promise-inner        → grid-template-columns: 1fr
  .nav-links            → display: none
  footer                → flex-direction: column
}

/* Mobile */
@media (max-width: 540px) {
  .hero-form, .cta-form → flex-direction: column; gap: 8px
  .hero-fi, .cta-fi     → border-radius: 100px (full pill, standalone)
  .hero-fb, .cta-fb     → border-radius: 100px
  .hero                 → padding: 40px 5% 60px
}
```

### Photo Card (Hero)

```css
.hero-card {
  aspect-ratio: 1/1;          /* square, matches photo dimensions */
  height: auto;
  max-height: 500px;
  border: 3px solid var(--marigold);
  border-radius: 14px;
  background: linear-gradient(175deg, #f5e8cc 0%, #FBF5E6 100%);
  box-shadow: 8px 8px 0 rgba(26,18,9,.12);
}

.hero-card .photo-slide {
  position: absolute;
  bottom: 48px; left: 0;
  width: 100%;
  height: calc(100% - 48px);  /* reserves space for footer strip */
  object-fit: contain;
  object-position: center bottom;
  transition: opacity .8s ease, transform .8s ease;
}
```

### Feature Card Colour Variants

```css
.feat-card:nth-child(1) { background: rgba(255,255,255,.06);  border-color: rgba(255,255,255,.1) }
.feat-card:nth-child(2) { background: rgba(200,151,58,.14);   border-color: rgba(200,151,58,.35) }
.feat-card:nth-child(3) { background: rgba(74,44,82,.2);      border-color: rgba(74,44,82,.45) }
```

### Signature Image

The signature PNG is processed to be transparent:
- Source: black ink on black bg RGB PNG
- Processed: pixel brightness extracted as alpha channel → white RGBA PNG (3× upscaled)
- Result: white script on transparent background, renders over any colour
- CSS: `opacity: 1; background: transparent;` (no blend mode needed)

---

## 9. JavaScript Behaviours

### Photo Slideshow

```js
// Auto-advances every 3,500ms
// Cross-fades between 2 photos: thumbs-up → pointing
// Dot indicators are clickable to jump to any slide
const INTERVAL = 3500;
setInterval(() => setSlide('hero', slides['hero'] + 1), INTERVAL);
```

### Bilingual Headline Rotation

```js
// Alternates every 3,200ms between:
const EN = ['Learn',  'Spanish', 'Today!'];
const ES = ['¡Habla', 'Español', 'Hoy!'];

// CSS fade animation on each span:
@keyframes hSwitch {
  from { opacity: 0; transform: translateY(6px) }
  to   { opacity: 1; transform: translateY(0) }
}
```

### Kit.com Email Form Submission

```js
const KIT = 'https://app.convertkit.com/forms/e59f04d7a6/subscriptions';

// Intercepts all forms with class="kf"
// POST to Kit endpoint via fetch()
// On success OR error: replaces form with inline success message
// Success message: "✓ You're on the list! Check your inbox for Day 1. 🇲🇽"
```

### Ticker Animation

```css
@keyframes tickScroll {
  from { transform: translateX(0) }
  to   { transform: translateX(-50%) }
}
/* Items duplicated 3× so loop is seamless */
/* Duration: 28s on main page, 30s on thank-you page */
```

---

## 10. Assets

All assets are base64-embedded inline within the HTML files. No external image requests.

### Photos

| Asset | Description | Used In | Notes |
|-------|-------------|---------|-------|
| Transparent thumbs-up | Jazmín, thumbs up, white bg removed | `index.html` hero card slide 1 | PNG with alpha |
| Transparent pointing | Jazmín, pointing left, white bg removed | `index.html` hero card slide 2 | PNG with alpha |
| Original headshot | Jazmín, professional portrait | `index.html` CTA sig block | JPEG |
| Thank you hero photo | Jazmín on sofa, cropped face/shoulders | `thank-you.html` hero circle | JPEG, 600×600 |

### Signature

| Asset | Description | Used In | Notes |
|-------|-------------|---------|-------|
| Jazmín signature | Handwritten "Jazmin" script | Both pages | Processed to transparent PNG (white ink) |

**Signature processing:** The source PNG (125×40px, black ink on black bg) is processed in Python — pixel brightness becomes the alpha channel, all pixels set to white (RGB 255,255,255), result upscaled 3× to 375×120px for crispness. Renders white on any background without blend modes.

---

## 11. Email Integration

**Provider:** Kit.com (ConvertKit)  
**Form UID:** `e59f04d7a6`  
**Endpoint:** `https://app.convertkit.com/forms/e59f04d7a6/subscriptions`  
**Script tag (not used — using direct API):** `https://test-872.kit.com/e59f04d7a6/index.js`

### Forms

| Page | Location | Button Text |
|------|----------|-------------|
| `index.html` | Hero panel | "Start Free →" |
| `index.html` | CTA Closer | "Get Day 1 Free →" |
| `thank-you.html` | (confirmation only, no form) | — |

### To update Kit form UID

Search for `e59f04d7a6` in both HTML files and replace with your new form UID.

---

## 12. Deployment

### Stack

- **Hosting:** Vercel (static)
- **Source:** GitHub `scottopiela/jazmin-method`, branch `main`
- **Auto-deploy:** Yes — every push to `main` triggers a new Vercel deployment (~30 seconds)
- **Custom domain:** `www.jazminmethod.com` (DNS pointed to Vercel)

### Deploy Process

```bash
# Make changes to index.html or thank-you.html
git add index.html thank-you.html
git commit -m "Your change description"
git push origin main
# Vercel auto-deploys in ~30 seconds
```

### Manual Deploy (Drag & Drop)

1. Go to [vercel.com/new](https://vercel.com/new)
2. Drag the `jazmin-site` folder onto the deploy zone
3. Vercel deploys as a static site

---

## 13. Content Inventory

### Main Page Copy

#### Nav
- Logo: `Jazmín`
- Links: `The Method` · `The Promise` · `Get Started`
- CTA: `Get Day 1 Free →`

#### Hero
- Eyebrow: `El método que sí funciona`
- Headline (EN): `Learn / Spanish / Today!`
- Headline (ES): `¡Habla / Español / Hoy!`
- Tagline: `Hear Spanish. Speak Spanish. Live Spanish.`
- Sub-copy: `Jazmín's sound-first method puts you inside the language from Day 1 — no grammar drills, no vocab lists, no frustration.`
- Form placeholder: `Your email address`
- Button: `Start Free →`
- Footnote: `🇲🇽 No credit card · Real conversation by Day 30 · Cancel anytime`
- Card label: `Jazmín · Tu maestra · Your coach`

#### Features Section
- Eyebrow: `The Method`
- H2: `Why everything you've tried didn't work.`
- Intro: `Most courses teach you about Spanish. Jazmín puts you inside it — from your very first lesson. The brain acquires language the same way in every person. Align with that process and Spanish becomes inevitable, not effortful.`

| Card | Title | Body |
|------|-------|------|
| 01 | Sound before grammar | Train your ear before your mouth. Every brain acquires language through sound first — starting Day 1, not page 200 of a textbook. |
| 02 | Spanish has 5 vowels. English has 15. | Once your ear is calibrated, the fog lifts. Words stick without memorization. This is the insight most teachers never share. |
| 03 | The Day 30 Promise | A real, unrehearsed conversation in Spanish — with another human being — by Day 30. Guaranteed, or Jazmín keeps working with you until it happens. |

#### Quote
- Eyebrow: `Student Testimonial`
- Quote: `"I took classes for two years, did the apps, bought the workbooks. I could read okay but the moment a native speaker opened their mouth I was lost. Jazmín's approach flipped everything — we started with listening and speaking from day one, no grammar charts, no memorising. Within a few weeks I wasn't just understanding more, I was actually responding. It felt less like studying and more like my ear finally woke up."`
- Attribution: `— Maria T. · Miami, FL`

#### Promise / Guarantee
- Eyebrow: `The Guarantee`
- H2: `The Day 30 Promise.`
- Body: `By Day 30 of this course you will have a real, unscripted conversation in Spanish with another person. Not a rehearsed phrase. Not a memorised script. A real conversation. If that doesn't happen, you get every dollar back — no questions, no forms, no friction.`
- Closing (Marigold): `We have never had to honour this refund. We don't expect to start with you.`
- Badge: `30 · Day Promise`

#### CTA Closer
- Eyebrow: `Start today · It's free`
- H2: `Ready to actually speak Spanish?`
- Body: `Get your free Day 1 lesson the moment you sign up. No credit card. No commitment. Real conversation by Day 30 — guaranteed.`
- Button: `Get Day 1 Free →`
- Footnote: `No spam · Unsubscribe anytime · Founding student pricing locked in`
- Sig: `Spanish Language Coach · Founder, The Jazmín Method`

#### Footer
- Logo: `Jazmín`
- Links: `The Method` · `The Promise` · `Get Started` · `Privacy`
- Copyright: `© 2025 The Jazmín Method`

---

### Thank You Page Copy

#### Hero
- Greeting: `¡Hola!`
- Flag: `🇲🇽 Welcome to Day 1 of your Spanish journey`
- H1: `You just took the most important step. Let's make it count.`
- Body: `Your first lesson is on its way to your inbox right now. Before it arrives, take a breath — and know that you don't need to memorise a single thing today. That's not how this works. Today, your only job is to listen.`
- Badge: `✓ You're on the list — check your inbox for Day 1`

#### 30-Day Roadmap Steps

| # | Title | Tag |
|---|-------|-----|
| 1 | Check your inbox — your Day 1 lesson is waiting | Do this today |
| 2 | Give yourself 10 minutes a day — same time, every day | This week |
| 3 | Don't try to speak yet — just listen | Days 1–7 |
| 4 | By Day 30 — a real, unscripted conversation | The guarantee |

#### Resource Cards (Placeholder)

| Icon | Type | Title | CTA | Status |
|------|------|-------|-----|--------|
| 🎧 | Audio Lesson | The 5 Spanish Vowels — Your First 10 Minutes | Coming in your Day 1 email | Placeholder |
| 📖 | Quick Read · 3 min | Why Your Brain Hasn't Been Ready for Spanish — Until Now | Read the article | Link to add |
| 🎙️ | Podcast Recommendation | Slow Spanish Podcasts for Beginners | See the list | Link to add |
| ✍️ | Free Download | The 50 Most Useful Spanish Phrases — In Context | Download the guide | Link to add |
| 📺 | Video · 8 min | Watch: Jazmín Explains the Method in 8 Minutes | Watch the video | Link to add |
| 💬 | Community | Join the Student Community | Join the group | Link to add |

#### Encouragement Quote
- Quote: `"The students who get to Day 30 aren't the ones with the most time or the most talent. They're the ones who listened first and trusted the process. You just proved you're one of them."`
- Attribution: `— Jazmín · Spanish Language Coach`

#### Closing CTA
- H2: `Your inbox is waiting. ¡Vámonos!`
- Body: `Everything starts with that first email. Open it, follow the one instruction, and you're already further along than most people who've "tried to learn Spanish" for years.`
- Button: `← Back to jazminmethod.com`
- Note: `Questions? Reply to your welcome email and Jazmín reads every one.`

---

## 14. Design Decisions & Rationale

### Single-file Architecture
All assets (photos, signature) are base64-embedded so the site works as a portable single file with zero external dependencies beyond Google Fonts. This simplifies deployment, eliminates 404 risks, and means the file can be previewed locally by just opening it in a browser.

### Cream Canvas Theme
Selected from 7 colour theme explorations as the primary brand direction. Warm Cream hero creates warmth and approachability. Aubergine nav and quote sections add depth and sophistication. Marigold gold provides the accent energy without being aggressive.

### Photo Card Approach
The hero uses a 1:1 aspect-ratio card with `object-fit: contain` and a gradient background matching the hero colour. This ensures photos with different compositions always show fully without cropping, while the gradient background makes the card feel intentional rather than showing letterboxing.

### Bilingual Headline
The hero headline rotates between English ("Learn Spanish Today!") and Spanish ("¡Habla Español Hoy!") every 3.2 seconds. This creates immediate emotional resonance with both Spanish learners (who see where they're going) and the brand voice.

### Signature Transparency
The handwritten signature PNG files had no alpha channel (black or white ink on solid backgrounds). These are processed programmatically to extract pixel brightness as an alpha channel, creating proper transparent PNGs that render cleanly on any background colour.

### DM Serif Display for Headings
All major section headings use DM Serif Display italic — the same font as the homepage "Why everything you've tried didn't work" heading. This creates visual rhythm and a warm editorial quality that distinguishes section headers from the sharper Unbounded display font used for the hero.

---

## 15. Pending / Placeholder Items

### Content to Fill In (Thank You Page)

| Item | Location | Notes |
|------|----------|-------|
| Article link | Resource card 2 | "Why Your Brain Hasn't Been Ready for Spanish" |
| Podcast list link | Resource card 3 | Slow Spanish Podcasts for Beginners |
| PDF download link | Resource card 4 | 50 Most Useful Spanish Phrases guide |
| Video link | Resource card 5 | 8-minute method explainer video |
| Community link | Resource card 6 | Student community / conversation partner group |
| Day 1 audio | Resource card 1 | Delivered via Kit email, not a link |

### Technical Items

| Item | Priority | Notes |
|------|----------|-------|
| Privacy policy page | Medium | Footer links to `#` |
| Thank you page redirect from Kit | High | Kit form currently redirects to same page — should redirect to `/thank-you` |
| Custom domain SSL | Done | `jazminmethod.com` via Vercel |
| OG/social preview tags | Medium | No `og:image` currently set |
| Favicon | Low | Not currently set |
| Google Analytics / tracking | TBD | No analytics currently on the page |

### Kit.com Redirect Setup

To send users to the thank you page automatically after form submission, update the Kit form settings:

1. In Kit dashboard → Forms → select form `e59f04d7a6`
2. Settings → "Redirect to a custom URL after subscription"
3. Enter: `https://www.jazminmethod.com/thank-you`

---

*End of documentation.*
