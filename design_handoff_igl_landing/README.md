# Handoff: IGL Potable Spirits — Investor-Grade Landing Page

## Overview
A single-page, investor-facing marketing site for **India Glycols Limited (IGL) — Potable Spirits Division**. It tells the division's premium-spirits story through a sequence of scroll-driven sections: a video-carousel hero, a "strategic foundations" split, an investment snapshot, a scroll-choreographed product range, an interactive product portfolio, market opportunity, sustainability, leadership, a roadmap timeline, and an investor CTA + footer. Tagline: **"Where smooth meets sophistication."**

## About the Design Files
The files in this bundle are **design references created in HTML** — a working prototype showing the intended look, motion, and behavior. They are **not production code to copy directly**.

The prototype is authored as a "Design Component" (`.dc.html`) that runs on a small bundled runtime (`support.js`) — a bespoke template/logic layer, **not** a standard framework. Do **not** ship `support.js` or the `.dc.html` format. Instead, **recreate these designs in the target codebase's environment** (React, Vue, Astro, plain HTML/CSS, etc.) using its established patterns. If no environment exists yet, a static-site/React stack (e.g. Next.js or Astro) suits this marketing page well.

To preview the prototype as-is, serve the folder over a static server and open `IGL Potable Spirits.dc.html` (it must be at the server root because `support.js` and the persistence sidecar resolve there).

## Fidelity
**High-fidelity (hifi).** Final colors, typography, spacing, imagery, and interactions are all specified. Recreate the UI pixel-faithfully. All scroll/hover/click behaviors described below are intended product behavior.

---

## Design Tokens

### Colors
| Token | Hex | Usage |
|---|---|---|
| Indigo (primary blue) | `#282E75` | Dark section backgrounds, headings on light bg, body text on beige, borders |
| Indigo deep | `#1c2052` | Hero/leadership/footer deepest background, scrim base |
| Beige | `#e4dcce` | Light section backgrounds, light text |
| Cream | `#f3eee4` | Headings on dark backgrounds |
| Oxblood | `#50130f` | Eyebrow labels on light bg, "Explore Our Craft" button, accents |
| CTA brown | `#281309` | Investor CTA section background |
| Brown (warm) | `#482a10` | Reserved palette tone |
| Charcoal | `#2b2727` | Reserved palette tone |
| Near-black | `#1e1e1e` | Portfolio section background |
| Champagne gold | `#b9985f` | Accent rules, numerals, primary buttons, dots, timeline line |
| Gold bright | `#d8b66a` | Leading edge of the animated roadmap line |
| Text on beige | `rgba(40,46,117,*)` | Body copy on light sections (indigo at reduced alpha) |
| Text on dark | `rgba(228,220,206,*)` | Body copy on dark sections (beige at reduced alpha) |

### Typography
- **Headings (H1–H4) & serif display:** `'Fraunces', serif` — Google Fonts, variable (ital, opsz 9–144, wght 300–700). Used at weight 500–600. (Originally specified as "Canela"; Fraunces is the chosen substitute.)
- **Body / UI / labels:** `'Inter', sans-serif` — weights 300/400/500/600.
- Google Fonts import (in `<head>`):
  `https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&family=Fraunces:ital,opsz,wght@0,9..144,300..700;1,9..144,300..700&display=swap`

**Type scale (desktop, px):**
- Hero H1: 84 / line-height 0.98 / letter-spacing -0.01em
- Section H2: 46–62 / 1.02–1.05
- H3 (cards, accordion, milestones): 22–38
- Eyebrow labels: 11 / uppercase / letter-spacing 0.3em
- Body: 14–16 / line-height 1.6–1.8
- Small caption/meta: 10–13

### Spacing & Layout
- Content max-width: **1320px**, horizontally centered.
- Section horizontal padding: **56px**; vertical padding: **120–130px**.
- Standard column gap: 64–80px; card grid gap: 18–36px.
- Border radius: **0** on cards/images (sharp corners). Buttons are sharp rectangles. Nav/carousel arrow buttons are 54px circles.
- Dot indicators: 7–11px circles.

### Shadows
- Bottle drop shadow: `drop-shadow(0 34px 64px rgba(0,0,0,0.6))`.
- Primary button glow (hero): `glowPulse` keyframe pulsing `box-shadow 0 0 26px 2px rgba(185,152,95,0.35)`.
- Timeline bright line: `box-shadow 0 0 12px rgba(185,152,95,0.55)`.
- Active milestone dot: `box-shadow 0 0 0 4px rgba(185,152,95,0.16), 0 0 14px rgba(185,152,95,0.7)`.

---

## Screens / Views
Single continuously-scrolling page. Sections top-to-bottom:

### 1. Hero
- **Purpose:** Brand statement + investor entry point.
- **Layout:** Full-viewport (`100vh`, min 680px). Fixed top nav. Left-anchored copy block vertically centered, max-width 42ch. A product bottle stands at right.
- **Components:**
  - **Nav** (absolute, top): left = "IG" monogram (34px bordered square) + "India Glycols / Potable Spirits" lockup; center = links (Investors, Portfolio, Manufacturing, Sustainability, Governance), 13px beige; right = gold "Investor Relations" button (`#b9985f` bg, `#282E75` text, 11px padding 18px, uppercase, nowrap).
  - **Carousel** (3 slides, crossfade): slide 1 = `assets/hero-1.mp4` (autoplay/muted/loop, object-fit cover); slide 2 = `assets/hero-2.jpg`; slide 3 = `assets/hero-3.jpg`. Each slide cross-fades via opacity over **1.6s ease**; auto-advance every **6.5s** (configurable). Slide dots at bottom-left: active dot is 26px wide cream pill, inactive 7px translucent; clicking a dot jumps and restarts the timer.
  - **Scrim:** two stacked gradients — horizontal `rgba(28,32,82,0.92→0.55)` left-to-right, plus vertical top/bottom darkening — to seat the left copy.
  - **Copy block:** gold eyebrow with 30px rule ("ISL's Zumba Black · Aged Rum"); H1 "Where smooth meets sophistication" (Fraunces 84px cream); 16px body; two buttons — primary gold "Investor Relations" (pulsing glow) + outlined "Explore the Portfolio". All fade-up on load (`fadeUp`, staggered 0–0.36s).
  - **Bottle** (`assets/bottle.png`): see Cross-section element below.

### Cross-section element — the standing bottle
- A single `<img>` (`assets/bottle.png`) positioned **absolute at page level** (not inside the hero), `right:9%; top:22vh; height:94vh; z-index:30; pointer-events:none`, so it **straddles the seam** between the hero and the section below it, sitting on top of both.
- **Scroll behavior:** translates downward at 0.22× scroll and scales up very slightly (`1 + min(scrollY,600)*0.00018`). Implemented via a `requestAnimationFrame`-throttled scroll listener.

### 2. Strategic Foundations
- **Purpose:** Establish operational credibility.
- **Layout:** Full-bleed two-column grid (1fr 1fr), min-height 760px, beige background.
- **Components:** Left = black-and-white master-distiller photo (`assets/craftsman.jpg`, `grayscale(1) contrast(1.05)`) **feathered into the beige** via a horizontal `mask-image: linear-gradient(90deg,#000 42%,transparent 99%)` plus an overlay gradient to `#e4dcce` — no hard edge. Bottom-left caption "Master distiller · grain to glass". Right = oxblood eyebrow, H2 "Strategic foundations of our strength", intro paragraph, then three numbered pillars (01 Backward integration, 02 Grain-to-glass control, 03 Regulatory excellence), each a top-bordered row; two buttons (oxblood "Explore Our Craft", outlined "View Manufacturing").

### 3. Investment Snapshot
- **Purpose:** Headline investment metrics.
- **Layout:** Indigo background, grid 0.85fr / 1.15fr. Left = eyebrow + H2 "Investment snapshot at a glance" + intro + source note. Right = 2×2 metric grid with gold hairline borders.
- **Metrics:** ₹450 Cr (Revenue contribution), 28% (YoY growth), 15+ (States & territories), 3 (Flagship brands). Values in Fraunces 58px gold.

### 4. Product Range (scroll-choreographed)
- **Purpose:** Show one in-market flagship + pipeline, with a hero bottle "settling" into a lineup, then a browsable carousel.
- **Layout:** Beige `<section>` ~230vh tall containing a `position:sticky; top:0; height:100vh` stage. **Important:** the page's outermost wrapper uses `overflow-x: clip` (NOT `hidden`) so `position:sticky` pins to the viewport.
- **Four scroll phases** (progress `p` = how far the sticky section has scrolled, 0→1):
  1. **Hold** (p≈0): bottle stands centered (~46% height) over a faint giant "AGED RUM" wordmark.
  2. **Turn** (p 0.14→0.30): bottle tilts slightly (up to −7°), straightening as it begins to fall.
  3. **Fall** (p 0.26→~0.72): bottle drops **straight down first** (vertical leads), then **slides horizontally** into the center slot (horizontal lags); scales from full to slot size (~0.96× slot height). Wordmark fades out (p 0.16→0.36); heading fades in (p 0.30→0.50); the 5-up category row fades in (p 0.24→0.46).
  4. **Settle:** bottle lands colored in the center slot.
- **Interactive carousel (after settle):** 5 category columns — Premium Whisky, Craft Vodka, **Zumba Black (center, in-market)**, Reserve Whiskey, Small-Batch Gin. The **center position is always the colored/active** bottle (full color, gold top-rule, dark label); the other four are greyed (`grayscale(1)`, opacity 0.4) with muted labels. Left/right **circular arrow buttons** (54px) rotate which category occupies center (labels cycle; wraps around). All transitions 0.5s. (Note: in the prototype all five reuse `bottle.png`; in production use distinct per-product bottle renders.)

### 5. Portfolio (interactive tab/accordion) — "Premium spirits crafted for distinction"
- **Purpose:** Browse three flagship expressions.
- **Layout:** Near-black `#1e1e1e` background. Grid 0.9fr / 1.1fr. Left = sticky image panel (aspect 3/4) cross-fading 3 photos. Right = a single-open **accordion** of 3 items + a 3-step process row.
- **Behavior:** Clicking a product header makes it the active tab — its body (tasting notes, italic positioning line, market line) expands (`max-height 0↔360px`, opacity, 0.55s) while others collapse, and the **left image cross-fades (0.7s)** to that product's photo:
  - Single Reserve Whisky → `assets/prod-whisky.jpg`
  - Amazing Vodka → `assets/prod-vodka.jpg`
  - Soulmate Whiskey → `assets/prod-whiskey.jpg`
- Active row: gold numeral, cream name, `#232020` fill; inactive rows dimmed. Default open = item 1. A small caption over the image shows the active product name. Below: 3 process steps (01 Fermentation & distillation, 02 Maturation & aging, 03 Bottling & assurance) with gold top rules.

### 6. Market Opportunity — "The spirits market is expanding"
- **Layout:** Indigo background, centered intro, grid 1.1fr / 0.9fr. Left = full-width image of a distillery interior (in prototype this is a drag-drop `<image-slot>`; in production use a static `<img>`, aspect 4/3). Right = H3 "The global spirits market exceeds $600 billion annually", paragraph, and two stats: **12%** (Premium segment CAGR, India), **2.8x** (Premiumisation multiple by 2030).

### 7. Sustainability — "Sustainability embedded in our operations"
- **Layout:** Beige background, centered intro, **3 equal cards** (grid 1fr 1fr 1fr, gap 36px).
- **Each card:** tall image (aspect 3/4, **sharp corners**, object-fit cover) above a centered caption = oxblood eyebrow + uppercase Inter statement (max 30ch).
  - Card 1 `assets/esg-1.jpg` — Environmental stewardship
  - Card 2 `assets/esg-2.jpg` — Community engagement
  - Card 3 `assets/esg-3.jpg` — Responsible marketing

### 8. Leadership — "Experienced stewards of long-term value"
- **Layout:** Indigo background. Top grid 1fr/1fr = governance eyebrow + H2 + gold "View Governance Framework" button | paragraph. Below: full-width **looping video banner** (`assets/leadership.mp4`, autoplay/muted/loop, aspect 21/8, object-fit cover).

### 9. Roadmap timeline — "Our path forward spans years of growth"
- **Layout:** Indigo background, grid 0.8fr / 1.2fr. Left = sticky heading/intro. Right = vertical timeline of 4 milestones (2024 Capacity expansion begins, 2025 Export market entry, 2026 Premium portfolio launch, 2027 Sustainability milestone). Each: gold dot, Fraunces year (34px gold), H3 title, body.
- **Scroll behavior (key interaction):** a thin vertical track (`rgba(185,152,95,0.18)`) runs full height; a **bright gold line** (2px, gradient to `#d8b66a`, glow) **grows downward** as you scroll (height = progress × track height, trigger ≈ 55% of viewport). Each milestone **dot lights up** (fills gold + glows + gold border) the moment the bright line's bottom edge passes it. Reference feel: seiter.design project-timeline.

### 10. Investor CTA
- **Layout:** Background `#281309`, centered, max-width 680px. H2 "Connect with our investor relations team", paragraph, two buttons: gold "Contact Investor Relations" + outlined "Download Annual Report".

### 11. Footer
- **Layout:** Deep-indigo `#1c2052`. Grid 1.4fr/1fr/1fr/1fr = brand blurb + 3 link columns (Investors, Company, Contact). Bottom bar: copyright + responsible-consumption / 21+ disclaimer.

---

## Interactions & Behavior (summary)
- **Hero carousel:** auto-advance 6.5s; 1.6s opacity crossfade; clickable dots reset the timer.
- **Standing bottle:** parallax translate (0.22×) + slight scale on scroll; spans hero↔section-2 seam at z-index 30.
- **Product range:** sticky 4-phase scroll choreography (hold→turn→fall→settle); then arrow-driven carousel with colored center.
- **Portfolio:** single-open accordion; clicking swaps the sticky left image with a 0.7s crossfade.
- **Roadmap:** scroll-grown gold line + sequential dot illumination.
- **Section headings:** every H1/H2 (except hero, which uses a load animation, and the range heading, which is scroll-driven) **fades up from below** (translateY 30px → 0, opacity 0→1, 1.2s `cubic-bezier(.2,.7,.2,1)`) when scrolled into view. Implementation is fail-safe: reveals on scroll-position check, an immediate on-load pass, and a 3.5s safety fallback so nothing stays hidden.
- **Buttons:** gold primary buttons; outlined secondary; arrow buttons have a hover state (oxblood border/text + faint oxblood fill).

## State Management
Minimal client state:
- `slide` (0–2): active hero carousel slide; driven by interval + dot clicks.
- `active` (0–4): centered product-range category; changed by prev/next arrows (wraps).
- `tab` (0–2): open portfolio accordion item / visible left image.
- Scroll-derived values (bottle transform, range phase, roadmap line height, dot states, heading reveals) are computed in a throttled scroll handler — **not** React state.
No data fetching; all content is static copy.

## Animations & Transitions (specifics)
- `fadeUp` keyframe: opacity 0→1, translateY(18px)→0. Hero copy staggers 0 / 0.12 / 0.24 / 0.36s; bottle 0.3s.
- `glowPulse` keyframe (4.5s ease-in-out infinite) on hero primary button.
- Carousel crossfade: `transition: opacity 1.6s ease`.
- Accordion: `transition: max-height 0.55s ease, opacity 0.45s ease`; image `opacity 0.7s ease`.
- Range carousel cells: `transition: opacity/filter/color/border 0.5s ease`.
- Heading reveal: `1.2s cubic-bezier(.2,.7,.2,1)`.
- Roadmap dots: `transition: background/box-shadow/border-color 0.4s ease`.

## Responsive behavior
The prototype is designed at desktop width (≈1320px content). For production, define breakpoints: collapse 2-col splits to single column, the 5-up range row and 3-up sustainability grid to fewer columns/stacked, reduce hero H1 to ~48–56px, and consider simplifying the sticky scroll choreography (it assumes tall viewports) to a static lineup on small screens.

## Assets
All in `assets/` (copied from the project; replace with production-resolution originals where noted):
- `hero-1.mp4` — hero carousel slide 1 (distillery/brand video). Also reused as `leadership.mp4`.
- `hero-2.jpg`, `hero-3.jpg` — hero carousel slides 2 & 3 (barley field; riders).
- `bottle.png` — ISL's Zumba Black bottle, transparent PNG (hero standing bottle + range lineup). **Provide distinct renders for the 4 pipeline categories in production.**
- `craftsman.jpg` — master distiller (rendered B&W + edge-masked).
- `prod-whisky.jpg`, `prod-vodka.jpg`, `prod-whiskey.jpg` — portfolio photos (Zumba Black serve; Amazing Vodka; Zumba Lemoni serve).
- `esg-1.jpg`, `esg-2.jpg`, `esg-3.jpg` — sustainability cards (barley in hand; pour; tasting flight).
- `leadership.mp4` — leadership banner loop (currently a copy of `hero-1.mp4` — **swap for the real leadership clip**).
- Market section distillery-interior image: **not yet supplied** — a drop-slot placeholder in the prototype. Provide a real photo.

Fonts: Google Fonts (Inter, Fraunces) — load via the `<link>` above or self-host.

## Files
- `IGL Potable Spirits.dc.html` — the full design prototype (markup + logic). Read this for exact values, copy, and interaction logic.
- `support.js` — prototype runtime only. **Reference, do not ship.**
- `image-slot.js` — drag-drop image placeholder web component used by the Market section in the prototype. **Reference, do not ship** — replace its slots with real `<img>`.
- `assets/` — all images/videos listed above.
