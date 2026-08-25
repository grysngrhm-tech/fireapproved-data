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

| Dataset | Records | Canonical page | Published copies |
|---|---|---|---|
| [ORSC R327 local adoption](datasets/r327-adoption/) | 5 municipalities | https://fireapproved.com/data/r327-adoption/ | not minted standalone |
| [OSFM BML WUI category censuses](datasets/osfm-bml-censuses/) | 276 listings across 16 categories | https://fireapproved.com/data/ | [Zenodo](https://doi.org/10.5281/zenodo.22099756) · [Hugging Face](https://huggingface.co/datasets/fireapproved/osfm-bml-censuses) · [Kaggle](https://www.kaggle.com/datasets/fireapproved/osfm-bml-censuses) |
| [Plants evidence directory](datasets/plants-evidence/) | 3,801 plant records | https://fireapproved.com/plants/ (one JSON twin per plant) | [Zenodo](https://doi.org/10.5281/zenodo.22099746) · [Hugging Face](https://huggingface.co/datasets/fireapproved/plants-evidence) · [Kaggle](https://www.kaggle.com/datasets/fireapproved/plants-evidence) |

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
