# Changelog

Snapshots of the structured data published by
[FireApproved.com](https://fireapproved.com). The live site is always the
source of truth; each entry here says what changed in the mirror.

Versions are dated snapshots (`YYYY.MM.DD`), matching `version` in
`datapackage.json` and `dataset.jsonld`.

## 2026.08.25 (published copies)

The two submitable datasets now have live registry records. The GitHub
release tag `v2026.08.25` remains the version pin; these URLs cite that
snapshot. `r327-adoption` is not minted standalone. Zenodo's
GitHub-release webhook was not enabled (that would have been a third
overlapping DOI).

- Plants: [10.5281/zenodo.22099746](https://doi.org/10.5281/zenodo.22099746)
  · [huggingface.co/datasets/fireapproved/plants-evidence](https://huggingface.co/datasets/fireapproved/plants-evidence)
  · [kaggle.com/datasets/fireapproved/plants-evidence](https://www.kaggle.com/datasets/fireapproved/plants-evidence)
- OSFM BML censuses:
  [10.5281/zenodo.22099756](https://doi.org/10.5281/zenodo.22099756)
  · [huggingface.co/datasets/fireapproved/osfm-bml-censuses](https://huggingface.co/datasets/fireapproved/osfm-bml-censuses)
  · [kaggle.com/datasets/fireapproved/osfm-bml-censuses](https://www.kaggle.com/datasets/fireapproved/osfm-bml-censuses)

## 2026.08.25

**The export became reproducible.** Previously the evidence rows attributed
every verdict to a source slug — `bardon-2005`, `apsvic` — and the mirror
shipped nothing explaining what those were. Since a classification is computed
from each source's `tier`, `evidenceKind` and `lineage`, none of which were
included, the README's claim that you could "recompute or re-weigh it
yourself" was not actually keepable. The source registry now ships, and it is.

Added:

- `datasets/plants-evidence/plant-sources.csv` and `.json` — all 112
  registered sources with publisher, region, tier, evidence kind, lineage,
  editions and scale notes. Join on `source`.
- `datasets/plants-evidence/plants-evidence.csv` — 26,878 evidence rows
  flattened into one loadable table, each carrying the plant's canonical URL.
  The `.jsonl` stays as the lossless twin.
- `datasets/osfm-bml-censuses/` — 276 OSFM Building Materials Listing entries
  across 16 category codes. The mirror previously carried only the 15-row 8165
  vent census, one of sixteen, so the materials half was effectively
  unpublished.
- `datapackage.json` (Frictionless) and `dataset.jsonld` (schema.org
  `DataCatalog`, which is what Google Dataset Search reads).
- `datasets/plants-evidence/croissant.json` and
  `datasets/osfm-bml-censuses/croissant.json` — Croissant 1.1, generated
  from `scripts/build-data-mirror.mjs` and validated with `mlcroissant
  validate --jsonld` (exit 0). Hugging Face and Kaggle read this format.
  `r327-adoption` has none; it is too thin for a standalone dataset page.
- `LICENSE` — the CC BY 4.0 legal code, fetched from
  creativecommons.org, so GitHub can detect the licence. `LICENSE.md`
  remains the human summary.
- Dataset README file tables now list `croissant.json`. `CITATION.cff`
  lead author is FireApproved.com (Grayson Graham remains as the person).
- A documented column reference for every field, including the two distinct
  meanings of `original`.

Changed:

- Plant records 2,123 → 3,801; evidence rows 5,008 → 26,878.
- The mirror is now rebuilt from the built site by
  `scripts/build-data-mirror.mjs` in the fireapproved-com repository, rather
  than assembled by hand.

Removed:

- `datasets/osfm-8165-vents/` — superseded by `osfm-bml-censuses`, which
  contains it. Nothing external referenced it.

## 2026.08.24

Initial mirror: `r327-adoption`, `osfm-8165-vents`, `plants-evidence`
(2,123 records / 5,008 evidence rows), CC BY 4.0.
