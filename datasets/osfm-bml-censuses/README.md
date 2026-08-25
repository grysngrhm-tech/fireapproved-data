# CAL FIRE OSFM Building Materials Listing — WUI category censuses

Complete public censuses of the CAL FIRE Office of the State Fire Marshal
Building Materials Listing (BML), one census per in-scope category code, from
a frozen snapshot. Every listing in a covered category is present — this is a
census, not a selection of products someone liked.

Each row keeps the OSFM listing ID, the brand, the product name as the listing
records it, the BML application number, and the issue and expiry dates. Where
a listing has no product page on FireApproved.com, the row carries a
`scopeRoute` saying why — most often because the manufacturer's own
instructions limit the product to interior or weather-protected use, which
puts it outside a wildfire-hardening directory. An honest absence is data.

- **Canonical pages:** https://fireapproved.com/data/ (one page per category,
  each with a JSON twin at `/data/{id}.json`)
- **Methodology:** https://fireapproved.com/methodology
- **Records:** 276 listings across 16 category codes.
- **Published copies (v2026.08.25):**
  [Zenodo DOI 10.5281/zenodo.22099756](https://doi.org/10.5281/zenodo.22099756)
  · [Hugging Face](https://huggingface.co/datasets/fireapproved/osfm-bml-censuses)
  · [Kaggle](https://www.kaggle.com/datasets/fireapproved/osfm-bml-censuses)
- **Files here:**
  - `osfm-bml-censuses.csv` — **Start here.** Every row from every category
    flattened into one table, with `categoryCode`, `category` and
    `categoryPage` columns added so the set is usable as a single file.
    Values are otherwise unaltered.
  - `osfm-bml-censuses.jsonl` — one line per category page, each line the
    verbatim JSON twin published on the site.
  - `croissant.json` — Croissant 1.1 metadata (what Hugging Face and Kaggle
    read). Validated with `mlcroissant validate --jsonld`.

## What this is not

- **Not a permit table.** A listing is a model record. Local amendments
  govern, and the authority having jurisdiction decides what is accepted.
- **Not a rating.** FireApproved issues no rating of its own; these rows
  reproduce what the listing body published.
- **Not the whole BML.** The snapshot holds 2,865 listings across 108 category
  codes. Ninety-two of those codes are out of scope for a wildfire
  home-hardening directory by their own official category name — fire alarm
  equipment, suppression systems, interior coatings, locks. Sixteen in-scope
  codes are covered here.

## Fields

| Field | Meaning |
|---|---|
| `categoryCode` | OSFM category code (e.g. `8110` decking) |
| `category` | Official category name |
| `listingId` | OSFM listing number |
| `brand` | Brand slug on FireApproved, or the company as the listing records it |
| `productName` | Product name as the listing records it |
| `productId` | Present when the product has a record on the site |
| `scopeRoute` | Present when it does not — and why |
| `protocol` | Test standard, where the linked record carries one. Absent rather than guessed: the BML snapshot itself records no test standard |
| `application` | Vent placement. Only meaningful in the 8165 vent census |
| `productPage` | The product's record on FireApproved.com, where the listing has earned one |
| `categoryPage` | The census page this row came from |
| `sourceUrl` | The BML search interface |
| `notes` | BML application number, issue date, expiry date, snapshot date |

**Citation:** FireApproved.com (2026). *CAL FIRE OSFM Building Materials
Listing — WUI category censuses* [Data set]. https://fireapproved.com/data/ —
CC BY 4.0.

- **License:** CC BY 4.0 — see the repository [LICENSE](../../LICENSE.md).

The live site is the source of truth. This mirror is rebuilt from the built
site by `scripts/build-data-mirror.mjs` in the fireapproved-com repository,
and each twin carries its own `lastVerified` date.

<!-- about:start -->

## About FireApproved.com

**Every wildfire plant list contradicts the next one, and almost none of them
say why.** One extension bulletin calls a shrub fire-resistant, the next calls
it a hazard, and neither shows its work.

[**FireApproved.com**](https://fireapproved.com) is where you find out what is
actually behind the advice. Look up a plant and you see every source that
rated it, the exact words each one used, when it was published — and where
they disagree, laid side by side instead of averaged into one anonymous
verdict you have to take on faith.

It covers the whole decision, not just the planting list:

- 🌿 **[Plants](https://fireapproved.com/plants/)** — thousands of taxa with
  every cited rating, browsable [by genus](https://fireapproved.com/plants/genus/),
  [by state](https://fireapproved.com/plants/state/) and
  [by USDA zone](https://fireapproved.com/plants/zone/), each tracing to
  [the source that rated it](https://fireapproved.com/plants/source/).
- 🏠 **[Materials](https://fireapproved.com/materials/)** — the vents, siding,
  decking, windows and roofing that are actually listed and tested, with the
  [standards](https://fireapproved.com/standards/) behind them and a
  [lapse log](https://fireapproved.com/materials/lapse-log/) for listings that
  have expired.
- 📍 **[States and requirements](https://fireapproved.com/states/)** — what the
  code adopted where you live [actually says](https://fireapproved.com/requirements/),
  cited to the ordinance rather than to a summary of it.
- 📚 **[Guides](https://fireapproved.com/guides/)** — plain-language answers,
  from [where to start](https://fireapproved.com/guides/hardening-ladder/) to
  [how to read a plant page](https://fireapproved.com/guides/how-to-read-a-plant-page/),
  with a [glossary](https://fireapproved.com/glossary/) for the terms the codes
  use.
- 🔎 **[Findings](https://fireapproved.com/findings/)** — the places where a
  test result or a jurisdiction contradicts what everyone repeats.

**Start here:** [fireapproved.com](https://fireapproved.com) ·
[the plant directory](https://fireapproved.com/plants/) ·
[the materials directory](https://fireapproved.com/materials/) ·
[how this is built](https://fireapproved.com/methodology/)

### Why this data is worth citing

The site issues no rating of its own. Every status is computed from cited
evidence by a published rule, and four properties make that reproducible:

1. **Every verdict keeps the source's own words** — its phrasing, its edition,
   and the date the document was read, not a label invented later.
2. **Classifications are computed, never hand-assigned.** See
   [the methodology](https://fireapproved.com/methodology/).
3. **Evidence deduplicates by lineage, not by row.** A rater who republishes
   the same finding in five places counts once, so a widely-copied opinion
   cannot outvote a laboratory result.
4. **Conflicts are preserved, not averaged.** When sources disagree the record
   says so and shows both sides.

The source registry ships alongside the evidence, so you can recompute or
re-weigh every classification yourself rather than trusting ours.

The live site is the source of truth and is always current. Machine-readable
entry points: [llms.txt](https://fireapproved.com/llms.txt) ·
[llms-full.txt](https://fireapproved.com/llms-full.txt) ·
[every page has a JSON twin](https://fireapproved.com/data/) (the `.json`
replaces the trailing slash).

*FireApproved is a citation directory. It is not a listing body, an insurer,
or a building official — verify at the source before you specify.*

<!-- about:end -->
