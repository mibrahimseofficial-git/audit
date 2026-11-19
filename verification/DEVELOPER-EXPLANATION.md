# Outstanding SEO Items — Detailed Explanation for the Developer

Verified live: 2026-11-18 (cache-busted). Every item below includes the exact
evidence found on the live site and a concrete fix.

---

# TAVOLA CREATIVE — 5 items NOT fixed + 2 partial

## ❌ 1. H1 headings — the task you marked "Completed" is NOT done

**What's wrong**
Two pages still fail the H1 task:

- `/web-design-services/` — the H1 is the lowercase fragment **"web design"**.
  It is not a real heading; it is not descriptive and it doesn't target the
  service.
- `/home-new-v/` — the page has **zero `<h1>` elements** at all.

**Evidence (live HTML)**
```html
<!-- https://www.tavolacreative.com/web-design-services/ -->
<h1 class="elementor-heading-title elementor-size-default">web design </h1>
```
```
https://www.tavolacreative.com/home-new-v/
  H1 count = 0
  title    = "Home new v - Tavola Creative"
```

**Why it matters**
Every indexable page should have exactly one descriptive H1. `/home-new-v/`
looks like a stray/duplicate homepage variant — it has no H1, a junk title
("Home new v"), and it is listed in the sitemap, so it competes with the real
homepage. `/web-design-services/` loses its strongest on-page keyword signal.

**Fix**
- `/web-design-services/`: change the H1 text to something like
  "Website Design Services for Growing Brands".
- `/home-new-v/`: either add a proper H1, or (better) **noindex or redirect**
  this stray page to `/`.

---

## ❌ 2. `/blogs/` heading structure — category labels still wrapped in `<h2>`

**What's wrong**
The blog archive still uses `<h2>` for **category badges**, not just article
titles. There are **21 `<h2>` elements and 0 `<h3>`**. Category names
("Marketing Strategy", "Case Study", "Uncategorized") are marked up as
headings.

**Evidence (live HTML)**
```
<h1> Blogs - Tavola Creative
<h2> Why Website Maintenance Matters for Small Businesses
<h2> Marketing Strategy      <-- category badge used as a heading
<h2> What Is Brand Visibility and How Can a Business Improve It?
<h2> Case Study              <-- category badge
<h2> Growing Wellness Brands on Instagram
<h2> Marketing Strategy
...
<h2> Uncategorized           <-- category badge
```
(Tag-level check: `<h2>` = 21, `<h3>` = 0.)

**Why it matters**
Category labels are not page sections — marking them as `<h2>` pollutes the
document outline and makes it ambiguous which text is the real article title.
"Uncategorized" also leaks an unmanaged taxonomy into the headings.

**Fix**
- Category badges: change `<h2>` → `<span>` (they are labels, not headings).
- Article titles: keep one heading level (e.g. `<h3>`).
- Replace the "Uncategorized" taxonomy with a real category.

---

## ❌ 3. `/blogs/` duplicated 5-post loop

**What's wrong**
The same five articles are output **twice** on `/blogs/` — once in the featured
grid and again in the "Latest Articles" grid.

**Evidence (live HTML — each article link appears 2×)**
```
2x  /website-maintenance-for-small-businesses/
2x  /what-is-brand-visibility-and-how-can-a-business-improve-it/
2x  /growing-wellness-brands-on-instagram/
2x  /is-a-social-media-marketing-agency-worth-it/
2x  /how-to-choose-a-digital-marketing-agency/
```
The "Latest Articles" `<h2>` is immediately followed by the same five titles
already shown above it.

**Why it matters**
Duplicate content on the same page, wasted crawl budget, and a confusing user
experience (the same posts back-to-back). It also doubles the heading count.

**Fix**
Exclude the featured posts from the "Latest Articles" query, or remove the
duplicate grid entirely.

---

## ❌ 4. PMB / virtual-mailbox address still in the footer

**What's wrong**
The footer still prints a **Private Mailbox (PMB)** mailing address in addition
to the physical office.

**Evidence (live HTML)**
```html
<span class="elementor-icon-list-text"> Mailing Address: 2045 W Grand Ave,
Suite B, PMB 28197, Chicago, IL 60612-1577</span>
```

**Why it matters**
Google's local guidelines discourage virtual mailboxes/PMBs on public pages.
Publishing two Chicago addresses (the physical 939 W North Ave office **and**
this PMB) fragments the local entity signal and can weaken local-pack
visibility.

**Fix**
Remove the "Mailing Address … PMB 28197" line from all public templates so the
verified physical address (939 W North Ave, Suite 750, Chicago, IL 60642) is
the only one indexed.

---

## ❌ 5. Missing `/seo-services/` page + still-heavy CSS

**What's wrong (two things)**

**(a) `/seo-services/` does not exist.**
```
GET https://www.tavolacreative.com/seo-services/  →  HTTP 404
```
The site promotes SEO as a service (homepage and `/web-design-services/`), and
there are SEO blog articles, but there is no dedicated SEO service page to
capture high-intent searches or serve as an internal-linking target.

**(b) 37 render-blocking stylesheets** are still loaded on the homepage:
```
TC home <link ... .css> count = 37
```
Each separate CSS file blocks first paint and hurts mobile LCP/TBT.

**Fix**
- Publish a `/seo-services/` pillar page (title, H1, meta description, service
  copy, internal links from the SEO blog posts).
- Consolidate/minify CSS (Elementor "Improved CSS Loading" / WP Rocket
  "Optimize CSS delivery") to cut the 37 files down.

---

## ⚠️ PARTIAL — footer "Kansas" anchor + Kansas City eyebrow

**What's wrong**
Two Kansas City labels are still wrong:

- The **footer/nav anchor** text is still **"Kansas"** (the state), not
  "Kansas City".
- The **eyebrow** on the Kansas City page reads **"Serving Businesses in
  Kansas"** (state, not city).

**Evidence (live HTML)**
```html
<a href=".../digital-marketing-agency-kansas-city/" class="elementor-item">Kansas</a>
```
```
KC eyebrow: "Serving Businesses in Kansas"
```

**Note:** the Chicago side is now fixed ("Serving Businesses in Chicago") — good.
The Kansas City page just needs the same treatment.

**Fix**
- Anchor text: "Kansas" → "Kansas City".
- Eyebrow: "Serving Businesses in Kansas" → "Serving Businesses in Kansas City".

---

# TAVOLA INTERNATIONAL — 4 items NOT fixed

## ❌ 1. `Article` schema still on the service homepage

**What's wrong**
The homepage JSON-LD still contains an `Article` node, even though this is a
commercial service homepage (not a blog post).

**Evidence (live JSON-LD)**
```json
{
  "@type": "Article",
  "headline": "U.S. Expat Tax Services for Americans Abroad | Tavola International",
  "datePublished": "2026-06-15T14:35:08-05:00",
  "dateModified": "2026-11-17T13:55:22-06:00",
  "author": { "@id": "https://www.tavola.international/#author", "name": "Sabeeh Rehman" },
  "publisher": { "@id": "https://www.tavola.international/#organization" }
}
```

**Why it matters**
Emitting `Article` on a service homepage sends mixed page-type signals to
Google and Rich Results — the page is treated partly as a news article, with a
generic "Sabeeh Rehman" author and no CPA/EA credential (a YMYL trust issue for
a tax site).

**Fix**
Disable `Article` schema on the homepage template; keep the primary type as
`AccountingService` (or `ProfessionalService`) and reserve `Article` for actual
blog posts.

---

## ❌ 2. No `parentOrganization` link to `tavola.group`

**What's wrong**
The Organization node is named "Tavola Group" but is **not connected** to the
group domain — there is no `parentOrganization` reference.

**Evidence (live JSON-LD)**
```json
{
  "@type": ["FinancialService", "Organization"],
  "@id": "https://www.tavola.international/#organization",
  "name": "Tavola Group",
  "url": "https://www.tavola.international",
  "sameAs": [ ... ]
}
```
```
'parentOrganization' present: False
```

**Why it matters**
Search engines can't tell that tavola.international is part of the Tavola Group
brand entity. Linking the parent consolidates brand/knowledge-graph signals
across tavola.group and the sister sites.

**Fix**
Add:
```json
"parentOrganization": {
  "@type": "Organization",
  "@id": "https://tavola.group/#organization",
  "name": "Tavola Group",
  "url": "https://tavola.group/"
}
```

---

## ❌ 3. PMB address still in the Tavola International footer

**What's wrong**
Same issue as Tavola Creative — the footer prints the virtual mailbox address.

**Evidence (live HTML)**
```html
<span class="elementor-icon-list-text">2045 W Grand Ave, Suite B, PMB 28197
```

**Why it matters**
A PMB on a YMYL financial/tax site weakens local-entity trust and contradicts
the physical HQ address.

**Fix**
Replace with the physical HQ (939 W North Ave, Suite 750, Chicago, IL 60642),
or explicitly frame the site as a service-area business and remove the PMB.

---

## ❌ 4. "Coming Soon!" placeholder still live

**What's wrong**
The "Insights & Resources" section still shows a **"Coming Soon!"** placeholder
with a numbered list of topics instead of real content.

**Evidence (live HTML)**
```
"> Coming Soon! Have a topic you want us to cover? Send your suggestion."
```

**Why it matters**
An empty "Coming Soon" block on a YMYL site gives no E-E-A-T value and reads as
unfinished. It occupies prime homepage real estate that could carry authority
content.

**Fix**
Publish the listed topics as real pillar pages (with `FAQPage` schema and
credentialed CPA/EA reviewer bylines), or replace the placeholder with links to
existing resources.

---

## ✅ Bonus — what IS now correct on Tavola International (alt text)

Most content images now have descriptive alt text:
```
alt='Tavola International logo' | Group-3624-1024x116.png
alt='Riga skyline with historic buildings along the river' | European-city-1-1024x683.webp
alt='Tax professional preparing a U.S. tax return' | service-tax-...webp
alt='a happy family walking on beach' | Global-Concierge-...png
```
**Still empty (2 real ones):** `Artboard-3-copy-6-1.webp` and one SVG
placeholder (plus 2 tracking pixels, which are harmless).

---

# Summary table

| Site | Item | Status |
|---|---|---|
| Creative | H1s (`/web-design-services/`, `/home-new-v/`) | ❌ Not fixed |
| Creative | `/blogs/` category `<h2>`s | ❌ Not fixed |
| Creative | `/blogs/` duplicate 5-post loop | ❌ Not fixed |
| Creative | PMB address in footer | ❌ Not fixed |
| Creative | `/seo-services/` 404 + 37 CSS files | ❌ Not fixed |
| Creative | Footer "Kansas" anchor + KC eyebrow | ⚠️ Partial |
| International | `Article` schema on homepage | ❌ Not fixed |
| International | `parentOrganization` → tavola.group | ❌ Not fixed |
| International | PMB address in footer | ❌ Not fixed |
| International | "Coming Soon!" placeholder | ❌ Not fixed |
| International | Image alt text | ✅ Done (2 images remain) |
| Creative | Image alt text | ✅ Done |
| Creative | Meta descriptions | ✅ Done (but duplicated) |
