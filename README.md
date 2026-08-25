# FireApproved data — CC BY 4.0 mirrors

Structured datasets from **[FireApproved.com](https://fireapproved.com)**, a
citation directory for wildfire-resistant construction and plants. The site
issues no ratings of its own — every status and claim links to the source
document it came from.

**The live site is the source of truth.** This repository mirrors the JSON
published there so the data is easy to find, cite, and load. When this mirror
and the site disagree, the site wins. Canonical URLs are listed in each
dataset's README.

## Datasets

| Dataset | Records | Canonical page |
|---|---|---|
| [ORSC R327 local adoption](datasets/r327-adoption/) | 5 municipalities | https://fireapproved.com/data/r327-adoption/ |
| [OSFM BML WUI category censuses](datasets/osfm-bml-censuses/) | 276 listings across 16 categories | https://fireapproved.com/data/ |
| [Plants evidence directory](datasets/plants-evidence/) | 3,801 plant records | https://fireapproved.com/plants/ (one JSON twin per plant) |

## How the data is built

Statuses are computed from evidence rows, never hand-assigned. Sources are
tiered (lab-tested, field-trial, post-fire-survey, and extension/agency lists
with stated method count as primary; compilations corroborate but are not
evidence), and conflicts stay visible rather than being averaged. Method:
https://fireapproved.com/methodology

## License

Creative Commons Attribution 4.0 International (CC BY 4.0) — see
[LICENSE](LICENSE.md). Give credit to FireApproved.com, link the license, and
indicate changes. Each dataset README carries a ready-made citation line.

Plant photo fields in the plants dataset are metadata only (attribution and
source URLs); the images themselves are not included here and are not CC BY.

<!-- about:start -->

## About FireApproved.com

[FireApproved.com](https://fireapproved.com) is a citation directory for
wildfire-resistant construction and plants. Every status, rating and
requirement on the site links to the source document it came from, and the
site issues no rating of its own — the evidence is the product.

Four things make this data unusual enough to cite:

1. **Every verdict keeps the source's own words.** Each evidence row carries
   the source's phrasing of its finding, the edition it appeared in, and the
   date the document was read — not a normalised label invented later.
2. **Classifications are computed, never hand-assigned.** A published rule
   turns evidence rows into a class. See
   [the methodology](https://fireapproved.com/methodology/).
3. **Evidence is deduplicated by lineage, not by row.** A rater who publishes
   the same finding in five places counts once, so a widely-republished
   opinion cannot outvote a laboratory result.
4. **Conflicts are preserved, not averaged.** When sources disagree, the
   record says so and shows both sides rather than emitting a tidy score.

### Where this data comes from

- [Plants](https://fireapproved.com/plants/) — the plant directory, one page
  per taxon, grouped by [genus](https://fireapproved.com/plants/genus/), with
  every [cited source](https://fireapproved.com/plants/source/) listed.
- [Materials](https://fireapproved.com/materials/) — listed and tested
  home-hardening products, with the
  [standards](https://fireapproved.com/standards/) they were tested to.
- [Datasets](https://fireapproved.com/data/) — the census pages these files
  mirror, each with a JSON twin.
- [Requirements](https://fireapproved.com/requirements/) and
  [states](https://fireapproved.com/states/) — what the adopted code actually
  says, per place.
- [Guides](https://fireapproved.com/guides/) and
  [glossary](https://fireapproved.com/glossary/) — how to read a plant page,
  what limited evidence means, and the terms used here.
- [Findings](https://fireapproved.com/findings/) — where a jurisdiction or
  test result contradicts a common assumption.

The live site is the source of truth. Machine-readable entry points:
[llms.txt](https://fireapproved.com/llms.txt) and
[llms-full.txt](https://fireapproved.com/llms-full.txt).

<!-- about:end -->
