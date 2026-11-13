# Technical & On-Page SEO Audit — Tavola Realty (corrected)

Audited: 2026-11-13 | Domain: tavolarealty.com | Method: live crawl + full
headless-Chromium render (with scroll, 5s settle) + schema parse

## 1. Snapshot

- https://www.tavolarealty.com/ (canonical self-referencing, www).
- Stack (confirmed): WordPress + Elementor (+ Elementor Pro) + **Yoast SEO**
  (confirmed via `yoast-schema-graph`) + iHomefinder **Kestrel** IDX
  (`kestrel.idxhome.com` scripts present).
- Content: 15 team pages (`/team/…`), 13 neighborhood pages (`/neighbor/…`).

## 2. Verified issues (real)

1. **"Home -" title prefix.** `<title>Home - Tavola Realty | Chicago Real Estate
   & Homes for Sale</title>`. Remove the generic prefix.
2. **Neighborhood pages have no H1.** `/neighbor/forest-park/` renders
   `h3 Explore` + `h2 Forest Park` … and **zero `<h1>`**. Promote the
   neighborhood name to an H1 (e.g. "Forest Park, IL Real Estate & Homes for
   Sale") across the template.
3. **Static zero market counters.** Rendered HTML shows
   "List-to-Sale Price Ratio 0 K / Avg. Days on Market 0 / Total Sales Volume
   $0 B / Homes Sold 0". Render real figures server-side.
4. **All images missing alt.** 28 of 28 images have empty/missing alt (not just
   the logos). Add descriptive alt text.
5. **29 render-blocking stylesheets** in the raw HTML (34 `rel=stylesheet`).
   Consolidate/minify.
6. **Duplicate navigation.** The 15-agent submenu is repeated across multiple
   `<nav>` wrappers (desktop + mobile). Reduce duplication to protect INP.
7. **Footer YouTube link** points to `youtube.com/@Tavolagroup` (group account,
   not the Realty channel).

## 3. Corrections to the supplied report

The supplied report's two **"Critical"** findings are **not reproducible**:

- **"39 Event items on the homepage, zero RealEstateAgent."** FALSE. The
  homepage schema graph (both raw and fully rendered) contains exactly:
  `WebPage`, `ImageObject`, `BreadcrumbList`, `WebSite`, `Organization`.
  There are **0 `Event`** items and **0 `RealEstateAgent`** items. The report's
  central premise is invented.
- **`href="about:invalid#zCSafez"` phone anchors.** FALSE. There are **0**
  occurrences of `about:invalid` in raw or rendered HTML. The phone links are
  valid `tel:+13123800636`.
- **"Footer omits street address."** FALSE. The footer already shows
  "Visit Our Office — 939 W North Ave, Suite 750, Chicago, IL 60642".
- **"Mobile drawer contains a dead `<a href="#">Join</a>`."** FALSE. Join links
  resolve to `/join-tavola/` and `/join-tavola/#application-form`.
- The `RealEstateAgent` schema **is** genuinely missing, and adding it (with
  `parentOrganization` → tavola.group) is still a valid recommendation — the
  report just reached a correct conclusion via a fabricated observation.

## 4. Recommended JSON-LD

```json
{
  "@context": "https://schema.org",
  "@type": "RealEstateAgent",
  "@id": "https://www.tavolarealty.com/#organization",
  "name": "Tavola Realty",
  "url": "https://www.tavolarealty.com/",
  "telephone": "+1-312-380-0636",
  "parentOrganization": {
    "@type": "Organization",
    "@id": "https://tavola.group/#organization",
    "name": "Tavola Group",
    "url": "https://tavola.group/"
  },
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "939 W North Ave, Suite 750",
    "addressLocality": "Chicago",
    "addressRegion": "IL",
    "postalCode": "60642",
    "addressCountry": "US"
  },
  "areaServed": [
    { "@type": "City", "name": "Chicago" },
    { "@type": "City", "name": "Forest Park" }
  ],
  "sameAs": [
    "https://instagram.com/tavolarealty/",
    "https://www.linkedin.com/company/tavola-realty/"
  ]
}
```

## 5. Priority actions

1. Remove "Home -" from the homepage title.
2. Add an H1 to every `/neighbor/*` template.
3. Render real market figures instead of static 0 counters.
4. Add descriptive alt text to all images.
5. Consolidate the 29 stylesheets and de-duplicate the navigation.
6. Add `RealEstateAgent` JSON-LD linked to `tavola.group`.
