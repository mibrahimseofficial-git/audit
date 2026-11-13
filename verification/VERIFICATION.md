# Independent Verification of the 6 "Technical & On-Page SEO Audit" PDFs

Date of my audit: 2026-11-13
Method: live fetch + headless Chromium (Playwright) render of each site, plus
robots.txt / sitemap / schema / DNS checks. Every claim below is backed by what
the live site actually returned on this date.

## TL;DR verdict

The reports are NOT reliable. They look machine-generated and contain many
"findings" that do not reproduce against the live sites. Roughly:

- 1 of 6 reports points at a domain that does not exist at all.
- Several "Critical/High" findings are fabricated (schema items that are not
  present, broken links that are not broken, addresses that are not used).
- The parts that ARE correct are mostly the generic, template-level advice
  (title tags, JSON-LD blueprints, E-E-A-T) that applies to almost any site.

Per-site scorecard is at the bottom.

---

## 1. Buy Manufacturers Direct — buymanufacturersdirect.com

### Claims vs reality

| Report claim | Verified? | Evidence |
|---|---|---|
| Domain signals `GOOGLE_EXTENDED_OPT_OUT` | **PARTLY TRUE (mis-framed)** | robots.txt is the Cloudflare "content signals" block. It sets `Google-Extended: Disallow` but `User-agent: *` is `Allow: /` and Googlebot is NOT blocked. The report treats a training-opt-out as a crawler-access problem; that is misleading. |
| Faceted nav `?sort= ?brand= ?price=` dilute crawl budget | **NOT VERIFIED** | Generic e-commerce boilerplate. No evidence gathered for this specific catalog. |
| Product pages "require complete Product+Offer JSON-LD (sku, mpn, gtin, price, availability, shippingDetails)" | **PARTLY TRUE** | A real PDP DOES emit Product+Offer JSON-LD with `sku`, `price`, `priceCurrency`, `availability`, `itemCondition`, dimensions/weight. But `mpn`, `gtin` and `brand` are all **absent/null**, and `shippingDetails` is absent. So the recommendation is reasonable, but the report never states what is actually missing. |
| Homepage schema | (not stated) | Homepage graph = Organization, WebSite, WebPage, VideoObject. No sitewide Product schema. |

### My own findings (real)

- Stack: WordPress + WooCommerce (Authorize.net, AvaTax, Mailchimp, product
  filters, Cloudflare Turnstile). Sitemap is segmented into `product-sitemap1..8`
  + `product_cat-sitemap` — actually good crawl hygiene.
- robots.txt: Googlebot/Bingbot allowed; AI-training bots (GPTBot, ClaudeBot,
  Google-Extended, etc.) blocked. This is an intentional policy, not a bug.
- PDP schema gaps (real): missing `brand`, missing `mpn`/`gtin`, missing
  `shippingDetails`; `itemCondition` is `NewCondition` (should be a full URL
  `https://schema.org/NewCondition`).
- Homepage H1 present and keyword-aligned ("Surface Preparation Equipment &
  Parts").

**Verdict: partially useful, largely generic, one misleading framing.**

---

## 2. New Age Behaviour — newagebehaviour.com  ❌ DOMAIN DOES NOT EXIST

### The headline problem

`newagebehaviour.com` returns **NXDOMAIN** from Google DNS and Cloudflare DNS
(status 3 = no such domain), and the Wayback Machine has **no snapshots** ever.
The report claims this domain returned a "PERMISSION_DENIED / 403 firewall
signal". A non-existent domain cannot return a 403. The entire report is written
about a domain that is not registered.

### The site that actually exists

`newagebehavior.com` (US spelling) resolves and serves a live ABA-therapy site:
- Title: "ABA Therapy for Autistic Children in NJ | New Age Behavior"
- Canonical: https://newagebehavior.com/
- robots.txt present and permissive (blocks only wp-admin, search, feeds).
- Schema present: `Organization` + `MedicalOrganization` (a relevant, correct
  type for an ABA clinic).
- H1 present, 0 images missing alt, phone `tel:7323807008`.

So a real, reasonably well-built site exists — the audit just points at the
wrong (non-existent) domain and invented a firewall problem for it.

**Verdict: WRONG. Wrong domain; invented 403. Needs a full re-audit of
newagebehavior.com.**

---

## 3. Revamp Wellness — revampwellness.ca

### Claims vs reality

| Report claim | Verified? | Evidence |
|---|---|---|
| Homepage title targets Langley exclusively | **TRUE** | `<title>Revamp Wellness Langley | RMT, Massage, Physio & Wellness</title>` |
| Homepage H1 is the slogan "Move without limits" | **TRUE** | only H1 = "Move without limits" |
| Full-screen clinic-selector modal on load | **TRUE (detail)** | `#revamp-popup` overlay "Welcome to Revamp Wellness / Please select your nearest clinic" |
| Synchronous Instagram feed causing CLS | **PARTLY TRUE** | an Instagram feed ("new posts loaded") is embedded, but I cannot confirm it is synchronous/CLS-causing from static evidence. |
| Blog articles name practitioners without linking bios | **TRUE** | Blog cards credit "Sabeeh Rehman" / "Jake Baker"; article pages have no author link to `/team/`. |
| Missing dual-entity MedicalClinic JSON-LD | **FALSE / MISLEADING** | Site already emits `MedicalBusiness` JSON-LD for the Langley clinic with correct address, geo, opening hours and phone. It is not "missing" — at most it lacks the second (Cloverdale) entity. |
| Implied phone for Cloverdale `+1-604-372-0050` | **FALSE** | Real Cloverdale phone is `(604)-579-1516`. Langley is `(604) 513-8422` (report's Langley number is right). |
| Implied Cloverdale postal `V3S 1G6` | **FALSE** | Real Cloverdale address is `17392 57 Ave #101, Surrey, BC V3S 2X6`. |
| Implied URLs `/locations/langley/`, `/locations/cloverdale/` | **FALSE** | Both 404. Real pages are `/langley/` and `/cloverdale/` (both 200). |
| ICBC/WSBC pages need FAQ schema | **PLAUSIBLE (not verified)** | No FAQPage schema seen on homepage; ICBC/WSBC pages exist but I did not exhaustively check them. |

### My own findings (real)

- Two clinics: Langley (`8029 199 St Unit 120, Langley Twp, BC V2Y 0E2`,
  `(604) 513-8422`) and Cloverdale (`17392 57 Ave #101, Surrey, BC V3S 2X6`,
  `(604)-579-1516`).
- Good: `MedicalBusiness` schema with geo + opening hours already present;
  images all have alt text; dedicated `/langley/` and `/cloverdale/` pages
  already exist and are indexable.
- Real issues: single-city (Langley) title bias; slogan H1; intrusive
  clinic-selector popup; author bylines not linked to bios; only one of the two
  clinics is marked up as a distinct entity.

**Verdict: MIXED — the on-page findings are broadly right, but the technical
schema/address/URL findings are wrong or invented.**

---

## 4. Tavola Realty — tavolarealty.com

### Claims vs reality

| Report claim | Verified? | Evidence |
|---|---|---|
| 39 Event items on homepage, zero RealEstateAgent | **FALSE** | Raw AND fully rendered (JS + scroll) homepage schema = WebPage, ImageObject, BreadcrumbList, WebSite, Organization. **0 Event, 0 RealEstateAgent.** |
| Homepage title starts with "Home -" | **TRUE** | `<title>Home - Tavola Realty | Chicago Real Estate & Homes for Sale</title>` |
| Broken `href="about:invalid#zCSafez"` phone anchors | **FALSE** | 0 occurrences of `about:invalid` in raw or rendered HTML. Real links are `tel:+13123800636`. |
| Header/footer logo `alt=""` | **TRUE (understated)** | Actually ALL 28 images have empty/missing alt — far worse than "logos". |
| 29 render-blocking stylesheets | **TRUE** | 29 `.css` `<link>`s (34 stylesheet rels) in raw HTML. |
| Nav menu duplicated 3x | **PARTLY** | 2–3 `<nav>` nodes; the 15-agent submenu is repeated in each (mobile + desktop) wrapper. "3 times" is arguable. |
| Neighborhood `/neighbor/*` has no H1 | **TRUE** | `/neighbor/forest-park/` headings: `h3 Explore`, `h2 Forest Park` … no `<h1>`. |
| Market counters static 0 (`0K, 0, $0B, 0+`) | **TRUE** | Rendered "List-to-Sale Price Ratio 0 K / Avg. Days on Market 0 / Total Sales Volume $0 B / Homes Sold 0". |
| Footer omits street address | **FALSE** | Footer already shows "Visit Our Office 939 W North Ave, Suite 750 Chicago, IL 60642". |
| Mobile drawer dead `<a href="#">Join</a>` | **FALSE** | Join links point to `/join-tavola/` and `/join-tavola/#application-form`. |
| Footer YouTube → `@Tavolagroup` | **TRUE** | `youtube.com/@Tavolagroup`. |

### My own findings (real)

- Stack claim is accurate: WordPress + Elementor + Yoast + iHomefinder
  **Kestrel** IDX (Kestrel scripts present). 15 team pages, 13 neighborhood pages.
- Real, verifiable problems: missing `<h1>` on neighborhood templates; static
  zero market counters; 29 stylesheets; all images missing alt; "Home -" title
  prefix.
- The two "Critical" findings (39 Events, `about:invalid` phones) are **not
  real**.

**Verdict: MIXED — several real on-page issues, but the two headline
"Critical" technical findings are fabricated.**

---

## 5. Tavola International — tavola.international

### Claims vs reality

| Report claim | Verified? | Evidence |
|---|---|---|
| Rich Results shows Articles (1) on homepage | **TRUE** | Rendered graph includes an `Article` node ("U.S. Expat Tax Services…") — injected on a commercial homepage. |
| Organization lacks `parentOrganization` to tavola.group | **TRUE** | The `FinancialService/Organization` node is named "Tavola Group" but has **no** `parentOrganization` link. |
| Footer shows PMB `2045 W Grand Ave, Suite B, PMB 28197` | **TRUE** | Footer: "2045 W Grand Ave, Suite B, PMB 28197 Chicago IL 60612-1577". |
| Phone `847-925-1489` shared across domains | **TRUE** | Present in footer; also used on tavolacreative.com. |
| "Insights & Resources — Coming Soon!" placeholder with 5 topics | **PARTLY TRUE** | There IS a "Coming Soon!" block and a numbered list of 5 topics, but the visible section header is "Insights & Resources / Stay informed…", not literally "Insights & Resources — Coming Soon!". |
| Sister domains use Yoast v28.8 while this uses Rank Math | **FALSE** | Tavola Realty uses Yoast; **tavolacreative.com ALSO uses Rank Math**, not Yoast. So the "sister domains use Yoast" premise is wrong. |
| Title/meta "strong and well-calibrated" | **TRUE** | Title and meta description are well-targeted. |
| Homepage E-E-A-T lacks CPA reviewer bylines | **PARTLY** | The Article schema author is a generic "Sabeeh Rehman" with no CPA/EA credential shown. |

### My own findings (real)

- Stack: WordPress + Elementor + **Rank Math** (not Yoast).
- Real issues: Article schema on a service homepage; no `parentOrganization`
  link to tavola.group; PMB/virtual-mailbox address in the footer (a genuine
  local-SEO risk); placeholder "Coming Soon" block.
- The stack-standardization claim is inaccurate.

**Verdict: MOSTLY RIGHT on-page, one wrong technical claim (SEO plugin).**

---

## 6. Tavola Creative — tavolacreative.com

### Claims vs reality

| Report claim | Verified? | Evidence |
|---|---|---|
| 27 external CSS stylesheets | **CLOSE** | 37 `.css` links / 39 stylesheet rels on the homepage (27 on some templates). Directionally right. |
| 5 Google Font families (Roboto, Roboto Slab, Montserrat, Glory, Outfit) | **PARTLY FALSE** | One combined request pulls **Glory, Roboto, Montserrat** only. **Roboto Slab and Outfit are absent** (0 occurrences). |
| Triple-duplicated `<nav>` DOM nodes | **OVERSTATED** | 9 `<nav>` nodes, but these are Elementor's per-widget main/dropdown wrappers (one main + one dropdown per menu instance), not simply "3 copies". |
| Footer Privacy Policy / Terms anchors have no href | **TRUE** | Footer anchors "Privacy Policy" and "Terms and Conditions" render with no `href`. |
| Footer social (Twitter/YouTube) icons lack href | **TRUE** | Footer "Facebook", "Twitter", "Youtube" render as no-href anchors. |
| Phone anchor `about:invalid#zCSafez` | **FALSE** | 0 occurrences. Phone is valid `tel:8479251489`. |
| /blogs/ wraps categories in `<h2>` and repeats the same 5 posts twice → 20 H2s | **PARTLY TRUE** | Blog archive has 21 H2s including category names ("Marketing Strategy", "Case Study", "Uncategorized") AND a duplicated 5-post loop ("Latest Articles" repeats the featured posts). The `<h2>`-for-category claim is true; "20 for five articles" is roughly true. |
| 3 of 5 featured images empty alt; one `alt="WordPress"` | **TRUE** | Blog page has `alt="WordPress"` ×4 and 14 of 30 images missing alt. |
| Static `0` counters on /web-design-services/ (should be 9, 9, 100%) | **TRUE** | Counter widgets render `0`, `0`, and 100% in HTML. |
| Chicago eyebrow typo "Serving Business in chicago" | **TRUE** | Confirmed on the Chicago location page. |
| Kansas City footer anchor reads "Kansas" | **TRUE** | Footer anchor text is "Kansas" for the Kansas City page. |
| Footer mixes 939 W North Ave with PMB 2045 W Grand Ave | **TRUE** | Both addresses appear. |
| Missing dedicated /seo-services/ page | **TRUE** | `/seo-services/` returns 404. |
| "West Peak Collective is now Tavola Creative" banner | **TRUE** | Present. |

### My own findings (real)

- Stack: WordPress + Elementor (+ ElementsKit, Elementor Pro, WP Rocket, Site
  Kit) + **Rank Math** (not Yoast).
- Real issues: no-href footer legal/social links; static zero counters;
  `/blogs/` heading pollution + duplicated post loop; PMB address alongside the
  physical one; lowercase eyebrow typos; missing `/seo-services/`; `alt="WordPress"`.
- The `about:invalid` phone claim and the "5 fonts incl. Roboto Slab & Outfit"
  claim are wrong.

**Verdict: MOSTLY RIGHT (best of the six) but with two wrong specifics.**

---

## Per-site scorecard

| Site | Report accuracy | Key problem |
|---|---|---|
| Buy Manufacturers Direct | ~50% | Generic; AI-opt-out mis-framed as a crawl bug |
| New Age Behaviour | ~0% | **Audited a non-existent domain; invented a 403** |
| Revamp Wellness | ~60% | Right on-page; wrong schema/address/URL specifics |
| Tavola Realty | ~55% | Real on-page issues; **2 "Critical" findings fabricated** |
| Tavola International | ~75% | Mostly right; wrong SEO-plugin claim |
| Tavola Creative | ~80% | Best report; 2 wrong specifics |

## Cross-cutting pattern

- Every report is written in the same confident template and invents specific
  numbers ("39 Events", "403 PERMISSION_DENIED", "27 CSS files", "5 fonts").
- Specific technical numbers are the least reliable part; generic advice is the
  most reliable.
- At least one report audited a domain that does not exist, which is only
  possible if the "audit" was generated from assumptions rather than a live crawl.
