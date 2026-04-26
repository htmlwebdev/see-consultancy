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

1. **Real photography** — we use placeholder boxes for team photos and hero imagery. The writeup says "for images visit unsplash.com" — that's a follow-up task once the client picks shots.
2. **Final logo asset** — keeping current `favicon/header-logo.png` until a high-res version is supplied.
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
