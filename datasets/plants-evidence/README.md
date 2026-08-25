# Plant flammability evidence directory

The full FireApproved plant directory as machine-readable evidence records:
3,801 plants carrying 26,878 flammability evidence rows, plus the source
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

## Files

| File | What it is |
|---|---|
| `plants-evidence.csv` | **Start here.** One row per evidence row (26,878), flattened and ready to load. Carries the plant's canonical URL on every row. |
| `plants-evidence.jsonl` | Lossless. One line per plant, each the verbatim JSON twin published on the site, including fields the flat table drops (photo metadata, common names, identifiers, review notes). |
| `plant-sources.csv` | The source registry, one row per source (112). |
| `plant-sources.json` | The same registry, lossless, keyed by slug — editions stay an array. |

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
