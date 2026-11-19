# Technical & On-Page SEO Audit — Tavola Creative (corrected)

Audited: 2026-11-13 | Domain: tavolacreative.com | Method: live crawl + render

## 1. Snapshot

- https://www.tavolacreative.com/ (canonical self-referencing, www).
- Stack (confirmed): WordPress + Elementor (+ Elementor Pro, ElementsKit Lite,
  WP Rocket, Google Site Kit) + **Rank Math SEO**. Not Yoast.
- Markets: Chicago, IL and Kansas City.
- Rebrand banner present: "West Peak Collective is now Tavola Creative".

## 2. Verified issues (real)

1. **Footer legal/social anchors have no href.**
   - "Privacy Policy" and "Terms and Conditions" render as `<a>` with no `href`.
   - Footer "Facebook", "Twitter", "Youtube" social labels also render as
     no-href anchors (upper-footer icons link to FB/IG correctly).
   Fix: give them real URLs.
2. **Static zero counters** on `/web-design-services/`: the counter widgets
   render `0` "service offerings", `0` "stage process", and 100% "flexible
   project scope" in HTML. Set real initial values.
3. **Blog archive heading pollution + duplicated loop** on `/blogs/`:
   - Category names ("Marketing Strategy", "Case Study", "Uncategorized") are
     wrapped in `<h2>` (21 H2s total).
   - The "Latest Articles" grid repeats the same featured 5 posts shown above.
   Fix: category badges → `<span>`; card titles → `<h3>`; remove the duplicated
   loop; retire "Uncategorized".
4. **Missing image alt / `alt="WordPress"`.** `/blogs/` has `alt="WordPress"`
   ×4 and 14 of 30 images without alt.
5. **Conflicting NAP.** Footer shows both the physical office
   (939 W North Ave, Suite 750, Chicago, IL 60642) and a PMB
   (2045 W Grand Ave, Suite B, PMB 28197, Chicago, IL 60612-1577). Use the
   physical HQ only.
6. **Typos.** Chicago location eyebrow reads "Serving Business in chicago"
   (should be "Serving Businesses in Chicago"); Kansas City footer anchor reads
   "Kansas".
7. **No dedicated `/seo-services/` page** — `/seo-services/` returns 404 even
   though SEO is promoted as a service.
8. **Heavy front-end.** 37 `.css` links / 39 stylesheet rels and multiple
   Elementor `<nav>` wrappers per menu instance. Consolidate for Core Web
   Vitals.

## 3. Corrections to the supplied report

- **"5 Google Font families: Roboto, Roboto Slab, Montserrat, Glory, Outfit."**
  FALSE. The single combined Google Fonts request pulls **Glory, Roboto,
  Montserrat** only. "Roboto Slab" and "Outfit" do **not** appear anywhere on
  the page (0 occurrences).
- **"Phone anchor outputs `about:invalid#zCSafez`."** FALSE. There are **0**
  occurrences of `about:invalid`; the phone link is a valid `tel:8479251489`.
- **"27 stylesheets / triple-duplicated `<nav>`."** Directionally right but
  imprecise: the homepage has 37 `.css` links, and the 9 `<nav>` nodes are
  Elementor's per-menu main+dropdown wrappers rather than a clean "3 copies".
- The rest (no-href Privacy/Terms, category `<h2>`s, duplicate 5-post loop,
  static counters, `alt="WordPress"`, PMB vs HQ, West Peak banner,
  missing `/seo-services/`) is **confirmed**.

## 4. Recommended JSON-LD

```json
{
  "@context": "https://schema.org",
  "@type": "ProfessionalService",
  "@id": "https://www.tavolacreative.com/#organization",
  "name": "Tavola Creative",
  "alternateName": "West Peak Collective",
  "url": "https://www.tavolacreative.com/",
  "telephone": "+1-847-925-1489",
  "priceRange": "$$$",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "939 W North Ave, Suite 750",
    "addressLocality": "Chicago",
    "addressRegion": "IL",
    "postalCode": "60642",
    "addressCountry": "US"
  },
  "areaServed": [
    { "@type": "City", "name": "Chicago",
      "containedInPlace": { "@type": "State", "name": "Illinois" } },
    { "@type": "City", "name": "Kansas City",
      "containedInPlace": { "@type": "State", "name": "Missouri" } }
  ],
  "sameAs": [
    "https://www.facebook.com/tavola.creative",
    "https://www.instagram.com/tavola.creative",
    "https://tavola.group/"
  ],
  "knowsAbout": [
    "Digital Marketing", "Web Design", "Social Media Marketing",
    "Paid Advertising", "Brand Strategy", "Search Engine Optimization"
  ]
}
```

## 5. Priority actions

1. Add real `href` values to footer Privacy Policy, Terms and social links.
2. Set real counter values on `/web-design-services/`.
3. Fix `/blogs/` headings (category → `<span>`, cards → `<h3>`) and remove the
   duplicated 5-post loop.
4. Remove the PMB address; keep only 939 W North Ave, Suite 750.
5. Fix the "chicago"/"Kansas" typos.
6. Publish a dedicated `/seo-services/` page.
7. Add alt text and de-duplicate Elementor CSS/nav for Core Web Vitals.
