# Canonical Research ID Registry

## Purpose

Multiple research processes are contributing to this repository concurrently. Early research used global-looking IDs such as `E81`. A later concurrent wave reused `E81-E100` while Wave 3 already contained `E81-E90`. No research content was lost, but those legacy IDs are ambiguous outside their source file.

From this point forward, **wave-scoped IDs are canonical**. Legacy IDs remain historical aliases only.

## Canonical scheme

`<namespace>-<type><number>`

Examples:
- `W1-E03`
- `W2-E01`
- `W3-E21`
- `W4F-E01`
- `W5P-E01`
- `W6N-E01`

Types:
- E = edge / hypothesis
- M = research method
- D = data source
- C = composite concept
- N = negative control
- W = future watchlist item

## Namespace map

### W1 — Core Edge Atlas
Source: `research/EDGE_ATLAS.md`

- Legacy E01-E40 -> W1-E01 through W1-E40
- Legacy W01-W03 -> W1-W01 through W1-W03

### W2 — Regulatory / short-pressure wave
Sources:
- `research/WAVE_2_DISCOVERIES.md`
- `research/WAVE_2_METHODS.md`

- Legacy E41-E60 -> W2-E01 through W2-E20
- Legacy M21-M40 -> W2-M01 through W2-M20

### W3 — Crypto / physical-energy / innovation wave
Sources:
- `research/WAVE_3_DISCOVERIES.md`
- `research/WAVE_3_METHODS.md`

- Legacy E61-E90 -> W3-E01 through W3-E30
- Legacy M41-M55 -> W3-M01 through W3-M15

### W4F — Funding / Treasury / procurement / ownership wave
Sources:
- `research/WAVE_4_DISCOVERIES.md`
- `research/WAVE_4_METHODS.md`

- Legacy E81-E100 -> W4F-E01 through W4F-E20
- Legacy M56-M70 -> W4F-M01 through W4F-M15

**Collision note:** legacy W4F E81-E90 overlaps legacy W3 E81-E90. Never join or refer across files using those legacy IDs alone.

### W5P — Physical-delivery / sanctions / cyber / port / tariff wave
Sources:
- `research/WAVE_5_DISCOVERIES.md`
- `research/WAVE_5_METHODS.md`

- Legacy E101-E122 -> W5P-E01 through W5P-E22
- Legacy M71-M90 -> W5P-M01 through W5P-M20

### W6N — NQ / gold / credit / procurement / policy wave
Sources:
- `research/WAVE_6_NQ_GOLD_DISCOVERIES.md`
- `research/WAVE_6_NQ_GOLD_METHODS.md`
- `research/WAVE_6_NQ_GOLD_SOURCE_NOTES.md`

W6N uses canonical IDs directly.

## Durable identity

The durable machine key should be:

`canonical_id + source_file + content_hash`

Titles are allowed to evolve without changing identity. If an idea is materially redefined rather than refined, allocate a new canonical ID and link it as a successor.

## Rules for Claude

When importing or discussing a candidate:
1. Use the canonical ID.
2. Preserve its source file and content hash.
3. Preserve a legacy ID only as an alias.
4. Never join records on a legacy ID alone.
5. If two candidates overlap conceptually, keep both provenance records and explicitly merge them in a new synthesis record rather than silently deleting one.

## Rules for future contributors

1. Never allocate new unscoped global `E###` or `M###` IDs.
2. Create a unique namespace before adding a wave.
3. Do not rewrite another contributor's historical source file merely to renumber it.
4. Add mappings here instead.
5. No force-pushing to resolve concurrent contributions.
