# On-Page SEO Status Report (corrected) — Tavola Creative & Tavola International

Re-verified live: 2026-11-18 | Method: cache-busted fetch + headless-Chromium
render + page-by-page crawl of both sitemaps, diffed against a 2026-11-13
baseline.

This replaces the supplied "On-Page SEO Implementation Report", which marks
three tasks (alt text, H1s, meta descriptions) as "Completed" for both sites.
That is not accurate. Below is the true state, per task and per page.

## Status summary

| Task | Tavola Creative | Tavola International |
|---|---|---|
| Image alt text | Partial — service pages done, blogs/case-study not | Not done |
| H1 headings | Was already mostly done; one weak H1, one page missing H1 | Already done; one generic H1 |
| Meta descriptions | Not done — no change; some pages still have none | Already done; unchanged |
| Footer legal links (unclaimed) | Fixed (credit due) | n/a |

## A. Tavola Creative (https://www.tavolacreative.com/)

### A1. Image alt text — PARTIAL

Done:
- Homepage and `/web-design-services/`: empty-alt images reduced from 20 to 2
  (remaining 2 are a YouTube thumbnail placeholder — low priority).

Not done (should be fixed):
- `/blogs/` — `alt="WordPress"` still appears ×4; the wellness case-study
  thumbnail and a 1×1 SVG placeholder are unlabelled.
- `/blogs/` and `/location/digital-marketing-agency-kansas-city/` — the typo
  `alt="Social Media Comapign heor"` is still live. Replace with
  `alt="Social media campaign hero for Tavola Creative"`.
- `/growing-wellness-brands-on-instagram/` — `alt="WordPress"` ×2.

### A2. H1 headings — MOSTLY ALREADY DONE

Done:
- Homepage now has a single H1 ("Your Creative Partner in Digital Marketing");
  the duplicate H1 present on 13 Nov was removed.

Still to fix:
- `/web-design-services/` H1 is the lowercase fragment **"web design"** →
  "Website Design Services for Growing Brands".
- `/home-new-v/` has **no H1** → add one (or noindex/redirect this stray page).
- `/blogs/` H1 is "Blogs - Tavola Creative" → "Digital Marketing Insights &
  Resources".

### A3. Meta descriptions — NOT DONE

- Homepage, `/web-design-services/`, `/blogs/`: descriptions are byte-for-byte
  identical to 13 Nov. No change was made.
- Missing entirely (add descriptions):
  - `/case-study/`
  - `/category/uncategorized/`, `/category/marketing-strategy/`,
    `/category/case-study/`
  - `/location/` archive

### A4. Other still-open items (from the original audit)

- Footer "Twitter" and "Youtube" labels remain href-less (Privacy, Terms and
  Facebook are now linked — good).
- Kansas City footer anchor still reads "Kansas" → "Kansas City".
- Chicago eyebrow still reads "Serving Business in chicago" → "Serving
  Businesses in Chicago".
- `/web-design-services/` counters now carry `data-to-value` 9 / 9 / 100 —
  confirm the rendered (post-animation) values display correctly for crawlers.

## B. Tavola International (https://www.tavola.international/)

### B1. Image alt text — NOT DONE

- Homepage still has **8 empty-alt images**, including the same content image
  (`Group-3624-1024x116.png`) repeated in each footer column and
  `Artboard-3-copy-6-1.webp`. This is unchanged from 13 Nov.
- Every other page checked (About, Services, all service pages, Contact,
  Resources, team pages) also still shows `empty=8`.
- Fix: give each content image a descriptive alt. (The Facebook/LinkedIn pixel
  `<img>` tags can be ignored or `aria-hidden`.)

### B2. H1 headings — ALREADY DONE

- All pages already had exactly one H1 on 13 Nov. No change required.
- Optional polish: `/services/` H1 is the generic **"Our Services"** → "Expat
  Tax & Cross-Border Advisory Services".

### B3. Meta descriptions — ALREADY DONE

- All pages already carried strong, unique meta descriptions on 13 Nov. No
  change was made, and none is needed here.

## C. Recommended remaining work (priority order)

1. **Tavola International** — add alt text to the 8 unlabelled content images
   on every page (sitewide template fix).
2. **Tavola Creative** — fix `/blogs/` and the Instagram case study: remove
   `alt="WordPress"`, fix the "Comapign heor" typo, add descriptive alts.
3. **Tavola Creative** — write meta descriptions for `/case-study/`, the three
   `/category/*` archives, and `/location/`; leave existing descriptions as-is.
4. **Tavola Creative** — fix the "web design" H1 and add an H1 to
   `/home-new-v/`; fix the Kansas City / Chicago typos and the two href-less
   footer social links.
5. **Tavola International** — optionally sharpen the `/services/` H1.

## D. Note on what genuinely improved since 13 Nov

- Tavola Creative: alt text on homepage + web-design pages; homepage duplicate
  H1 removed; footer Privacy/Terms now linked.
- Tavola International: no visible change against the three claimed tasks.

The claimed "meta descriptions added" and "alt text updated sitewide" do not
hold for Tavola International, and "meta descriptions added" does not hold for
Tavola Creative.
