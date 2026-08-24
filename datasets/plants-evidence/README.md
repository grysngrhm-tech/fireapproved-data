# Plants evidence directory

The full FireApproved plant directory as machine-readable evidence records:
2,123 plants carrying 5,008 flammability evidence rows (source, verdict,
verbatim quoted claim, edition, access date), identifiers (GBIF, Wikidata,
iNaturalist, ITIS, USDA symbol where resolved), state placements, and growth
facts.

FireApproved issues no ratings of its own. Each plant's classification is
computed from the evidence rows by a published method (majority direction by
independent source lineage; direct fire evidence is never silently outvoted by
curation; conflicts stay visible). This export carries the evidence, so you
can recompute or re-weigh it yourself.

- **Canonical pages:** https://fireapproved.com/plants/ — every plant has a
  JSON twin at `https://fireapproved.com/plants/{id}.json`; each line of this
  file is one twin, verbatim.
- **Methodology:** https://fireapproved.com/methodology
- **File here:** `plants-evidence.jsonl` — one JSON record per line, sorted by
  plant id.
- **License:** CC BY 4.0 — see the repository [LICENSE](../../LICENSE.md).
  Photo fields are metadata only (attribution, source and observation URLs);
  the images themselves are not included and are not CC BY.

**Citation:** FireApproved.com (2026). *Plants evidence directory* [Data set].
https://fireapproved.com/plants/ — CC BY 4.0.

The live site is the source of truth; this mirror is refreshed manually.
