# Technical & On-Page SEO Audit — Buy Manufacturers Direct (corrected)

Audited: 2026-11-13 | Domain: buymanufacturersdirect.com | Method: live crawl +
render + a real product-page (PDP) fetch

## 1. Snapshot

- https://buymanufacturersdirect.com/ (canonical self-referencing, non-www).
- Stack (confirmed): WordPress + **WooCommerce** (Authorize.net CIM gateway,
  AvaTax, Mailchimp for WooCommerce, product filters, Cloudflare Turnstile,
  hide-price, GTM Kit).
- Category: B2B/B2C direct-from-manufacturer industrial / surface-preparation
  equipment (shot blasters, floor grinders, scarifiers).
- Homepage H1: "Surface Preparation Equipment & Parts" — keyword-aligned.

## 2. Crawlability (verified)

- robots.txt is the Cloudflare "content signals" template:
  - `User-agent: *` → `Allow: /` with `Content-Signal: search=yes, ai-train=no`.
  - Training/AI crawlers (GPTBot, ClaudeBot, CCBot, Bytespider,
    Applebot-Extended, Google-Extended, etc.) → `Disallow: /`.
- **Important framing correction:** the supplied report calls the
  `Google-Extended` opt-out a "Critical" crawler-restriction problem. That is
  misleading. `Google-Extended` controls only Gemini/AI *training*, **not**
  Google Search. Googlebot is **not** blocked (`User-agent: * Allow: /`). This
  is a deliberate AI-training policy, not a crawl-access bug.
- Sitemap hygiene is actually good: `sitemap_index.xml` fans out into
  `product-sitemap1..8.xml`, `product_cat-sitemap.xml`, `page-sitemap.xml`,
  `post-sitemap.xml`, `location-sitemap.xml`, `video-library-sitemap.xml`.

## 3. Product structured data (verified on a real PDP)

Fetched a real product
(`/shop/manufacturers/general-equipment-company/attachment-clamp-13-5d/`).
It emits a `Product` + `Offer` JSON-LD block containing:
- `name`, `description`, `sku` ("810045170176"), `category`, dimensions
  (weight/height/width/depth), `image`, and an `offers` object with `price`
  (2025.00), `priceCurrency` (USD), `priceValidUntil`, `availability`
  (InStock), and a `seller`.

**Real gaps in the Product schema:**
- `brand` → **absent**
- `mpn` → **absent**
- `gtin` / `gtin13` → **absent**
- `shippingDetails` → **absent**
- `itemCondition` is `NewCondition` (should be the full URL
  `https://schema.org/NewCondition`).

So the report's recommendation ("add mpn/gtin/brand/shippingDetails") is
reasonable — but the report never states which fields are actually missing, and
it frames the whole audit around a non-issue (the AI-training opt-out).

## 4. Corrections to the supplied report

- **"Critical: domain signals Google-Extended opt-out → verify Googlebot
  access."** Misframed. Googlebot is allowed; the opt-out only affects Gemini
  training. Not a crawl-budget emergency.
- **"Faceted `?sort= ?brand= ?price=` duplicate URLs dilute crawl budget."**
  Generic e-commerce boilerplate; not evidenced for this catalog.
- **"Product pages require complete Product+Offer JSON-LD (sku, mpn, gtin,
  price, availability, shippingDetails)."** Partially valid: the page already
  has Product+Offer with sku/price/availability; what is genuinely missing is
  brand/mpn/gtin/shippingDetails.

## 5. Priority actions

1. Enrich the `Product` JSON-LD: add `brand`, `mpn`/`gtin`, and
   `shippingDetails`; change `itemCondition` to the full
   `https://schema.org/NewCondition` URL.
2. Keep the AI-training opt-out only if intentional (it is harmless to Search).
3. Add buying-guide copy below top category grids to capture head terms.
4. Ensure discontinued SKUs 301 to replacement SKUs or the parent category
   rather than 404ing.
5. Standardise canonical handling for filtered/sorted category URLs.
