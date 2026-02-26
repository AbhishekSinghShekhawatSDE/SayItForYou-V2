# SayItForYou

Anonymous message delivery on Instagram. You write it. We deliver it.

Live site: [sayitforyou.fun](https://www.sayitforyou.fun)
Instagram: [@sayitforyou.fun](https://www.instagram.com/sayitforyou.fun)

---

## What It Does

SayItForYou lets anyone send an anonymous message to another person on Instagram without direct contact. You fill out a form, our team produces an Instagram reel from your words, and we deliver it to the recipient — after asking for their consent first.

**Message types supported:**
- Apology
- Confession
- Love message
- General personal message
- Custom (any type you describe)

**Core promise:** If you choose anonymous, your name and Instagram handle never appear anywhere — not in the reel, not in the DM to the recipient.

---

## How It Works

1. **You write** — Fill out the form on the site. Takes two minutes.
2. **We produce** — Our team turns your message into a polished Instagram reel with design, music, and tone.
3. **We ask for consent** — We DM the recipient privately and ask if they want to receive a message.
4. **We deliver** — If they agree, we deliver. If they decline, we notify you. Nothing goes live without consent.

---

## Project Structure

```
sayitforyou/
├── index.html              # Main site — hero, form, how it works, testimonials, FAQ
├── Privacy Policy.html     # Privacy policy page (rename to privacy-policy.html)
├── assets/
│   ├── favicon.png         # Site icon — 512x512 PNG
│   ├── hero-video.webm     # Background video for hero section
│   └── social-card.png     # OG image — 1200x630 PNG (create this)
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla HTML, CSS, JavaScript — single file, no build step |
| Icons | Font Awesome 6.5 via CDN |
| Fonts | Inter via Google Fonts |
| Form backend | Google Apps Script (REST endpoint) |
| Hosting | Any static host (current: custom domain) |
| Video | WebM format, autoplay muted loop |

No frameworks. No npm. No dependencies to maintain.

---

## Form Backend

The form posts JSON to a Google Apps Script endpoint. The script writes submissions to a Google Sheet.

**Endpoint:**
```
https://script.google.com/macros/s/AKfycbwBEPy7FO2BYMtgt1IsLjMaFrCEf_PltodMpblAVv2CvnZj7gOXRhg8k0yeiiMy1xmVHw/exec
```

**Fields submitted:**

| Field | Required | Notes |
|---|---|---|
| `yourName` | No | Sender's first name |
| `yourInstagram` | Yes | Sender's handle, internal only |
| `anonymityChoice` | Yes | `"Anonymous"` or `"Reveal Identity"` |
| `messageType` | Yes | Apology / Confession / Love Message / Personal / Other |
| `otherMessageType` | No | Shown only when type is "Other" |
| `recipientInstagram` | Yes | Who receives the message |
| `additionalInfo` | No | Background context, internal only |
| `message` | Yes | The actual message, 600 char limit |

**Expected response:**
```json
{ "status": "success" }
```

On success, the page unlocks scroll, shows the success view, and closes the sheet after 5 seconds. On error, an inline error message appears and the form resets.

---

## Page Flow

```
Load site
  └─ Body overflow: hidden (scroll locked)
  └─ Hero visible — video background, headline, CTA button

User taps "Send an Anonymous Message"
  └─ Bottom sheet slides up (mobile)
  └─ Modal appears centered (desktop ≥640px)
  └─ Form fields displayed

User fills form and submits
  └─ Spinner shows, button disabled
  └─ POST to Google Apps Script
  └─ On success:
       ├─ Success view shown inside sheet
       ├─ Page unlocks (overflow: auto) after 2.5 seconds
       ├─ Scroll hint appears at hero bottom
       └─ Sheet closes after 5 seconds

User scrolls down
  └─ How It Works section (bento grid)
  └─ Mission section
  └─ Testimonials (1-col mobile, auto-grid desktop)
  └─ FAQ accordion
  └─ Instagram CTA
  └─ Footer
```

---

## Design System

```css
/* Gradient — Instagram palette */
--grad: linear-gradient(135deg, #833AB4 0%, #C13584 45%, #E1306C 80%, #F56040 100%);

/* Gradient text */
--grad-text: linear-gradient(100deg, #c86dd7 0%, #f06292 50%, #ff9f9f 100%);

/* Backgrounds */
--dark:  #0a0a0f
--dark2: #111118

/* Motion */
--spring: cubic-bezier(.34, 1.56, .64, 1)   /* bouncy opens */
--smooth: cubic-bezier(.32, .72, 0, 1)       /* fast exits */
```

Typography: Inter, weights 300–900 + italic 800.
Icons: Font Awesome 6.5 Free.
Border radius: 18–24px for cards, 50px for pills and buttons.
Glass effect: `backdrop-filter: saturate(180%) blur(22px)` with `rgba(255,255,255,.06)` backgrounds.

---

## SEO Implementation

### Meta Tags

| Tag | Value |
|---|---|
| Title | SayItForYou \| Send Anonymous Messages on Instagram (55 chars) |
| Description | 155-char description with CTA and key terms |
| Keywords | 8 keyword phrases targeting search intent |
| Robots | `index, follow, max-snippet:-1, max-image-preview:large` |
| Googlebot | Same as robots |
| Canonical | `https://www.sayitforyou.fun/` |
| hreflang | `en` + `x-default` |

### Open Graph

All required tags present: `og:type`, `og:url`, `og:title`, `og:description`, `og:image`, `og:image:width` (1200), `og:image:height` (630), `og:image:alt`, `og:image:type`, `og:locale`, `og:site_name`.

### Twitter Card

`summary_large_image` card with `twitter:site`, `twitter:creator`, title, description, image, and alt text.

### Schema Markup (JSON-LD)

Eight structured data blocks on the homepage:

| Schema Type | Purpose |
|---|---|
| `Organization` | Brand identity, logo, social links, contact point |
| `WebSite` | Site-level signals for Google |
| `Service` | Core offering with offer catalog (4 message types) |
| `HowTo` | 4-step process — feeds Google SGE and voice answers |
| `FAQPage` | 7 questions — appear as expandable results in Google |
| `BreadcrumbList` | Navigation signal |
| `WebApplication` | Signals interactive app to crawlers |
| `ItemList` | 3 user reviews with rating values |

Privacy Policy page has: `WebPage` (with `datePublished` + `dateModified`), `BreadcrumbList` (2 levels), `Organization`.

### GEO Meta

`geo.region: IN`, `geo.country: India`, `coverage: Worldwide`, `distribution: Global`. Targets regional crawlers (Bing, Yandex) alongside Google.

### AEO (Answer Engine Optimization)

HowTo and FAQPage schemas are the primary AEO signals. These allow Google SGE, Perplexity, and voice assistants to surface direct answers from the site without requiring a click. The `speakable: true` meta tag is also set.

### Semantic HTML

- `<main>` landmark wraps all site content
- `<section>` with `aria-labelledby` on every content block
- `<article>` on every policy section
- `<nav>` with `aria-label` on header and footer navigation
- `role="list"` on custom list elements
- `aria-expanded` on FAQ accordion triggers
- `itemscope` and `itemtype` on hero section

---

## Responsive Breakpoints

| Breakpoint | Behavior |
|---|---|
| `< 640px` | Mobile — bottom sheet, 1-col layouts, compact spacing |
| `≥ 640px` | Sheet becomes centered modal |
| `≥ 700px` | Bento grid goes 2-col, testimonials auto-fill |
| `≥ 900px` | Hero content left-aligned, sections get wider padding |
| `≥ 1280px` | Section padding increases for large screens |
| Max content width | 1080px on main site, 760px on privacy policy |

---

## Accessibility

- All interactive elements have `aria-label` or visible label text
- FAQ keyboard navigation: Enter and Space both trigger toggle
- Sheet closes on Escape key
- `prefers-reduced-motion` is respected by CSS transition defaults
- Color contrast targets WCAG AA on all primary text
- Images have descriptive `alt` text
- Form has `novalidate` with custom validation messages via `aria-live="polite"`

---

## Things To Do

These are not done yet. Do these before considering the site production-ready.

### Rename the privacy policy file

The file is currently `Privacy Policy.html` (space in filename). Rename it:

```
Privacy Policy.html  →  privacy-policy.html
```

Then update the link in `index.html` footer:

```html
<!-- Change this -->
<a href="Privacy Policy.html">Privacy Policy</a>

<!-- To this -->
<a href="privacy-policy.html">Privacy Policy</a>
```

### Create the social card image

`assets/social-card.png` must exist at exactly **1200 × 630 pixels**. Every WhatsApp share, Instagram DM link, LinkedIn post, and Twitter card uses this image. A dark background with the gradient headline and your tagline works well.

### Update Twitter handle

Both `index.html` and `privacy-policy.html` have:

```html
<meta name="twitter:site" content="@sayitforyoufun">
<meta name="twitter:creator" content="@sayitforyoufun">
```

Replace `@sayitforyoufun` with your actual handle if different. Remove both tags if you have no Twitter presence.

### Submit to Search Console

After pushing both files live:

1. Open [Google Search Console](https://search.google.com/search-console)
2. Use the URL Inspection tool on `https://www.sayitforyou.fun/`
3. Use the URL Inspection tool on `https://www.sayitforyou.fun/privacy-policy.html`
4. Request indexing for both

### Create and submit a sitemap

Create `sitemap.xml` in your root directory:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://www.sayitforyou.fun/</loc>
    <lastmod>2026-01-01</lastmod>
    <changefreq>monthly</changefreq>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://www.sayitforyou.fun/privacy-policy.html</loc>
    <lastmod>2026-01-01</lastmod>
    <changefreq>yearly</changefreq>
    <priority>0.3</priority>
  </url>
</urlset>
```

Then create `robots.txt`:

```
User-agent: *
Allow: /
Disallow: /assets/

Sitemap: https://www.sayitforyou.fun/sitemap.xml
```

Submit the sitemap URL in Search Console under Sitemaps.

### Remove `ayushi.html` from the repository

If this file is still in your public repo or on the server, remove it. It is a privacy risk.

### Post the first five real deliveries

The site has testimonials and stats but no public proof of delivery yet. Post five real delivered messages on Instagram before running any promotion. This is the single highest-impact action for trust and conversion.

### Add a confirmation email or DM

When someone submits the form, they get a success message but no follow-up. An automated Instagram DM or email confirmation builds trust and reduces "did it work?" uncertainty.

---

## Privacy Policy Page

Separate file: `privacy-policy.html`

Matches the main site design exactly. Dark background, same gradient system, Inter font, Font Awesome icons. All policy sections are in glass-style cards with scroll reveal animations.

Sections covered:
1. Our Commitment to Your Privacy
2. Information We Collect
3. How We Use Your Information
4. Who We Share Your Information With
5. How We Protect Your Information
6. Your Rights and Choices
7. Children's Privacy (under 13)
8. Changes to This Policy
9. Contact Us

Effective date: July 20, 2025.

---

## License

This project is private. All rights reserved. Do not reuse, copy, or redistribute without permission.

---

*SayItForYou — Say what you couldn't say.*
