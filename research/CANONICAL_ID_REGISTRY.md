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

### W7T — Physical network telemetry wave
Sources:
- `research/WAVE_7_TELEMETRY_DISCOVERIES.md`
- `research/WAVE_7_TELEMETRY_METHODS.md`
- `research/WAVE_7_TELEMETRY_SOURCE_NOTES.md`

W7T uses canonical IDs directly:
- edges W7T-E01 through W7T-E23
- methods W7T-M01 through W7T-M20
- sources W7T-D01 through W7T-D12

### W8M — Mechanical flow / pre-trade intent wave
Sources:
- `research/WAVE_8_MECHANICAL_FLOWS_DISCOVERIES.md`
- `research/WAVE_8_MECHANICAL_FLOWS_METHODS.md`
- `research/WAVE_8_MECHANICAL_FLOWS_SOURCE_NOTES.md`

W8M uses canonical IDs directly:
- edges W8M-E01 through W8M-E24
- methods W8M-M01 through W8M-M20
- sources W8M-D01 through W8M-D08

### W9O — Hidden operational exhaust wave
Sources:
- `research/WAVE_9_OPERATIONAL_EXHAUST_DISCOVERIES.md`
- `research/WAVE_9_OPERATIONAL_EXHAUST_METHODS.md`
- `research/WAVE_9_OPERATIONAL_EXHAUST_SOURCE_NOTES.md`

W9O uses canonical IDs directly:
- edges W9O-E01 through W9O-E23
- methods W9O-M01 through W9O-M22
- sources W9O-D01 through W9O-D11

### W10B — Dealer balance-sheet / funding-plumbing wave
Sources:
- `research/WAVE_10_BALANCE_SHEET_DISCOVERIES.md`
- `research/WAVE_10_BALANCE_SHEET_METHODS.md`
- `research/WAVE_10_BALANCE_SHEET_SOURCE_NOTES.md`

W10B uses canonical IDs directly:
- edges W10B-E01 through W10B-E22
- methods W10B-M01 through W10B-M20
- sources W10B-D01 through W10B-D08

### W11S — Future physical supply pipeline wave
Sources:
- `research/WAVE_11_FUTURE_SUPPLY_DISCOVERIES.md`
- `research/WAVE_11_FUTURE_SUPPLY_METHODS.md`
- `research/WAVE_11_FUTURE_SUPPLY_SOURCE_NOTES.md`

W11S uses canonical IDs directly:
- edges W11S-E01 through W11S-E23
- methods W11S-M01 through W11S-M20
- sources W11S-D01 through W11S-D08

### W12C — Clearing / margin / delivery mechanics wave
Sources:
- `research/WAVE_12_CLEARING_MARGIN_DISCOVERIES.md`
- `research/WAVE_12_CLEARING_MARGIN_METHODS.md`
- `research/WAVE_12_CLEARING_MARGIN_SOURCE_NOTES.md`

W12C uses canonical IDs directly:
- edges W12C-E01 through W12C-E24
- methods W12C-M01 through W12C-M22
- sources W12C-D01 through W12C-D08

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


### W8R — Pre-regulatory warning / safety lifecycle wave
Sources:
- `research/WAVE_8_REGULATORY_DISCOVERIES.md`
- `research/WAVE_8_REGULATORY_METHODS.md`
- `research/WAVE_8_REGULATORY_SOURCE_NOTES.md`

W8R uses canonical IDs directly:
- edges W8R-E01 through W8R-E20
- methods W8R-M01 through W8R-M20
- sources W8R-D01 through W8R-D10


### W9C — Capacity rights before reality wave
Sources:
- `research/WAVE_9_CAPACITY_RIGHTS_DISCOVERIES.md`
- `research/WAVE_9_CAPACITY_RIGHTS_METHODS.md`
- `research/WAVE_9_CAPACITY_RIGHTS_SOURCE_NOTES.md`

W9C uses canonical IDs directly:
- edges W9C-E01 through W9C-E20
- methods W9C-M01 through W9C-M20
- sources W9C-D01 through W9C-D10


### W11C — Mandatory commitments / convexity wave
Sources:
- `research/WAVE_11_COMMITMENT_CONVEXITY_DISCOVERIES.md`
- `research/WAVE_11_COMMITMENT_CONVEXITY_METHODS.md`
- `research/WAVE_11_COMMITMENT_CONVEXITY_SOURCE_NOTES.md`

W11C uses canonical IDs directly:
- edges W11C-E01 through W11C-E22
- methods W11C-M01 through W11C-M20
- sources W11C-D01 through W11C-D10


### W12F — Freight / livestock / exchange rule-state wave
Sources:
- `research/WAVE_12_FREIGHT_RULESTATE_DISCOVERIES.md`
- `research/WAVE_12_FREIGHT_RULESTATE_METHODS.md`
- `research/WAVE_12_FREIGHT_RULESTATE_SOURCE_NOTES.md`

W12F uses canonical IDs directly:
- edges W12F-E01 through W12F-E22
- methods W12F-M01 through W12F-M20
- sources W12F-D01 through W12F-D10


### W13H — Human capacity / communications resilience wave
Sources:
- `research/WAVE_13_HUMAN_CAPACITY_DISCOVERIES.md`
- `research/WAVE_13_HUMAN_CAPACITY_METHODS.md`
- `research/WAVE_13_HUMAN_CAPACITY_SOURCE_NOTES.md`

W13H uses canonical IDs directly:
- edges W13H-E01 through W13H-E24
- methods W13H-M01 through W13H-M20
- sources W13H-D01 through W13H-D10


### W14I — Critical infrastructure / chokepoints wave
Sources:
- `research/WAVE_14_INFRASTRUCTURE_CHOKEPOINTS_DISCOVERIES.md`
- `research/WAVE_14_INFRASTRUCTURE_CHOKEPOINTS_METHODS.md`
- `research/WAVE_14_INFRASTRUCTURE_CHOKEPOINTS_SOURCE_NOTES.md`

W14I uses canonical IDs directly:
- edges W14I-E01 through W14I-E25
- methods W14I-M01 through W14I-M20
- sources W14I-D01 through W14I-D10
