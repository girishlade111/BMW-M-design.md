# BMW M Website — Complete Project Context for AI Assistants

> **Purpose:** This document is a single comprehensive context file that explains the entire BMW M website project — its architecture, design system, code logic, component mapping, and implementation details. Feed this file to any AI tool to give it full context for making changes, improvements, or debugging.

---

## 1. Project Overview

```
Project:   BMW M — The Ultimate Driving Machine
Type:      Single-page static brand/marketing website
Domain:    High-performance automotive (BMW M division)
File:      index.html (~33 KB, 608 lines)
Design:    Based on DESIGN.md — a YAML design token specification
Stack:     Vanilla HTML5 + CSS3 + JavaScript (zero dependencies, no build step)
```

### 1.1 What This Website Does

A single HTML file that renders a full BMW M brand landing page. It is a **static marketing surface** — no backend, no database, no framework. The page visually demonstrates the BMW M design system with:

- Full-bleed hero section with automotive photography overlay
- Product showcase grid (M3, M4, M5)
- Editorial magazine section with category filtering tabs
- Technical specification data display
- Call-to-action band with dealer finder
- Multi-column footer with navigation links
- Fixed-position utility widgets (cookie consent, chatbot launcher)

### 1.2 Design Philosophy (from DESIGN.md)

The system is a **near-black canvas** (`#000`) with white BMW Type Next Latin headlines in **confident UPPERCASE**. Brand energy comes from **full-bleed automotive photography** — cars cornering at speed, carbon-fiber details, cockpit shots. UI chrome recedes to minimal labels.

**Key brand rules:**
- The **M tricolor stripe** (light blue → dark blue → red) is brand-identity only — never a button or background fill
- **Zero border radius** (0px) on all buttons, cards, inputs. Only icon buttons get `rounded.full`
- **Typography contrast**: heavy display (700 weight) vs light body (300 weight) — never blur this contrast
- **Spacing**: `section` (96px) between major bands, `xxl` (64px) inside hero bands, `lg` (24px) inside cards
- **No drop shadows** — depth comes from photography, not chrome

---

## 2. File Structure (5 files)

```
BMW-M-design.md/
├── DESIGN.md            # Full design system specification (503 lines)
├── index.html           # The website itself (608 lines, all HTML+CSS+JS)
├── CONTEXT.md           # This file — AI context document
├── robots.txt           # Crawler permissions (8 lines)
├── sitemap.xml          # XML sitemap for SEO (121 lines, 17 URLs)
└── README.md            # Standard project documentation (215 lines)
```

---

## 3. index.html — Complete Code Architecture

### 3.1 Head Section (lines 1–309)

#### Meta Tags Layer (lines 4–39)

| Lines | Tag | Purpose |
|-------|-----|---------|
| 4-5 | `charset`, `viewport` | Encoding + responsive viewport |
| 8 | `<title>` | 60-char title: "BMW M — The Ultimate Driving Machine \| High-Performance Sports Cars & SUVs" |
| 9 | `meta description` | 160-char description with keywords M3, M4, M5, M xDrive, 617 hp |
| 10 | `meta keywords` | 14 comma-separated keywords |
| 11 | `meta author` | "BMW M" |
| 12-13 | `meta robots` + `googlebot` | "index, follow, max-image-preview:large, max-snippet:-1, max-video-preview:-1" |
| 14 | `meta rating` | "general" |
| 15 | `meta theme-color` | `#000000` — matches black canvas |
| 16 | `meta application-name` | "BMW M" |
| 18 | `link canonical` | `https://bmwm.example.com/` |

**Open Graph (lines 21–30):**
- `og:type` = "website", `og:url`, `og:site_name`, `og:title`, `og:description`
- `og:image` = Unsplash BMW photo at 1200×630px
- `og:locale` = "en_US"

**Twitter Card (lines 33–39):**
- `twitter:card` = "summary_large_image"
- `twitter:site` + `twitter:creator` = "@BMW"

#### JSON-LD Structured Data (lines 42–95)

Single `<script type="application/ld+json">` block containing:

```
Schema.org/WebSite
  ├── name: "BMW M"
  ├── url, description, inLanguage
  ├── publisher: Schema.org/Organization
  │     ├── name, url, logo (ImageObject)
  │     └── sameAs: [Facebook, Instagram, YouTube URLs]
  └── mainEntity: Schema.org/ItemList
        └── itemListElement: [3× Schema.org/Product]
              ├── Product 1: BMW M3 Sedan (503 hp, 0-100 in 3.8s)
              ├── Product 2: BMW M4 Coupe (503 hp, 0-100 in 3.7s)
              └── Product 3: BMW M5 Competition (617 hp, 0-100 in 3.2s)
```

Each `Product` has: `position`, `name`, `description` (with specs), `url`, `brand` (Brand: "BMW M").

#### Font Preconnects (lines 97–99)

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;700&family=Saira+Condensed:wght@700&display=swap" rel="stylesheet">
```

- **Inter** (300/400/700) — primary font, open-source substitute for BMW Type Next Latin
- **Saira Condensed** (700) — alternate display font for headlines (condensed feel)

### 3.2 CSS Stylesheet (lines 100–309)

Inline `<style>` block, ~210 lines. No external CSS files.

#### Global Reset (lines 101–111)

```css
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
html { font-size: 16px; -webkit-font-smoothing: antialiased; }
body { font-family: 'Inter', ...; background-color: #000; color: #fff; overflow-x: hidden; }
img { display: block; max-width: 100%; height: auto; }
a { text-decoration: none; color: inherit; }
ul { list-style: none; }
```

#### Utility Classes (lines 113–114)

```css
.container { max-width: 1440px; margin: 0 auto; padding: 0 24px; }
.full-bleed { width: 100%; }
```

#### Component Styles Mapping

| CSS Selector | Lines | Component Type | Design Token Equiv |
|---|---|---|---|
| `.top-nav` | 117-137 | Fixed navigation bar | `component.top-nav` |
| `.hero-photo-band` | 140-158 | Full-screen hero | `component.hero-photo-band` |
| `.btn-primary` | 161-167 | Primary CTA button | `component.button-primary` |
| `.btn-primary-outline` | 168-174 | Outline button | `component.button-primary-outline` |
| `.m-stripe-divider` | 177-181 | M tricolor stripe | `component.m-stripe-divider` |
| `.section` / `.section-dark` / `.section-card-bg` | 183-186 | Section containers | spacing tokens |
| `.section-header` | 188-190 | Section title + label | typography tokens |
| `.model-grid` / `.model-card` | 192-201 | 3-up model cards | `component.model-card` |
| `.feature-grid` / `.feature-card` | 203-210 | 3-up magazine cards | `component.feature-photo-card` |
| `.spec-grid` / `.spec-cell` | 212-216 | 4-up spec table | `component.spec-cell` |
| `.category-tabs` / `.category-tab` | 218-222 | Filter tabs | `component.category-tab` |
| `.cta-band-photo` | 224-232 | Pre-footer CTA | `component.cta-band-photo` |
| `.footer` / `.footer-grid` | 234-243 | Page footer | `component.footer` |
| `.cookie-consent` | 245-255 | Cookie banner | `component.cookie-consent-card` |
| `.chatbot-launcher` | 257-265 | Chatbot widget | `component.chatbot-launcher` |
| `.text-link` | 267-270 | Inline uppercase link | `component.text-link` |
| `.mobile-nav` | 299-308 | Full-screen mobile menu | responsive variant |

#### Responsive Breakpoints (lines 272–297)

Three media queries:

| Width | Key Changes |
|-------|-------------|
| `max-width: 1024px` | Grids 3→2 columns (model, feature, spec) |
| `max-width: 768px` | Nav → hamburger, h1 80→48px, grids 2→1, footer 4→2 cols, spacing halved |
| `max-width: 480px` | Footer 2→1 column |

Specific mobile behaviors at 768px:
- `.nav-links` hidden (`display: none`)
- `.hamburger` shown (`display: flex`)
- Right nav icons hidden (except hamburger)
- `.hero-content h1` shrinks to 48px
- `.section` padding 96→48px
- `.cookie-consent` expands full-width (left+right=16px)
- `.chatbot-launcher` repositions (right:16px, bottom:80px)
- `.category-tabs` gains horizontal scroll (`overflow-x: auto`)

### 3.3 HTML Body Structure (lines 311–607)

#### Skip Link (line 313)

```html
<a href="#main-content" class="skip-link" style="position:absolute;left:-9999px;...">Skip to main content</a>
```

Accessibility feature — hidden off-screen, focusable via Tab key. When focused, becomes visible.

#### Mobile Navigation Overlay (lines 316–324)

```html
<div class="mobile-nav" id="mobileNav" role="dialog" aria-modal="true" aria-label="Mobile navigation menu">
  <div class="m-stripe-divider" aria-hidden="true">...</div>
  <button class="close-btn" onclick="toggleNav()" aria-label="Close navigation menu">✕</button>
  <a href="#" onclick="toggleNav()">Models</a>
  <a href="#" onclick="toggleNav()">Topics</a>
  <a href="#" onclick="toggleNav()">Magazine</a>
  <a href="#" onclick="toggleNav()">Configurator</a>
  <a href="#" onclick="toggleNav()">Fastlane</a>
</div>
```

- Hidden by default (`display: none`)
- Shown via JS toggle (`.open` class → `display: flex`)
- Full-screen black overlay with centered uppercase links (40px, 700 weight)
- M tricolor stripe pinned to top
- Close button top-right
- All nav links call `toggleNav()` to close on selection

#### Top Navigation (lines 327–348)

```html
<nav class="top-nav" aria-label="Main navigation">
  <div class="container">
    <a href="/" class="nav-logo" aria-label="BMW M home">
      <div class="m-stripe-logo" aria-hidden="true"><span></span><span></span><span></span></div>
      <div class="bmw-roundel" aria-hidden="true"></div>
      <span class="m-wordmark">M</span>
    </a>
    <div class="nav-links" role="menubar">
      <a href="#" role="menuitem">Models</a>
      ...
    </div>
    <div class="nav-right">
      <button title="Language" aria-label="Select language">🌐</button>
      <button title="Search" aria-label="Search BMW M">🔍</button>
      <button title="Account" aria-label="My account">👤</button>
      <button class="hamburger" onclick="toggleNav()" aria-label="Open navigation menu" aria-expanded="false">☰</button>
    </div>
  </div>
</nav>
```

- Fixed at top (64px height), border-bottom 1px `#3c3c3c`
- Logo cluster: M tricolor stripes (4px each) + CSS-drawn BMW roundel (radial gradient) + "M" wordmark
- Menu items in `nav-link` typography (14px, 400 weight, 0.5px tracking)
- Right cluster: 3 icon buttons (48×48px) + hamburger (hidden on desktop)
- Hamburger `aria-expanded` toggled via JS

#### Main Content (lines 351–497)

Wrapped in `<main id="main-content">`. Contains 5 sections:

**Section 1: Hero Photo Band (lines 352–365)**
```html
<section class="hero-photo-band" aria-label="Hero: BMW M The Ultimate Driving Machine">
  <img class="hero-bg" src="..." alt="..." fetchpriority="high">
  <div class="hero-overlay">
    <div class="hero-content">
      <p class="eyebrow">The M Brand</p>
      <h1>The Ultimate<br>Driving Machine</h1>
      <p class="subtitle">Where motorsport engineering meets the open road...</p>
      <div class="btn-group">
        <a href="#" class="btn-primary">Explore Models</a>
        <a href="#" class="btn-primary-outline">Build Your M</a>
      </div>
    </div>
  </div>
</section>
```

- Full-bleed background image (absolute positioned, `object-fit: cover`)
- `fetchpriority="high"` on hero image (LCP optimization)
- Gradient overlay from transparent → black at bottom
- `display-xl` headline (80px, 700 weight, UPPERCASE) via Saira Condensed
- Subtitle in `body-md` (16px, 300 weight, `#bbb`)
- Two CTAs: primary (filled on hover) + outline

**Section 2: Model Grid (lines 370–407)**
```html
<section class="section section-dark" aria-label="BMW M model lineup">
  ...
  <div class="model-grid">
    <article class="model-card" itemscope itemtype="https://schema.org/Product">
      <img class="model-img" src="..." alt="..." loading="lazy" itemprop="image">
      <div class="model-info">
        <h3 itemprop="name">M3 Sedan</h3>
        <meta itemprop="brand" content="BMW M">
        <p class="specs" itemprop="description">503 hp · 0–100 in 3.8s · 6‑MT / 8‑AT</p>
        <a href="#" class="text-link" aria-label="Explore BMW M3 Sedan details">Explore This Model</a>
      </div>
    </article>
    <!-- M4 Coupe, M5 Competition — same structure -->
  </div>
</section>
```

- 3 cards in CSS Grid (3 columns, 24px gap)
- Each card is `<article>` with `itemscope itemtype="https://schema.org/Product"`
- Image: 16:10 aspect ratio via `aspect-ratio: 16/10`, `object-fit: cover`
- Model name in `display-md` (40px, 700 weight, UPPERCASE)
- Specs in `body-sm` (14px, 300 weight)
- "Explore This Model" link in `text-link` style (14px, 700, 1.5px tracking, → arrow via `::after`)

**Section 3: Magazine Grid (lines 412–453)**
```html
<section class="section section-dark" aria-label="BMW M Magazine editorial articles">
  ...
  <div class="category-tabs" role="tablist" aria-label="Filter magazine articles by category">
    <button class="category-tab active" role="tab" aria-selected="true">All</button>
    <button class="category-tab" role="tab" aria-selected="false">Magazine</button>
    ...
  </div>
  <div class="feature-grid">
    <article class="feature-card">
      <img class="feature-img" src="..." loading="lazy">
      <div class="feature-body">
        <p class="category-tag">Motorsport</p>
        <h3>Inside the M4 GT3: Engineering for Victory</h3>
        <p>From the Nürburgring to Daytona...</p>
      </div>
    </article>
    <!-- 2 more articles -->
  </div>
</section>
```

- Category tabs: 5 tabs (All, Magazine, Models, Lifestyle, Motorsport)
  - `role="tablist"` on container, `role="tab"` + `aria-selected` on each button
  - Active tab: white text + 2px white bottom border
  - Inactive tabs: `#bbb` text, no border
  - JS handles click → class toggle + `aria-selected` update
- Feature cards: `surface-card` background (`#1a1a1a`), 16:9 images, category tag, h3, body excerpt

**Section 4: Spec Grid (lines 458–484)**
```html
<section class="section section-card-bg" aria-label="BMW M performance technical specifications">
  ...
  <div class="spec-grid">
    <div class="spec-cell">
      <p class="spec-value">3.2s</p>
      <p class="spec-label">0–100 km/h</p>
    </div>
    <!-- 3 more cells: 617 hp, 305 km/h, 553 lb·ft -->
  </div>
</section>
```

- 4 cells in CSS Grid (4 columns, 24px gap)
- `surface-soft` background (`#0d0d0d`)
- Value in `display-sm` (32px, 700 weight, Saira Condensed)
- Label in `label-uppercase` (14px, 700, 1.5px tracking, `#bbb`)

**Section 5: CTA Band (lines 489–496)**
```html
<section class="cta-band-photo" aria-label="Call to action: schedule a BMW M test drive">
  <img class="cta-bg" src="..." alt="..." loading="lazy">
  <div class="cta-overlay">
    <h2>Experience the M Difference.<br>Schedule Your Test Drive.</h2>
    <a href="#" class="btn-primary-outline" aria-label="Find a BMW M dealer near you">Find a Dealer</a>
  </div>
</section>
```

- Full-bleed background photo, centered content
- `display-md` headline (40px, 700 weight, UPPERCASE)
- Single outline CTA button centered below

#### Footer (lines 499–558)

```html
<footer class="footer" aria-label="Site footer">
  <div class="container">
    <div class="footer-grid">
      <div class="footer-col">
        <h4>BMW M Models</h4>
        <ul>
          <li><a href="#">M3 Sedan</a></li>
          <!-- 8 model links -->
        </ul>
      </div>
      <div class="footer-col"><h4>BMW M Lifestyle</h4>...</div>
      <div class="footer-col"><h4>Owners</h4>...</div>
      <div class="footer-col"><h4>Company</h4>...</div>
    </div>
    <div class="footer-bottom">
      <p class="disclaimer">© 2026 BMW AG...</p>
      <select class="lang-select" aria-label="Language selector">
        <option>English</option>
        <option>Deutsch</option>
        ...
      </select>
    </div>
  </div>
</footer>
```

- 4-column CSS Grid (collapses to 2 → 1 at breakpoints)
- Column headers in `label-uppercase` (white)
- Link text in `body-sm` (14px, 300 weight, `#7e7e7e` / muted)
- Bottom row: disclaimer (12px caption) + language dropdown
- 1px `hairline` border-top and separator between grid and bottom

#### Utility Widgets (lines 560–574)

**Cookie Consent (lines 561–567):**
```html
<div class="cookie-consent" id="cookieConsent" role="dialog" aria-label="Cookie consent notice" aria-modal="false">
  <p>BMW M uses cookies...</p>
  <div class="btn-group">
    <button class="btn-primary" onclick="acceptCookies()">Accept Cookies</button>
    <button class="text-link" onclick="acceptCookies()">Cookie Settings</button>
  </div>
</div>
```
- Fixed bottom-right, 360px max-width
- Dismissed via JS `acceptCookies()` → sets `display: none`
- On mobile: expands full-width (left/right 16px)

**Chatbot Launcher (lines 570–574):**
```html
<div class="chatbot-launcher" id="chatbotLauncher" role="button" tabindex="0" aria-label="Open BMW M chatbot">
  <h3>BMW M Chatbot</h3>
  <p>Have questions...</p>
  <button class="btn-primary" style="width:100%;">Launch Chat</button>
</div>
```
- Fixed right side, `surface-card` background
- `role="button" + tabindex="0"` makes it keyboard-focusable
- Hover: opacity 0.9

### 3.4 JavaScript (lines 576–606)

Three functions + one event listener:

**`toggleNav()` (lines 577–582):**
```js
function toggleNav() {
  const nav = document.getElementById('mobileNav');
  const hamburger = document.querySelector('.hamburger');
  const isOpen = nav.classList.toggle('open');
  hamburger.setAttribute('aria-expanded', isOpen);
}
```
- Toggles `.open` class on `#mobileNav` (shows/hides overlay)
- Syncs `aria-expanded` on hamburger button for accessibility

**`acceptCookies()` (lines 583–585):**
```js
function acceptCookies() {
  document.getElementById('cookieConsent').style.display = 'none';
}
```
- Simply hides the cookie consent dialog

**Category Tab Handler (lines 587–596):**
```js
document.querySelectorAll('.category-tab').forEach(tab => {
  tab.addEventListener('click', function() {
    document.querySelectorAll('.category-tab').forEach(t => {
      t.classList.remove('active');
      t.setAttribute('aria-selected', 'false');
    });
    this.classList.add('active');
    this.setAttribute('aria-selected', 'true');
  });
});
```
- Removes `.active` + `aria-selected="false"` from all tabs
- Adds `.active` + `aria-selected="true"` to clicked tab
- Note: This is visual-only — does not filter article cards (no actual data filtering)

**Escape Key Handler (lines 598–605):**
```js
document.addEventListener('keydown', function(e) {
  if (e.key === 'Escape') {
    const mobileNav = document.getElementById('mobileNav');
    if (mobileNav.classList.contains('open')) {
      toggleNav();
    }
  }
});
```
- Closes mobile nav when Escape pressed

---

## 4. Design Token to CSS Mapping

### 4.1 Color Hex Values

| Token | Hex | CSS Usage |
|-------|-----|-----------|
| `canvas` | `#000000` | `body background`, `.top-nav`, `.hero-photo-band`, `.section-dark` |
| `surface-card` | `#1a1a1a` | `.feature-card`, `.chatbot-launcher` |
| `surface-soft` | `#0d0d0d` | `.spec-cell`, `.section-card-bg` |
| `on-dark` | `#ffffff` | All text color (white) |
| `body` | `#bbbbbb` | `.subtitle`, `.specs`, `p`, `.category-tag`, inactive tabs |
| `muted` | `#7e7e7e` | Footer links, `.disclaimer` |
| `hairline` | `#3c3c3c` | Borders, dividers |
| `m-blue-light` | `#0066b1` | M stripe span 1 |
| `m-blue-dark` | `#1c69d4` | M stripe span 2, BMW roundel |
| `m-red` | `#e22718` | M stripe span 3 |

### 4.2 Typography Implementation

Because BMW Type Next Latin is a licensed font, the implementation uses two Google Fonts substitutes:

| Design Token | CSS Font | CSS Size | Weight | Letter-Spacing |
|---|---|---|---|---|
| `display-xl` (80px) | Saira Condensed | 80px | 700 | -0.5px |
| `display-lg` (56px) | Saira Condensed | 56px | 700 | -0.5px |
| `display-md` (40px) | Saira Condensed | 40px | 700 | -0.5px |
| `display-sm` (32px) | Saira Condensed | 32px | 700 | -0.5px |
| `title-lg` (24px) | Inter | 24px | 700 | 0 |
| `label-uppercase` (14px) | Inter | 14px | 700 | 1.5px |
| `body-md` (16px) | Inter | 16px | 300 | 0 |
| `body-sm` (14px) | Inter | 14px | 300 | 0 |
| `button` (14px) | Inter | 14px | 700 | 1.5px |
| `nav-link` (14px) | Inter | 14px | 400 | 0.5px |
| `caption` (12px) | Inter | 12px | 400 | 0.5px |

### 4.3 Spacing Implementation

| Token | Value | Used In |
|-------|-------|---------|
| `section` | 96px | `.section` padding-top/bottom |
| `xxl` | 64px | `.hero-overlay` padding |
| `xl` | 40px | `.section-header` margin-bottom |
| `lg` | 24px | Grid gaps, card padding, `.container` padding |
| `md` | 16px | Button group gap, footer bottom padding |
| `sm` | 12px | Category tab padding |

---

## 5. Responsive Behavior Detail

### 5.1 Grid Collapse Chain

```
Desktop (1024px+)     Tablet (768-1024px)    Mobile (<768px)
──────────────────────────────────────────────────────────
.model-grid:  3 cols  →  2 cols              →  1 col
.feature-grid: 3 cols →  2 cols              →  1 col
.spec-grid:   4 cols  →  2 cols              →  1 col
.footer-grid: 4 cols  →  2 cols              →  1 col (<480px)
```

### 5.2 Navigation Collapse

| State | Desktop | Mobile |
|-------|---------|--------|
| Menu links | Horizontal row, visible | Hidden |
| Hamburger | Hidden | Visible |
| Right icons | 3 visible (language, search, account) | Hidden |
| Mobile overlay | Never shown | Full-screen on hamburger click |
| `aria-expanded` | N/A | Tracks open/closed state |

### 5.3 Typography Scaling

| Element | Desktop | Mobile (<768px) |
|---------|---------|-----------------|
| Hero h1 | 80px | 48px |
| Section h2 | 56px | 36px |
| CTA h2 | 40px | 32px |
| Subtitle | 16px | 14px |

### 5.4 Spacing Scaling

| Element | Desktop | Mobile (<768px) |
|---------|---------|-----------------|
| Section padding | 96px vertical | 48px vertical |
| Cookie consent | 360px max, right:24px | full-width, right/left:16px |
| Chatbot launcher | right:24px, bottom:100px | right:16px, bottom:80px |

---

## 6. SEO Implementation Summary

### 6.1 Meta Tags — 4 Categories

| Category | Count | Lines |
|----------|-------|-------|
| Primary (short form) | 10 tags | 8-18 |
| Open Graph (long form) | 8 properties | 21-30 |
| Twitter Card | 6 tags | 33-39 |
| Structured Data | 1 script (4 entities) | 42-95 |

### 6.2 robots.txt (8 lines)

```
User-agent: *
Allow: /
Sitemap: https://bmwm.example.com/sitemap.xml
```

### 6.3 sitemap.xml (121 lines, 17 URLs)

URL priority distribution:
- `1.0`: Homepage
- `0.9`: Models listing page
- `0.8`: Individual models (M3, M4, M5), Configurator
- `0.7`: X3/X4/X5/X6 M, Magazine, Motorsport
- `0.6`: Magazine articles, Lifestyle

All URLs use `weekly` or `monthly` changefreq.

### 6.4 Accessibility Features

- Skip navigation link (line 313)
- ARIA roles: `banner`, `navigation`, `main`, `menubar`, `menuitem`, `tablist`, `tab`, `dialog`, `button`
- ARIA attributes: `aria-label`, `aria-modal`, `aria-hidden`, `aria-expanded`, `aria-selected`
- `alt` text on all images (descriptive, 10-15 words)
- `fetchpriority="high"` on hero image (LCP)
- `loading="lazy"` on all other images
- Keyboard: Escape closes mobile nav, tabs are keyboard-focusable
- Touch targets: All buttons/links at least 48×48px

---

## 7. Data Flow Diagram

```
index.html
│
├── <head>
│   ├── Meta tags → Search engines / Social media crawlers
│   ├── JSON-LD → Google Rich Results / Knowledge Graph
│   ├── Font preconnects → Google Fonts CDN
│   └── CSS styles → Browser rendering engine
│
├── <body>
│   ├── Skip link → Keyboard accessibility
│   ├── Mobile nav overlay ← JS toggleNav()
│   ├── Top nav (fixed) → Visual navigation
│   ├── <main>
│   │   ├── Hero section ← Unsplash CDN image (fetchpriority=high)
│   │   ├── M stripe divider (CSS-only, 3 colored spans)
│   │   ├── Model grid ← 3× Unsplash images (lazy)
│   │   │   └── JSON-LD itemprop microdata
│   │   ├── M stripe divider
│   │   ├── Magazine grid ← 3× Unsplash images (lazy)
│   │   │   └── Category tabs ← JS click handler (visual-only)
│   │   ├── M stripe divider
│   │   ├── Spec grid (static data)
│   │   ├── M stripe divider
│   │   └── CTA band ← Unsplash image (lazy)
│   ├── Footer (4-column static link list)
│   ├── Cookie consent ← JS acceptCookies() → hide
│   └── Chatbot launcher (static placeholder)
│
└── <script>
    ├── toggleNav() → mobile nav + aria-expanded
    ├── acceptCookies() → hide cookie consent
    ├── Category tab click → visual toggle + aria-selected
    └── Escape key → close mobile nav
```

**External Resources:**
1. Google Fonts API (Inter + Saira Condensed)
2. Unsplash CDN (5 automotive photos)

**No runtime dependencies, no frameworks, no build step.**

---

## 8. Known Gaps & Improvement Opportunities

### 8.1 Functional Gaps

| Gap | Location | Description |
|-----|----------|-------------|
| Category tabs do not filter | Lines 419-425, 587-596 | Tabs toggle visually but articles stay static. Needs JS filtering logic |
| All links are `#` | Multiple | No actual page routing — all links are placeholders |
| Chatbot is static | Lines 569-574 | No actual chat functionality — just a visual card |
| No carousel | DESIGN.md mentions | Photo carousel arrows are styled but no carousel is implemented |
| No form validation | Not implemented | `text-input` is styled but no form exists on the page |
| No dark/light mode | Per design | Intentional — design spec says no light mode |
| Language selector is decorative | Footer | Dropdown exists but has no JS to switch language |
| No analytics | Not implemented | No Google Tag Manager, GA4, or other analytics scripts |
| No cookie consent persistence | Lines 561-567, 583-585 | Cookie dismissal is in-memory only (hides on reload) |
| Hero doesn't cycle | Line 352-365 | Single static image, no image rotation/carousel |

### 8.2 Code Quality Gaps

| Issue | Location | Suggestion |
|-------|----------|------------|
| Inline `style` attribute | Line 313, 573 | Move to CSS classes |
| Emoji icons | Lines 342-345 | Replace with SVG icons for consistency |
| Hardcoded domain | `robots.txt`, `sitemap.xml`, `canonical` | `bmwm.example.com` needs replacement |
| No CSS custom properties | All CSS | Colors/tokens repeated — should use `--var` for maintainability |
| `onclick` in HTML | Multiple | Migrate to `addEventListener` in JS |
| No content security policy | Missing | Add `meta http-equiv="Content-Security-Policy"` |
| No favicon | Missing | Add `<link rel="icon">` |

### 8.3 Performance Optimizations Possible

- **Preload hero image**: Already using `fetchpriority="high"` — could add `<link rel="preload">`
- **CSS minification**: Inline CSS ~5KB uncompressed
- **Image optimization**: Unsplash URLs could use `&auto=format&fit=crop` for WebP
- **Font subsetting**: Inter font includes many weights/characters not used
- **Critical CSS inlining**: Already inline — no additional HTTP request
- **Service worker**: Could add for offline caching

### 8.4 SEO Gaps

- No `hreflang` tags for multi-language support (language selector is UI-only)
- No breadcrumb structured data
- No `FAQPage` or `Article` structured data for magazine content
- No `VideoObject` structured data
- Sitemap URLs are placeholders — no actual pages exist at those paths
- No Google Analytics or Search Console verification meta tag

---

## 9. How to Feed This to an AI for Modifications

### 9.1 Quick Context (for small changes)

Share the entire `CONTEXT.md` file. Include specific instructions:

```
I have a BMW M website at /path/to/index.html (608 lines).
Context file: /path/to/CONTEXT.md

Please [make change X].
Key files to modify:
- index.html (lines for relevant sections)
- DESIGN.md (if changing design tokens)
- sitemap.xml, robots.txt (if changing URLs)
```

### 9.2 Change Patterns by Component

| Change Type | Files to Modify | Lines to Reference |
|---|---|---|
| Change hero headline | index.html | 357 |
| Add a new model card | index.html | 377-404 (clone `<article>` block) |
| Add new color | DESIGN.md + index.html | DESIGN.md:6-27, index.html:127-129 |
| Change responsive breakpoint | index.html | 272-297 |
| Add analytics script | index.html | before `</head>` (line 99) |
| Make tabs actually filter | index.html | 419-451 (HTML) + 587-596 (JS) |
| Add new page/routing | index.html + new `.html` files | Full hyperlink updates |
| Replace images | index.html | 353, 379, 388, 397, 428, 436, 444, 491 |

### 9.3 Best Practices from DESIGN.md

1. New components default to `border-radius: 0`. Only use `rounded.full` for circular icon buttons
2. Display headlines stay UPPERCASE 700; body stays sentence-case 300. Never blur the contrast
3. The M tricolor is brand-identity-only — never extend it to buttons or background fills
4. Use `section` spacing (96px) between major editorial bands for vertical rhythm
5. When in doubt about emphasis: bigger photography before bigger type

---

## 10. Quick Reference — Line Number Map

| Component | HTML Lines | CSS Lines | JS Lines |
|-----------|-----------|-----------|----------|
| HTML head / meta | 1-99 | — | — |
| CSS styles | — | 100-309 | — |
| Skip link | 313 | — | — |
| Mobile nav | 316-324 | 299-308 | 577-582, 598-605 |
| Top nav | 327-348 | 117-137 | — |
| Hero band | 352-365 | 140-158 | — |
| M stripe divider | 368, 410, 455, 486-487 | 177-181 | — |
| Model grid | 370-407 | 192-201 | — |
| Magazine grid | 412-453 | 203-210, 218-222 | 587-596 |
| Spec grid | 458-484 | 212-216 | — |
| CTA band | 489-496 | 224-232 | — |
| Footer | 499-558 | 234-243 | — |
| Cookie consent | 561-567 | 245-255 | 583-585 |
| Chatbot launcher | 569-574 | 257-265 | — |
| JavaScript | — | — | 576-606 |

---

## 11. DESIGN.md — Design Specification Companion

The `DESIGN.md` file (503 lines) is a YAML-based design specification. Key sections:

| Section | Lines | Content |
|---------|-------|---------|
| Frontmatter YAML | 1-243 | Colors (27 tokens), Typography (13 scales), Spacing (8 tokens), Components (21 specs) |
| Overview | 245-260 | Brand philosophy, key characteristics |
| Colors | 262-290 | Brand/accent, surface, hairlines, text, semantic |
| Typography | 292-327 | Font family (BMW Type Next Latin), hierarchy table, principles, font substitutes (Inter) |
| Layout | 329-346 | Spacing system, grid, container (1440px max), whitespace philosophy |
| Elevation & Depth | 348-362 | Flat, hairline, card surface, photographic depth |
| Shapes | 364-379 | Border radius scale (none → full), photography geometry |
| Components | 381-433 | Detailed spec for all 21 components |
| Do's and Don'ts | 435-453 | Brand rules |
| Responsive | 455-482 | Breakpoints, touch targets, collapsing strategy |
| Iteration Guide | 484-493 | Workflow rules |
| Known Gaps | 495-503 | Limitations of the design analysis |

---

## 12. Environment & Build

- **Zero build step** — open `index.html` directly in a browser
- **No package.json** — no npm/pip/bundler needed
- **Served via**: file:// protocol or any static HTTP server
- **Local server**: `npx serve .` or `python -m http.server`
- **Git**: hosted at `https://github.com/girishlade111/BMW-M-design.md`
- **CI/CD**: none configured (static site — drag-drop to Netlify/Vercel)
- **Browser support**: Modern browsers (Chrome, Firefox, Safari, Edge) — CSS Grid + `aspect-ratio` require 2020+ browsers
