# Plant flammability evidence directory

The full FireApproved plant directory as machine-readable evidence records:
3,801 plants carrying 27,007 flammability evidence rows, plus the source
registry those rows are attributed to.

FireApproved issues no ratings of its own. Each plant's classification is
computed from the evidence rows by a published method — majority direction by
independent source lineage; direct fire evidence is never silently outvoted by
curation; conflicts stay visible. **This export carries the evidence and the
registry, so you can recompute or re-weigh it yourself.**

- **Canonical pages:** https://fireapproved.com/plants/ — every plant has a
  JSON twin where the `.json` replaces the page's trailing slash, so
  `/plants/{id}/` is served as JSON at `/plants/{id}.json`.
- **Methodology:** https://fireapproved.com/methodology/
- **Records:** 3,801 plants carrying 26,878 flammability evidence rows, and
  112 registered sources.
- **Coverage:** source documents dated 1968 through 2026-08-25
  (23,103 of 26,878 rows carry a document date). 112 sources in the
  United States, Europe, the Mediterranean, Australia, New Zealand,
  South America, and other named regions. Not a global flora census.
- **Published copies (v2026.08.25):**
  [Zenodo DOI 10.5281/zenodo.22099746](https://doi.org/10.5281/zenodo.22099746)
  · [Hugging Face](https://huggingface.co/datasets/fireapproved/plants-evidence)
  · [Kaggle](https://www.kaggle.com/datasets/fireapproved/plants-evidence)
  · [Wikidata Q141177673](https://www.wikidata.org/wiki/Q141177673)

## Files

| File | What it is |
|---|---|
| `plants-evidence.csv` | **Start here.** One row per evidence row (26,878), flattened and ready to load. Carries the plant's canonical URL on every row. |
| `plants-evidence.jsonl` | Lossless. One line per plant, each the plant's published record, including fields the flat table drops (photo metadata, common names, identifiers, review notes, and the typed range, status, hardiness and maintenance assertions). Three runtime-only keys the site uses to answer place questions in the browser (`localAssessmentInputs`, `localAssessmentContract`, `legacyCompatibilityProjection`) are withheld: they are machinery, not cited facts, and they were 42% of the payload. |
| `plant-sources.csv` | The source registry, one row per source (112). |
| `plant-sources.json` | The same registry, lossless, keyed by slug — editions stay an array. |
| `croissant.json` | Croissant 1.1 metadata (what Hugging Face and Kaggle read). Validated with `mlcroissant validate --jsonld`. |

Join `plants-evidence.source` to `plant-sources.slug`.

## How to reproduce a classification

1. Take a plant's evidence rows from `plants-evidence.csv`.
2. Resolve each row to its lineage: if `original` names a slug present in
   `plant-sources`, use that source; otherwise use `source`. This is
   chain-to-root — it stops a rater outvoting itself through republication.
3. Keep only Tier 1 rows (`tier` in the registry).
4. Tally distinct lineages recommending versus condemning. A lineage carrying
   both directions is internally conflicted and counts for neither.
5. Majority direction classifies. A tie is `disputed`. If direct fire evidence
   dissents from a curated majority, the result is `disputed` rather than the
   majority — direct evidence is not outvoted by curation.

## Columns — `plants-evidence.csv`

| Column | Meaning |
|---|---|
| `plantId` | Stable id; the last segment of the canonical URL |
| `scientificName` | Name as the directory files it |
| `acceptedName` | Currently accepted name where it differs |
| `family`, `plantForm` | Botanical family; tree / shrub / grass / etc. |
| `flammabilityClass` | **Computed**: `fire-resistant`, `mixed-evidence`, `highly-flammable` |
| `ratingReason` | Why: `consensus`, `majority`, `disputed`, `conditional`, `mid-scale`, `limited-evidence` |
| `recommendation` | User-facing resolution: `on-list`, `avoid`, `candidate`, `conflict` |
| `canonicalUrl` | The plant's page on FireApproved.com |
| `source` | Registry slug this row is attributed to — joins to `plant-sources.slug` |
| `sourcePage` | The page for that source on FireApproved.com, listing everything else it rated. Distinct from `canonicalUrl`, which is the plant |
| `original` | **Two meanings.** When it names a registry slug (580 rows), it is a chain-to-root pointer and the row's tier and lineage resolve through it. Otherwise (19,507 rows) it is a bibliographic citation key for the primary study named by a compilation, and the row resolves through `source`. |
| `via` | The intermediate that republished the claim, where one is recorded |
| `verdict` | Normalised direction: `recommend`, `avoid`, `mid`, and similar |
| `verdictRaw` | **The source's own wording of its finding** |
| `claims` | Supporting statements extracted from the source, pipe-separated |
| `claimOriginal` | The claim in the original language where the source is not English |
| `score` | The source's own numeric score, where it published one — scales are **not** interchangeable between sources |
| `plantPart` | What was tested or observed (foliage, litter, whole plant) |
| `condition` | Stated condition, e.g. `irrigated` — a rating can be conditional on it |
| `sourcePlacement` | The source's own placement rule, in its own zone vocabulary |
| `edition`, `documentDate` | Which edition of the source, and its date |
| `sourceUrl` | The source document itself |
| `accessedOn` | When the document was read |

## Columns — `plant-sources.csv`

| Column | Meaning |
|---|---|
| `slug` | Join key |
| `name`, `publisher`, `url` | The document, who published it, where it is |
| `region` | Geographic scope the source speaks to |
| `tier` | Evidence tier. Tier 1 sources classify; others corroborate. Unset where the source states no method (6 of 112) |
| `evidenceKind` | `lab-tested`, `field-trial`, `post-fire-survey`, `expert-curated`, and similar |
| `lineage` | The root this source's findings trace to. Sources sharing a lineage are **not** independent |
| `editions` | Editions and dates, flattened; intact as an array in the JSON |
| `canonicalUrl` | The source's page on FireApproved.com, listing every plant it covers |
| `scaleNotes` | How the source's own scale was mapped to a verdict — read this before comparing scores across sources |
| `notes` | Reconciliation decisions, held rows, and honest gaps |

## Limits

- **Not a planting permit.** Evidence about a plant is not permission to plant
  it anywhere; [Zone 0](https://fireapproved.com/glossary/zone-0/) is
  noncombustible regardless of any plant's class.
- **No plant is fireproof.** Condition, maintenance and placement govern.
- **Scores are not comparable across sources.** Each source's scale is its
  own; `scaleNotes` says how it was read.
- Photo fields in the JSONL are metadata only (attribution and source URLs);
  the images are not included and are not CC BY.

**Citation:** FireApproved.com (2026). *Plant flammability evidence directory*
[Data set]. https://fireapproved.com/plants/ — CC BY 4.0.

- **License:** CC BY 4.0 — see the repository [LICENSE](../../LICENSE.md).

The live site is the source of truth. This mirror is rebuilt from the built
site by `scripts/build-data-mirror.mjs` in the fireapproved-com repository.

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

- 📍 **[Places](https://fireapproved.com/places/)** — start with where you are.
  One briefing per state covering what the code adopted there
  [actually says](https://fireapproved.com/requirements/), cited to the
  ordinance rather than to a summary of it.
- 🌿 **[Plants](https://fireapproved.com/plants/)** — thousands of taxa with
  every cited rating, browsable [by genus](https://fireapproved.com/plants/genus/)
  or [by the source that rated it](https://fireapproved.com/plants/source/), and
  grouped for a place on [Grow](https://fireapproved.com/grow/).
- 🏠 **[Materials](https://fireapproved.com/materials/)** — the vents, siding,
  decking, windows and roofing that are actually listed and tested, with the
  [standards](https://fireapproved.com/standards/) behind them and a
  [lapse log](https://fireapproved.com/materials/lapse-log/) for listings that
  have expired. [Build](https://fireapproved.com/build/) walks the house by
  assembly.
- 📚 **[Learn](https://fireapproved.com/learn/)** — plain-language answers,
  from [where to start](https://fireapproved.com/guides/hardening-ladder/) to
  [how to read a plant page](https://fireapproved.com/guides/how-to-read-a-plant-page/),
  with a [glossary](https://fireapproved.com/glossary/) for the terms the codes
  use and [the full guide index](https://fireapproved.com/guides/).
- 🔎 **[Findings](https://fireapproved.com/findings/)** — the places where a
  test result or a jurisdiction contradicts what everyone repeats.

**Start here:** [fireapproved.com](https://fireapproved.com) ·
[where you are](https://fireapproved.com/places/) ·
[the plant directory](https://fireapproved.com/plants/) ·
[the materials directory](https://fireapproved.com/materials/) ·
[how this is built](https://fireapproved.com/methodology/)

> **Changed since the 2026-08-25 snapshot.** The site reorganized around
> location on 2026-08-26. `/states/`, `/plants/state/` and `/plants/zone/` are
> gone; [`/places/`](https://fireapproved.com/places/) is the state trunk, and
> [Build](https://fireapproved.com/build/), [Grow](https://fireapproved.com/grow/)
> and [Learn](https://fireapproved.com/learn/) are the three branches off it.
> Record URLs in the data files (`/plants/{id}/`, `/materials/{id}/`) did not
> move, so rows published against the earlier snapshot still resolve.

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
