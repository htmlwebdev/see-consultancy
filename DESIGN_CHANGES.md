# SEE Website Revamp — Design & Change Document

**Project:** Simplify Energy Economics (SEE) — `see-energy.co.uk`
**Author:** Arshad
**Date:** April 2026
**Source documents reviewed (in `data/`):**

- `SEE Website Draft Content.docx` — page-by-page copy
- `Website Writeup.docx` / `Website Writeup.pdf` — long-form text per page
- `SEE Color Pallet -1.pptx` — new brand palette
- `SEE_Website_Demo.pdf` / `SEE_Website_Demo.pptx` — visual mock-up the client signed off on

---

## 1. What the client is asking for, in one paragraph

The current site (built late-2024) is a generic Bootstrap "consultancy" template with placeholder copy and stock imagery. The client wants the *structure* to look broadly similar (a clean hero, section blocks, footer with quick links), but every piece of copy, the navigation, the team line-up, the colour palette, and one **entirely new page** ("Our Expertise") need to change. The home page tagline becomes **"Helping you to SEE Through"**, and the company is now positioned as an analytical, advisory **and training** firm — training is currently invisible on the live site.

---

## 2. Page-level inventory & change matrix

| # | Current page | New page | Change type | Summary of change |
|---|---|---|---|---|
| 1 | `index.html` | `index.html` | **Major rewrite** | New tagline, new "About SEE" blurb, new "What we do" block, simplified footer, palette swap |
| 2 | `about.html` | `about.html` | **Major rewrite** | Replaces all copy with Our Story / Our Clients / Our Team (3 people) / Our Approach / Testimonials |
| 3 | `services.html` | `services.html` | **Major rewrite** | Splits into **Consultancy Services** (12 cards) and **Training Services** (6 cards) |
| 4 | — | `expertise.html` | **NEW PAGE** | 8 expertise pillars, each with bullets |
| 5 | `contact.html` | `contact.html` | **Light edit** | Replaces "Our Services" panel with **"Why choose us"** (5 reasons), keeps form & cards |
| 6 | `privacy-policy.html` | `privacy-policy.html` | **Style only** | Header/footer/colour pass to match the rest |
| 7 | `terms-of-service.html` | `terms-of-service.html` | **Style only** | Header/footer/colour pass |
| 8 | `404.html` | `404.html` | **Style only** | Header/footer/colour pass |

---

## 3. Navigation

| Position | Current | New |
|---|---|---|
| 1 | Home | Home |
| 2 | About Us | About us |
| 3 | Services | Services |
| 4 | Contact | **Our Expertise** *(new item)* |
| 5 | — | Contact us |

The same nav goes on **every** page (active state per page). Footer "Quick Links" mirrors this list.

---

## 4. Brand palette (from `SEE Color Pallet -1.pptx`)

The current CSS uses `#235954` (a hard-coded teal). The client's new palette keeps that primary teal and layers in cool blues / soft cyans. All new pages will route through CSS variables in `css/see-theme.css` so a single edit can re-tone the whole site.

| Role | Hex | Where it's used |
|---|---|---|
| **Primary — Logo / important** | `#255951` | Logo, headlines, key buttons, link hovers |
| Primary Dark (blue) | `#4075AA` | Section accents, secondary buttons |
| Primary Light (cyan) | `#86CFD6` | Card hover states, divider accents |
| Secondary Light | `#72C1E8` | Tags, soft highlights |
| Secondary Dark | `#7365A7` | Sparingly — section dividers, icons |
| Alternate text | `#476EA1` | Body emphasis, sub-headlines |
| Alternate dark | `#476893` | Footer background tint |
| Alternate light | `#EFFEFE` | Section backgrounds (very pale) |
| Alternate light 2 | `#F8F9FA` | Cards / page background |
| Alternate accent | `#69009E` | CTA hover (use sparingly) |

Typography stays on the existing system stack (Open Sans / Bootstrap defaults) — the client did not call for a font change, only "fonts to be discussed and finalized".

Icons should come from **flaticon.com** (per the writeup), images from **unsplash.com**. For now the preview uses Font Awesome (already shipped with the site) so the layout is faithful but doesn't pull in unlicensed imagery.

---

## 5. Detailed copy & component changes (per page)

### 5.1 Home (`index.html`)

| Block | New copy |
|---|---|
| Hero H1 | **Helping you to "SEE" Through** |
| Hero sub | We help energy companies, investors, and policymakers make smarter, faster, and more resilient decisions across the global energy value chain. |
| Hero CTAs | "Our Services" (→ services.html), "Contact Us" (→ contact.html) |
| About SEE block H2 | About SEE |
| About SEE body | From market analysis and economic evaluation to project financing, trading strategies, and executive training, we deliver data-driven solutions that bridge industry experience with advanced analytics. |
| About SEE CTA | "Learn More" → `about.html` |
| What we do H2 | What we do |
| What we do body | We offer a wide range of services and collaborative training programs in the energy sector. |
| What we do CTA | "Learn More" → `services.html` |
| Footer blurb | Simplify Energy Economics (SEE), a company registered in Scotland U.K., provides expert analytical and advisory support across the energy sector. For more details follow us on LinkedIn. |
| Footer Quick Links | About us · Services · Our Expertise · Contact |
| Footer Copyright | © 2026 SEE. All Rights Reserved. · Terms of Service · Privacy Policy |

**Removed from old home:** the slider with two slides + "Our Solutions for Energy Sector" generic stats + the partner logo strip (until real partners are confirmed).

### 5.2 About us (`about.html`)

Sections, in this order:

1. **Our Story** — full ~250-word paragraph from the writeup (15+ years experience, full-value-chain pitch, mission statement).
2. **Our Clients** — 11 client-type tiles: Upstream Companies, Midstream Operators, LNG & Natural Gas, Energy Finance firms, Solar & Wind companies, Energy Utilities, Consultancy firms, National Oil Companies, International Oil Companies, Investment companies, Trading firms.
3. **Our Team** — three cards (image placeholder + bio + LinkedIn + email):
   - Raj Srivastava — Founder, Director & Principal Economist
   - Dilip Jena — Energy Economist & CEPMLP Lecturer (Dundee)
   - Vikas Kooneti — Senior Analyst
4. **Our Approach** — narrative + 3 emphasis bullets (Clarity over complexity / Decision relevance / Transparency and robustness).
5. **Testimonials** — 3 quotes captured from `SEE_Website_Demo.pdf` page 7:
   - Haitham Ghais — Head of OPEC
   - Alex Kemp — Professor, Aberdeen
   - Amir Alizadeh — Director CGCSTF, Bayes Business School London

### 5.3 Services (`services.html`)

Two sub-sections, each with intro paragraph + cards:

**Consultancy Services** (12 cards):
1. Investment Analysis & Valuation
2. Project Economics & Financial Modeling
3. Risk Analysis & Sensitivity Assessment
4. Transaction Support & Due Diligence
5. Deal Structuring & Commercial Advisory
6. Portfolio Services & Optimization
7. Asset Optimization & Performance Analysis
8. Trading Advisory & Market Execution Support
9. Data Analytics & Decision Support
10. Market Research, Analysis & Forecasting
11. Strategy Development & Growth Planning
12. Market Entry & Expansion Strategy

**Training Services** (6 cards):
1. Applied Energy Economics & Financial Modeling
2. Real Industry Case Studies & Applications
3. Energy Markets, Trading & Hedging Workshops
4. Portfolio Optimization & Investment Strategy
5. Tailored Corporate & Executive Training
6. Practical Learning & Capability Building

Each card holds 4 bullet points (verbatim from writeup) on hover/expand.

### 5.4 Our Expertise (`expertise.html`) — NEW

8 expertise pillars laid out as alternating left/right blocks (icon + heading + 4 bullets):

1. Oil & Gas Fiscal Modeling & Energy Economics (PSC & JV Frameworks)
2. Renewable Energy & Power Markets
3. Financial Modelling & Investment Analysis
4. Project Finance & Debt Structuring
5. Market Research & Price Forecasting
6. M&A Strategy & Commercial Advisory
7. Data Analytics, Forecasting & Digital Optimization
8. Trading, Risk Management & Derivatives
9. Executive Training & Capability Building *(9th, kept because it's a distinct pillar in the writeup)*

### 5.5 Contact (`contact.html`)

Existing layout works. Change:

- Replace the "Our Services" sidebar with a **"Why choose us"** panel (5 bullets from draft content):
  - Proven Industry Experience
  - Globally Recognized Expertise
  - Data-Driven & Transparent Methodologies
  - Commercially Relevant Insights
  - High-Quality Training & Knowledge Transfer
- Update LinkedIn card copy and email card copy to match the demo PDF page 20.
- The form keeps its current `js/contact.js` validation hook.

### 5.6 Privacy / Terms / 404

Pure cosmetic refresh — same nav, same footer, same colour variables.

---

## 6. Things explicitly **out of scope** for this preview

1. **Real photography** — hero and "visual" split-blocks use Unsplash URLs (already wired in CSS). Team photos (`raj-srivastava.jpg`, `dilip-jena.jpg`, `vikas-kooneti.jpg`) are now real assets in `preview/images/` — these replaced the original placeholder-initials approach.
2. **Final logo asset** — SVG logo (`preview/images/see-logo.svg`) is live in the header. Falls back to `../favicon/header-logo.png` if SVG fails to load.
3. **Form back-end** — the contact form posts to the same handler the live site uses; nothing in the preview changes that.
4. **Custom font** — pending client decision.
5. **Partner logos** on the home page — removed until real partners are confirmed.

---

## 7. File structure of this preview

```
preview/
├── DESIGN_CHANGES.md         ← this document
├── HOSTING.md                ← how to run the dev server / Cloudflare deploy
├── index.html                ← new home
├── about.html                ← new about
├── services.html             ← new services
├── expertise.html            ← NEW page
├── contact.html              ← refreshed contact
├── privacy-policy.html       ← style refresh
├── terms-of-service.html     ← style refresh
├── 404.html                  ← style refresh
└── css/
    └── see-theme.css         ← new palette + overrides for all pages
```

The preview reuses the live site's `css/`, `js/`, `fonts/`, `images/`, `favicon/` folders by relative path (`../css/...`) so we don't duplicate ~1 MB of vendor assets. The dev server (see `HOSTING.md`) is started from the **repo root** so those paths resolve.

---

## 8. Sign-off & promote-to-production plan

Once the client approves the preview:

1. Move the 8 HTML files in `preview/` up to the repo root (overwriting the old ones).
2. Move `preview/css/see-theme.css` to `css/see-theme.css` and add it to the existing `<link>` chain in each page (or merge it into `css/style.css`).
3. Update `sitemap.xml` to add `/expertise.html` and bump `<lastmod>` on every URL.
4. Delete the `preview/` folder (or leave it for the next iteration).
5. Commit, push to `main`, GitHub Pages auto-deploys.

If you switch to Cloudflare Pages mid-flight, see `HOSTING.md` §3 — it's a one-time `wrangler pages project create` and points at the same Git repo.

---

## 9. Implementation status & deviations from source documents

**Last updated:** April 2026

### 9.1 What's done

| Item | Status | Notes |
| --- | --- | --- |
| Brand palette (`css/see-theme.css`) | ✅ Done | All 10 colour variables live; overrides Bootstrap/style.css throughout |
| Compact sticky header | ✅ Done | Single-bar layout with logo, nav links, "Contact us" CTA button |
| Mobile nav (hamburger) | ✅ Done | Animated 3-bar → X toggle; slides open below header |
| `index.html` | ✅ Done | Hero, About SEE split, What We Do split, Capabilities cards, CTA strip, footer |
| `about.html` | ✅ Done | Our Story, Our Clients (11 tiles), Our Team (3 cards), Our Approach + pill list, Testimonials |
| `services.html` | ✅ Done | Consultancy (12 cards) + Training (6 cards), each with 4 bullets |
| `expertise.html` | ✅ Done | 9 alternating expertise rows (8 original pillars + Executive Training as a full pillar) |
| `contact.html` | ✅ Done | "Why choose us" panel (5 bullets), form, LinkedIn & email cards |
| `privacy-policy.html` | ✅ Done | Style refresh only |
| `terms-of-service.html` | ✅ Done | Style refresh only |
| `404.html` | ✅ Done | Style refresh only |
| SEO meta tags | ✅ Done | Full suite on all pages — see §9.3 below |
| Team photos | ✅ Done | Real images (`raj-srivastava.jpg`, `dilip-jena.jpg`, `vikas-kooneti.jpg`) in `preview/images/` |
| Testimonials | ⏸ Pending greenlight | HTML is fully built in `about.html`; section is live in the preview but **not promoted to production** until client confirms the quotes are accurate and authorised |

### 9.2 UI choices that differ from the PPT / Word doc

The following are **intentional deviations** made during build, not oversights. All are open for feedback.

1. **Home — "Where we add value" capability cards (new section)**
   The original designs showed Hero → About SEE → What We Do → Footer with no capability preview on the home page. A third section was added with 6 feature cards ("Energy Economics & Project Evaluation", "Market Research & Price Forecasting", "Strategy M&A & Commercial Advisory", "Renewables & Energy Transition", "Data Analytics & Digital Tools", "Executive Training") plus a dark "Have a project on the table?" CTA strip above the footer. Rationale: a home page that immediately signals the firm's range without forcing visitors to click through to Services first. Can be removed or collapsed if the client prefers a cleaner scroll.

2. **Home — "Talk to us" ghost button (secondary CTA)**
   The design doc specified "Contact Us" as the secondary hero button. Changed to "Talk to us" to be less transactional alongside "Our Services". Easy to revert.

3. **Home — "What we do" copy expanded**
   Added "— covering upstream, midstream, LNG, power, renewables, and the energy transition" to the sub-text. Not in the original draft but makes the scope explicit.

4. **About — section heading copy**
   The About SEE block headline reads "Bridging industry experience with advanced analytics" rather than the generic "About SEE" H2 in the mock-up. Feels less placeholder-y; reverts to original on request.

5. **Expertise — 9 pillars, not 8**
   The design doc listed 8 pillars with "Executive Training & Capability Building" as a parenthetical 9th. The build treats it as a full, equal pillar because it represents a distinct revenue line. The page title also reads "Nine Energy Pillars" in the SEO. Can be collapsed back to 8 if preferred.

6. **Testimonials — present but on hold**
   Testimonials are fully built in `about.html`. They are visible in the preview but will not go live until Raj confirms the quotes, names and titles are accurate and that the individuals have consented to being cited publicly.

7. **Team cards — real photos used**
   The original plan was initials-placeholder for team cards. Actual photos were added to `preview/images/`. If any photo needs replacing or cropping, swap the file and the `<img src="">` in `about.html`.

### 9.3 SEO additions (not in original scope)

Every page now has a complete SEO head block:

- **Primary meta tags** — `<title>`, `<meta name="description">`, `<meta name="keywords">`, `author`, `publisher`, `copyright`, `robots`, `canonical`, `geo.region`, `geo.placename`
- **Open Graph** — `og:type`, `og:title`, `og:description`, `og:url`, `og:image` (1200×630, pointing to `see-og-image.jpg`), `og:image:alt`, `og:locale`, `og:site_name`
- **Twitter / X Card** — `summary_large_image` card with title, description, image
- **Browser / PWA** — `theme-color`, `msapplication-TileColor`, `format-detection`
- **JSON-LD structured data** — `Organization`, `WebSite`, `WebPage` (or `AboutPage` / `ItemPage`) graph on every page; `index.html` includes full `hasOfferCatalog`; `about.html` includes `employee` Person nodes for all three team members and three `Review` nodes for testimonials

**Still needed before go-live:**

- Create `images/see-og-image.jpg` (1200×630 hero image) at the repo root
- Confirm all canonical URLs resolve on the live domain
- Submit updated `sitemap.xml` (with `expertise.html` added) to Google Search Console

---

## 10. April 2026 update — V2 content + visual sharpening

Round of changes driven by client review of `data/SEE Website Draft Content V2.pdf` and a follow-up note on visual quality. Each item below maps 1:1 to a red-highlighted change in the V2 PDF or to a direct client request.

### 10.1 Copy changes from V2 PDF

**`about.html` — Raj Srivastava bio (`#raj-srivastava` card and JSON-LD)**

- Reworded experience description from *"market research, strategy development, financial modelling, and due diligence"* → *"valuation, modeling, strategy development, and due diligence"* (matches V2 PDF page 2).
- Tightened the M&A advisory sentence: *"Before these roles, he worked in M&A advisory with Deloitte and CGG Robertson UK."*
- Replaced the energy-transition sentence with *"Raj has also led workstreams in the energy-transition space."* and added the Symposium-2021 talk on its own sentence.
- Added Warwick scholarship note: *"…which he completed on a scholarship…"*
- Certifications list now ends in **ESG Investing** (was *Climate Finance*).
- **NEW third paragraph** — community / yoga instructor / London Marathon 2025 / IIT & ISM alumni boards.

**`expertise.html` — Pillar 5 (Market Research & Price Forecasting)**

- Removed bullet *"Energy-transition commodities (lithium, nickel, copper) assessment"* (struck through in V2 PDF).
- Added bullet *"Power markets & energy-transition dynamics"*.

**`expertise.html` — Pillar 8 (Trading, Risk Management & Derivatives)**

- Reworded *"Hedging frameworks for price, basis, and volume risk"* → *"Risk management & hedging programs across price, basis, and volume risk"* (matches V2 wording).

### 10.2 Visual changes (client request)

**Team photos no longer blurry (`about.html` + `css/see-theme.css`)**

The source files in `preview/images/` are small (Raj 355×355, Dilip 200×200, Vikas 116×114). The previous CSS used `aspect-ratio: 1/1` on the photo block, which forced the images to fill the full card width (~360 px+ on desktop) and visibly upscaled them. The card layout now uses a **150×150 circular avatar** centred at the top of each card with a white border + soft shadow. The photos are no longer upscaled, so blur is gone. Body text below the avatar is centre-aligned for headings/role, left-aligned for the bio paragraphs.

**Higher-contrast palette (`css/see-theme.css` `:root` variables)**

The previous palette read as a bit washed out, especially against white sections. Each variable was deepened / saturated:

| Variable | Old | New | Why |
| --- | --- | --- | --- |
| `--see-primary` | `#255951` | `#1A4A43` | deeper teal — stronger headings, buttons, links |
| `--see-primary-dark` | `#4075AA` | `#2E5FA0` | richer steel blue accent |
| `--see-primary-light` | `#86CFD6` | `#5FB8C2` | punchier hover/light accents |
| `--see-secondary-l` | `#72C1E8` | `#2FA4DC` | saturated sky blue tag colour |
| `--see-secondary-d` | `#7365A7` | `#5A4A99` | deeper purple divider |
| `--see-alt-accent` | `#69009E` | `#7A00B5` | sharper CTA hover |
| `--see-text` | `#1f2a30` | `#131c21` | darker primary copy |
| `--see-body` | `#3a4750` | `#2b363e` | stronger body grey |
| `--see-muted` | `#5b6770` | `#4a565f` | tighter muted contrast |
| `--see-border` | `#e6eef0` | `#d8e3e6` | slightly stronger borders |
| `--see-bg-soft` | `#EFFEFE` | `#E5F8F8` | a touch cooler / more visible |

All other styling cascades through the variables, so the deepening propagates everywhere automatically. Brand identity stays the same — the colours are darker/more saturated versions of the same hues, not new colours.

### 10.3 New section — Our Clients & Partners (`index.html`)

A new section sits between **What we do** and **Where we add value** on the home page:

1. **Heading** — "Our Clients & Partners" (with the kicker "Trust").
2. **Intro paragraph** — *"We are proud to have served many companies across the globe as clients within a short period of time. We have also collaborated with select companies to provide integrated services when needed."* (verbatim from client note).
3. **Moving logo banner** — `.see-marquee` strip with `.see-marquee-track` looping horizontally via CSS-only animation (`@keyframes see-marquee-slide`, 35s linear infinite, paused on hover). The track contains 8 logo slots duplicated for a seamless loop. Currently populated with `Client 1…5` / `Partner 1…3` placeholder tiles — **swap each `<span class="logo-placeholder">…</span>` for an `<img src="…">` once the client supplies the actual logo files** (drop them into `preview/images/clients/` and reference by relative path; CSS sizes them to 56 px tall, max 180 px wide, grayscale by default and full-colour on hover).
4. **"Who we work with" banner** — full-width gradient panel below the marquee with the heading and a short blurb. Implemented as `.see-work-banner`.

Marquee is mask-faded at the left and right edges so the loop seam is invisible, and the duplicated track means the animation can run indefinitely without snapping back.

### 10.4 Files touched in this round

```
preview/about.html              — Raj bio rewrite (3 paragraphs) + JSON-LD description
preview/expertise.html          — Pillar 5 bullet swap, Pillar 8 bullet rewording
preview/index.html              — new Clients & Partners section (marquee + banner)
preview/css/see-theme.css       — palette deepening, team-card avatar restyle,
                                  marquee + work-banner components
preview/DESIGN_CHANGES.md       — this section
```

### 10.5 Outstanding items for the client

- Provide client/partner logo files (PNG or SVG, transparent background preferred) — placeholders in the marquee track will be replaced 1:1.
- Confirm the new palette feels right against the existing logo (the request acknowledged the logo itself is muted; the site can run a slightly bolder palette around it).
- Confirm the bio third-paragraph wording (community / marathon) is the final version.
