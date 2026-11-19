# Technical & On-Page SEO Audit — Tavola International (corrected)

Audited: 2026-11-13 | Domain: tavola.international | Method: live crawl + render

## 1. Snapshot

- https://www.tavola.international/ (canonical self-referencing, www).
- Stack (confirmed): WordPress + Elementor + **Rank Math SEO** (confirmed via
  `rank-math-schema`). Not Yoast.
- Category: YMYL cross-border / expat U.S. tax and advisory.
- Title: "U.S. Expat Tax Services for Americans Abroad | Tavola International"
  — well-targeted. Meta description also good.

## 2. Verified issues (real)

1. **Article schema on a service homepage.** The rendered graph contains an
   `Article` node ("U.S. Expat Tax Services…") plus a generic `Person` author
   ("Sabeeh Rehman"). Emitting Article on a commercial homepage sends mixed
   page-type signals. Disable Article schema on the homepage template.
2. **Organization not linked to the parent.** The `FinancialService` +
   `Organization` node is named "Tavola Group" but carries **no
   `parentOrganization`** reference, and the site's own brand entity is not
   cleanly connected to `tavola.group`. Add the parent link.
3. **Virtual mailbox (PMB) in the footer.** Footer shows
   "2045 W Grand Ave, Suite B, PMB 28197, Chicago IL 60612-1577" and phone
   `847-925-1489` (shared with tavolacreative.com). PMBs are discouraged in
   LocalBusiness signals. Prefer the physical HQ address (939 W North Ave,
   Suite 750, Chicago, IL 60642) or frame the page as a service-area business.
4. **"Coming Soon!" placeholder.** The homepage has an "Insights & Resources"
   section whose live state is a "Coming Soon!" block with a numbered list of 5
   topics (U.S. tax filing abroad; FBAR/FATCA; foreign income exclusions &
   credits; moving abroad/returning; …). Replace with real published pillar
   content.
5. **Homepage images missing alt.** 12 of 23 images lack alt text.

## 3. Corrections to the supplied report

- The report claims sister Tavola domains use **Yoast SEO v28.8** and that only
  Tavola International uses Rank Math. FALSE for the comparison drawn:
  **tavolacreative.com also uses Rank Math.** (Tavola Realty does use Yoast.)
  The "ecosystem standardization" premise is therefore inaccurate.
- The report's "5 non-clickable tax topics" description is essentially right,
  but the on-page header reads "Insights & Resources / Stay informed…", not
  literally "Insights & Resources — Coming Soon!".

## 4. Recommended JSON-LD

```json
{
  "@context": "https://schema.org",
  "@type": "AccountingService",
  "@id": "https://www.tavola.international/#organization",
  "name": "Tavola International",
  "url": "https://www.tavola.international/",
  "telephone": "+1-847-925-1489",
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
  "areaServed": { "@type": "Place", "name": "Worldwide" },
  "knowsAbout": [
    "U.S. Expat Tax Preparation",
    "FBAR and FATCA Compliance",
    "Foreign Earned Income Exclusion",
    "Cross-Border Tax Planning",
    "Streamlined Filing Compliance Procedures"
  ]
}
```

## 5. Priority actions

1. Remove Article schema from the homepage; set primary type to
   `AccountingService`.
2. Add `parentOrganization` → tavola.group.
3. Replace the PMB footer address with the physical HQ (or frame as
   service-area).
4. Publish the placeholder "Coming Soon" topics as real pillar pages with
   FAQPage schema and credentialed (CPA/EA) reviewer bylines.
5. Add alt text to the 12 images missing it.
