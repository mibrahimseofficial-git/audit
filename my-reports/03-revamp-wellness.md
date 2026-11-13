# Technical & On-Page SEO Audit — Revamp Wellness (corrected)

Audited: 2026-11-13 | Domain: revampwellness.ca | Method: live crawl + render

## 1. Snapshot

- https://revampwellness.ca/ (canonical self-referencing, non-www).
- Two clinics:
  - **Langley**: 8029 199 St Unit 120, Langley Twp, BC V2Y 0E2 — (604) 513-8422
  - **Cloverdale (Surrey)**: 17392 57 Ave #101, Surrey, BC V3S 2X6 — (604)-579-1516
- Category: YMYL multidisciplinary rehab (RMT, physio, chiro, kinesiology,
  acupuncture, ICBC/WorkSafeBC active rehab).

## 2. What the site already does well

- `MedicalBusiness` JSON-LD is already present for the **Langley** clinic with
  correct address, geo coordinates, telephone and opening-hours specification.
- A second `Organization` node with social `sameAs` links exists.
- Dedicated, indexable location pages already exist: `/langley/` and
  `/cloverdale/` (both return 200).
- All images on the homepage have alt text (0 missing).
- robots.txt is clean and permissive, and references `sitemap_index.xml`.

## 3. Verified issues (real)

1. **Single-city title bias.** Homepage title =
   "Revamp Wellness Langley | RMT, Massage, Physio & Wellness". Cloverdale/Surrey
   is invisible in the title. Fix: "Revamp Wellness | RMT, Physio & Chiro in
   Langley & Cloverdale".
2. **Slogan H1.** The only H1 is "Move without limits" — no treatment or
   geography keywords. Fix: "Multidisciplinary Physiotherapy, RMT & Chiropractic
   Clinic in Langley & Cloverdale", keeping the tagline as a subheading.
3. **Intrusive clinic-selector popup.** A full-screen overlay
   (`#revamp-popup`, "Welcome to Revamp Wellness / Please select your nearest
   clinic") fires on load. On mobile this risks the intrusive-interstitial
   penalty. Fix: replace with a dismissible sticky bar.
4. **Blog bylines not linked to bios.** Blog cards credit clinicians
   ("Sabeeh Rehman", "Jake Baker"); article pages carry no author link to a
   credentialed bio. A `/team/` page exists (200) — link to it.
5. **Only one of two clinics is marked up.** Add a second entity for Cloverdale
   (correct address/phone above) via a JSON-LD `@graph`.

## 4. Corrections to the supplied report

- The supplied report's Cloverdale phone `+1-604-372-0050` is **wrong**; the real
  number is **+1-604-579-1516**.
- Its Cloverdale postal code `V3S 1G6` is **wrong**; the real one is
  **V3S 2X6**.
- Its assumed URLs `/locations/langley/` and `/locations/cloverdale/` **404**;
  the real pages are `/langley/` and `/cloverdale/`.
- It claims dual-entity MedicalClinic schema is "lacking" — in fact a single
  MedicalBusiness entity already exists; only the second clinic is missing.

## 5. Recommended JSON-LD (corrected)

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "MedicalClinic",
      "@id": "https://revampwellness.ca/#langley",
      "name": "Revamp Wellness – Langley",
      "url": "https://revampwellness.ca/langley/",
      "telephone": "+1-604-513-8422",
      "address": {
        "@type": "PostalAddress",
        "streetAddress": "8029 199 St Unit 120",
        "addressLocality": "Langley",
        "addressRegion": "BC",
        "postalCode": "V2Y 0E2",
        "addressCountry": "CA"
      },
      "medicalSpecialty": ["Physiotherapy", "Chiropractic", "MassageTherapy"],
      "priceRange": "$$"
    },
    {
      "@type": "MedicalClinic",
      "@id": "https://revampwellness.ca/#cloverdale",
      "name": "Revamp Wellness – Cloverdale",
      "url": "https://revampwellness.ca/cloverdale/",
      "telephone": "+1-604-579-1516",
      "address": {
        "@type": "PostalAddress",
        "streetAddress": "17392 57 Ave #101",
        "addressLocality": "Surrey",
        "addressRegion": "BC",
        "postalCode": "V3S 2X6",
        "addressCountry": "CA"
      },
      "medicalSpecialty": ["Physiotherapy", "Chiropractic", "MassageTherapy"],
      "priceRange": "$$"
    }
  ]
}
```

## 6. Priority actions

1. Update homepage title + H1 to cover Langley AND Cloverdale.
2. Add the second (Cloverdale) MedicalClinic entity with correct address/phone.
3. Replace the on-load popup with a dismissible sticky selector.
4. Link blog author bylines to credentialed `/team/` bios.
5. Add FAQPage schema to ICBC and WorkSafeBC pages.
