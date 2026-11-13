# Independent verification of the 6 SEO audit PDFs

## What was asked

Pull all files from https://github.com/mibrahimseofficial-git/audit, audit every
site myself, and say whether the supplied audit reports are correct. If not,
produce my own reports.

## What I did

1. Cloned the repo (6 PDFs, one per site) and extracted the text.
2. Audited each live site independently on **2026-11-13** using:
   - `curl` for robots.txt, sitemaps, and raw HTML,
   - headless Chromium (Playwright) to render JS-heavy pages and read the
     **rendered** DOM + JSON-LD (this is what Google Rich Results sees),
   - DNS lookups (Google + Cloudflare resolvers) and the Wayback Machine.
3. Compared every claim to the evidence.

## The verdict

**No — the reports are not reliable.** They read like machine-generated
templates. The generic advice is mostly fine, but the specific technical
"findings" are frequently wrong or invented. Highlights:

- **New Age Behaviour report audited a domain that does not exist.**
  `newagebehaviour.com` is NXDOMAIN (never archived). The real site is
  `newagebehavior.com`. A non-existent domain cannot return the "403
  PERMISSION_DENIED" the report describes.
- **Tavola Realty's two "Critical" findings are fabricated.** There is **no**
  Event schema (the report claims 39) and **no** `about:invalid#zCSafez`
  phone links (the report claims them). Both verified 0 on raw and rendered
  HTML.
- **Tavola Creative:** the "5 fonts incl. Roboto Slab & Outfit" and
  `about:invalid` phone claims are false (fonts are Glory/Roboto/Montserrat;
  phone is a valid `tel:`).
- **Revamp Wellness:** Cloverdale phone, postal code and location URLs in the
  report are all wrong.
- **Tavola International:** the "sister domains use Yoast" premise is wrong —
  tavolacreative.com also uses Rank Math.
- **Buy Manufacturers Direct:** the AI-training opt-out is misframed as a
  crawl-access bug (Googlebot is allowed).

## Accuracy scorecard

| Site | Report accuracy | Headline problem |
|---|---|---|
| Buy Manufacturers Direct | ~50% | Misframed non-issue; generic |
| New Age Behaviour | ~0% | **Audited a non-existent domain** |
| Revamp Wellness | ~60% | Wrong schema/address/URL specifics |
| Tavola Realty | ~55% | **2 "Critical" findings fabricated** |
| Tavola International | ~75% | Wrong SEO-plugin claim |
| Tavola Creative | ~80% | 2 wrong specifics |

Full comparison: see `../VERIFICATION.md`.

## My own reports (one per site)

- `01-buy-manufacturers-direct.md`
- `02-new-age-behavior.md`  (corrected domain)
- `03-revamp-wellness.md`
- `04-tavola-realty.md`
- `05-tavola-international.md`
- `06-tavola-creative.md`

Each lists what is actually true, what is wrong in the original, and a
prioritised action list backed by live evidence.
