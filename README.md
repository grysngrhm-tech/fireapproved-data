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
| [OSFM 8165 ember- and flame-resistant vents census](datasets/osfm-8165-vents/) | 15 listings | https://fireapproved.com/data/osfm-8165-vents/ |
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
