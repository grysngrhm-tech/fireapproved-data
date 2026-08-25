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
- **Files here:**
  - `osfm-bml-censuses.jsonl` — one line per category page, each line the
    verbatim JSON twin published on the site.
  - `osfm-bml-censuses.csv` — every row from every category flattened into one
    table, with `categoryCode`, `category` and `categoryPage` columns added so
    the set is usable as a single file. Values are otherwise unaltered.

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
| `sourceUrl` | The BML search interface |
| `notes` | BML application number, issue date, expiry date, snapshot date |

**Citation:** FireApproved.com (2026). *CAL FIRE OSFM Building Materials
Listing — WUI category censuses* [Data set]. https://fireapproved.com/data/ —
CC BY 4.0.

- **License:** CC BY 4.0 — see the repository [LICENSE](../../LICENSE.md).

The live site is the source of truth. This mirror is rebuilt from the built
site by `scripts/build-data-mirror.mjs` in the fireapproved-com repository,
and each twin carries its own `lastVerified` date.
