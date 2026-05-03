# Nebyan Doğal — Developer Handoff
**Version:** 1.0  
**Date:** May 2026  
**Prepared by:** Busy Istanbul  
**Client:** Nebyan Doğal Gıda San. Tic. A.Ş.

---

## Package Contents

```
nebyan-design/
├── nebyan-tokens.css        ← Single source of truth for all design variables
├── nebyan-icons.css         ← Icon utility class system
├── nebyan-icons.svg         ← SVG sprite (46 icons, load once in <body>)
├── pages/
│   ├── homepage.html        ← Full homepage layout
│   ├── category.html        ← Category / shop listing page
│   └── product-detail.html  ← Product detail page
└── HANDOFF.md               ← This file
```

---

## Platform

Custom stack. Not Shopify or WordPress.

These files are **design-faithful HTML prototypes** — pixel-accurate representations of the intended design. They are not a framework or CMS template. The developer should use these as a visual specification and build the production templates against them.

---

## How to Use the Shared Files

### 1. Load tokens first
Every page must import `nebyan-tokens.css` before any other stylesheet.

```html
<link rel="stylesheet" href="/assets/css/nebyan-tokens.css">
<link rel="stylesheet" href="/assets/css/nebyan-icons.css">
```

### 2. Load the SVG sprite once
Place the sprite inline at the top of `<body>` on every page (or inject it via a server-side include). This avoids CORS issues with external SVG files.

```html
<body>
  <!-- SVG sprite — must be first element in body -->
  <?php include 'nebyan-icons.svg'; ?>
  <!-- or for Node/template engines: -->
  <%- include('nebyan-icons.svg') %>
```

### 3. Use icons
```html
<span class="nb-icon nb-icon-20 nb-icon-muted">
  <svg><use href="#ni-truck"/></svg>
</span>
```

**Size classes:** `nb-icon-14` / `nb-icon-16` / `nb-icon-20` / `nb-icon-24` / `nb-icon-28` / `nb-icon-32` / `nb-icon-48`  
**Color classes:** `nb-icon-black` / `nb-icon-muted` / `nb-icon-green` / `nb-icon-accent` / `nb-icon-amber` / `nb-icon-white` / `nb-icon-red`

---

## Typography

### Fonts
Both fonts are **licensed** — they are not available via Google Fonts CDN.

| Font | Weight | Usage |
|------|--------|-------|
| DM Sans | 400, 500, 700, 800 | All UI text, body, buttons, labels |
| DM Serif Display | Regular (italic) | Hero headlines, promo titles, testimonial quotes only |

For development/preview, use the Google Fonts CDN:
```html
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,400;0,9..40,500;0,9..40,700;0,9..40,800&family=DM+Serif+Display&display=swap" rel="stylesheet">
```

For production, self-host both fonts and update `--font` and `--serif` in `nebyan-tokens.css`.

---

## Design Tokens Reference

All variables are declared in `nebyan-tokens.css`. Do not hardcode any of these values in component CSS.

### Colours
| Token | Value | Usage |
|-------|-------|-------|
| `--black` | `#111111` | Primary text, buttons, borders on hover |
| `--white` | `#ffffff` | Card backgrounds, nav |
| `--bg` | `#F5F5F5` | Page background, image placeholders |
| `--border` | `#E0E0E0` | All card and component borders |
| `--text` | `#444444` | Body copy |
| `--muted` | `#888888` | Secondary text, icons |
| `--green-dark` | `#1A4731` | Primary brand green, promo bar, nav badge |
| `--green-mid` | `#2D6A4F` | Green borders on attribute tags |
| `--green-accent` | `#22C55E` | Stock dot, fresh badge, checkmarks |
| `--amber` | `#F59E0B` | Sale badge, star rating, promo accent |
| `--rust` | `#8B2800` | Promo banner background |
| `--sale-red` | `#dc2626` | Sale labels and nav sale link |
| `--cream` | `#F0EDE8` | Testimonial section background |
| `--bg-dark` | `#1A1A1A` | Hero, newsletter, dark sections |
| `--bg-dark-input` | `#2a2a2a` | Dark section form inputs |
| `--green-tint-bg` | `#f0fdf4` | Promo/success box fill |
| `--green-tint-bd` | `#bbf7d0` | Promo/success box border |
| `--green-attr-bg` | `#f0faf4` | Product attribute tag fill |

### Layout
| Token | Value | Usage |
|-------|-------|-------|
| `--max-width` | `1200px` | All content containers |
| `--page-x` | `40px` | Horizontal page padding |
| `--nav-height` | `64px` | Sticky nav height |
| `--nav-z` | `200` | Nav z-index |

### Border Radius
| Token | Value | Usage |
|-------|-------|-------|
| `--r-sm` | `8px` | Small elements (checkboxes, payment badges) |
| `--r-md` | `12px` | Cards, filter sidebar, accordions |
| `--r-lg` | `16px` | Product cards, recipe cards, sidebar |
| `--r-xl` | `20px` | Gallery main image, promo banners, split images |
| `--r-pill` | `100px` | All buttons, search pills, all badges |

---

## Page Structure

### Homepage (`homepage.html`)
| Section | Notes |
|---------|-------|
| Promo bar | Green `--green-dark` background. CMS-editable text + link. |
| Sticky nav | 64px, z-index 200. Logo links to homepage. |
| Hero | Dark bg with green gradient. Serif headline. 3 float cards right side. |
| Category strip | 8 icons across. Circular border, 72px. Links to category pages. |
| Featured products | 4-column grid. Trust tag pills above. Hover reveals quick-add. |
| Promo banner | Rust `--rust` background. Serif amber headline. CMS-driven. |
| Trust strip | 3-column, 1px gap (acts as separator). |
| About / FAQ | 50/50 split. Image left, FAQ accordion right. |
| Feature cards | 4-column. Icon + title + desc + link. |
| Testimonials | Cream bg. Carousel: prev/next + dot indicators. |
| Newsletter | Dark bg. Email input + submit. |
| Info strip | 4 contact cards on `--bg`. |
| Footer | 4-column: logo+tagline, 3 link groups. |

### Category (`category.html`)
| Section | Notes |
|---------|-------|
| Breadcrumb | `Anasayfa › Taze Et Ürünleri` |
| Category hero | Title + result count + sub-category pills (filter tabs). |
| Sidebar | Sticky at `top: 80px` (nav height + 16px). Collapsible filter groups. |
| Sort bar | Result count + active filter chips + sort dropdown + grid/list toggle. |
| Product grid | 3-column (within sidebar layout). Hover: quick-add + wishlist appear. |
| Pagination | Page numbers + prev/next arrows. |

### Product Detail (`product-detail.html`)
| Section | Notes |
|---------|-------|
| Breadcrumb | 4-level: `Anasayfa › Taze Et Ürünleri › Dana Ürünleri › [Product]` |
| Product main | 50/50: gallery left, info right. |
| Gallery | Thumbnail strip + main image + zoom/nav buttons. |
| Product info | Vendor, title, price+discount, attribute tags, stock, description, weight options, qty+cart, trust strip, pickup, match carousel, share. |
| Accordion | Besin Değerleri (open by default), İçindekiler, Saklama Koşulları, Kargo ve İade. |
| Cooking methods | Tava / Fırın / Tencere / Izgara — custom SVG icons. |
| Payment box | Payment logos + shield icon + security text. |
| Recipes | 4-column grid linked to Nebyan Mutfak blog. |
| Related products | 4-column "Son Gezilen Ürünler". |
| Info strip + Newsletter + Footer | Same as homepage. |

---

## CMS Fields Required

The following fields must be mapped in the CMS for dynamic content to render correctly.

### All Pages
- Site-wide promo bar text + link URL
- Navigation category labels + URLs
- Footer link groups

### Product Detail — fields that currently have NO CMS mapping (must add):
| Field | Description |
|-------|-------------|
| Product image(s) | Gallery thumbnails + main image |
| Product description | Long text / rich text |
| Besin değerleri | Nutrition table (enerji, protein, yağ, karbonhidrat, sodyum) |
| İçindekiler | Ingredients text |
| Saklama koşulları | Storage conditions |
| Pişirme önerileri | Multi-select: Tava / Fırın / Tencere / Izgara |
| Yanında alınanlar | Related product references (up to 3) |
| Yemek tarifleri | Related recipe references (up to 4) |

See the existing panel screenshot in the project brief for currently available fields.

---

## What To Add Before Going Live

- [ ] Favicon (`/favicon.ico` + SVG favicon)
- [ ] Self-hosted fonts replacing Google CDN import
- [ ] Open Graph image (`og:image`) for each page type
- [ ] Canonical URLs (`<link rel="canonical">`)
- [ ] Google Analytics / GTM tag
- [ ] Cookie consent banner (KVKK compliance — Turkish law requires this)
- [ ] Structured data / JSON-LD for product pages (Schema.org `Product`)
- [ ] 404 page
- [ ] Form handling for newsletter signup (backend or Mailchimp/Klaviyo)

---

## Browser Support

Design targets: Chrome 110+, Safari 16+, Firefox 115+, Edge 110+.  
No IE support. SVG `<use href>` is supported in all modern browsers.

---

## Contact

**Design:** Busy Istanbul — batujohn@busyistanbul.com  
**Client:** Nebyan Doğal — info@nebyandogal.com
