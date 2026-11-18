# Verification — "On-Page SEO Implementation Report" (Tavola Creative & Tavola International)

Verified: 2026-11-18 | Method: fresh live fetch (cache-busted) + headless-Chromium
render + page-by-page crawl of both sites' sitemaps, compared against my
2026-11-13 baseline snapshots.

The report is a 1-page "TASK COMPLETION REPORT" claiming three tasks are
**Completed** for **Tavola Creative** and **Tavola International**:

1. Updated Image Alt Text
2. Set H1 Headings
3. Added Meta Descriptions

## Verdict: mostly NOT correct

Two of the three tasks are **overstated**, and the two sites are in very
different states. Only *some* real work is visible on Tavola Creative. Tavola
International shows essentially none of the three claimed changes.

| Task | Tavola Creative | Tavola International |
|---|---|---|
| Image alt text | Partial (some filled, key ones left) | **Not done** |
| H1 headings | Mostly already present; one weak, one page still missing | Already present (no change) |
| Meta descriptions | **Not done** — no change vs 13 Nov | Already present (no change) |

## 1. Image alt text — "Completed" is FALSE for Tavola International

**Tavola International (fail).** The homepage still has **8 empty-alt images**,
including the *same* content image repeated in each footer column
(`Group-3624-1024x116.png`, ×5) plus `Artboard-3-copy-6-1.webp`. This is
identical to my 13 Nov baseline — nothing changed. Every other TI page (About,
Services, Contact, Resources, all service and team pages) still shows
`empty=8`. The one missing `alt` is the Facebook pixel and the empties include
the LinkedIn pixel — those are harmless, but the *content* images are still
unlabelled.

**Tavola Creative (partial).** On the homepage and `/web-design-services/`,
empty-alt images dropped from **20 → 2** (baseline → now), so real work was
done. **But two problems remain and the report never mentions them:**

- The `/blogs/` page still carries `alt="WordPress"` **×4** on the wellness
  case-study thumbnails and a 1×1 SVG placeholder. This is the exact issue the
  original audit flagged ("thumbnail carries alt=WordPress") and it is **not
  fixed**.
- `/growing-wellness-brands-on-instagram/` still has `alt="WordPress"` ×2.
- The `/blogs/` page also still contains the **typo alt text**
  `alt="Social Media Comapign heor"` (should be "Social Media Campaign Hero")
  that the original audit explicitly called out — **not fixed**.

## 2. H1 headings — claim is misleading

**Tavola Creative.** H1s were **already present** on the 13 Nov baseline; the
only real change is that the homepage duplicate H1 (×2) was reduced to a single
H1 — good, but that is not "configured H1 headings across pages". Two real H1
problems remain, and neither is addressed:

- `/web-design-services/` H1 is still the lowercase fragment **"web design"**
  (not a proper heading).
- `/home-new-v/` has **zero H1** elements.
- `/blogs/` H1 is still the auto-generated "Blogs - Tavola Creative" (not
  keyword-targeted).

**Tavola International.** Every page already had exactly one H1 on 13 Nov
(e.g. homepage "U.S. Expat Tax Services for Americans Living Abroad"). There is
no change to point to. Also, the `/services/` H1 is still the generic
**"Our Services"**.

## 3. Meta descriptions — "Added" is FALSE

**Tavola Creative.** Meta descriptions are **byte-for-byte identical** to the
13 Nov baseline on every page I compared (home, web-design, blogs). No new meta
descriptions were added. Worse, several pages still have **no meta description
at all**:

- `/case-study/`
- `/category/uncategorized/`, `/category/marketing-strategy/`,
  `/category/case-study/`
- `/location/` archive ("Locations Archive - Tavola Creative")

**Tavola International.** Meta descriptions were already present and good on
13 Nov; they are unchanged. The report claims to have "crafted and implemented"
them, but nothing changed. (To TI's credit, the descriptions that exist are
well-written — they simply predate this task.)

## 4. Bonus finding — a fix the report didn't claim (positive)

The original audit's "Critical" footer issue **has been genuinely fixed** on
Tavola Creative: footer "Privacy Policy" and "Terms and Conditions" now have
real `href`s (`/privacy-policy/`, `/terms-and-conditions/`), whereas on 13 Nov
they were href-less. The report's three headline tasks don't mention this, so
the credit is misdirected.

## 5. Still-open items the report should have covered

On Tavola Creative (all verified still broken today):

- Footer "Twitter" and "Youtube" social labels are **still href-less**.
- Kansas City footer anchor still reads **"Kansas"** (not "Kansas City").
- Chicago eyebrow still reads **"Serving Business in chicago"** (lowercase,
  grammar).
- Kansas City alt still reads **"Social Media Comapign heor"**.
- `/web-design-services/` counters now carry `data-to-value` 9/9/100 — but the
  original audit's concern was the *rendered* value; this looks improved and is
  worth confirming visually.
- `/case-study/` and category pages still lack meta descriptions.

On Tavola International (all still broken today):

- 8 empty-alt content images on every page.
- `/services/` H1 is "Our Services" (generic).

## Bottom line

The report over-claims. Genuine partial progress exists on Tavola Creative
(alt text on service pages, homepage duplicate-H1 removed, footer legal links
fixed), but **the "Meta Descriptions" task was not done on either site**, the
**"Image Alt Text" task was not done on Tavola International**, and the
**"H1 Headings" task was largely already complete before this work started**.
