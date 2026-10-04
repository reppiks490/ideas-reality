# Wave 47S — Research Methods

Namespace: **W47S**

## W47S-M01 — Public-Time vs Legal-Time
Store:
announcement/publication time,
Federal Register publication,
effective legal time,
list-file update time,
first ingest.

## W47S-M02 — Complete List Vintage Archive
Archive each OFAC/BIS/CSL list vintage, not only deltas.

## W47S-M03 — Hash / Integrity Verification
Where official hashes are published, verify downloaded sanctions files before ingest.

## W47S-M04 — List-Specific Semantics
SDN, non-SDN, Entity List, DPL, UVL and MEU are different legal states.

Do not collapse them.

## W47S-M05 — Name Matching Is Not Identity
Use identifiers, addresses, registration numbers, IMO/MMSI/tail numbers and ownership evidence.

Fuzzy name matches remain probabilistic.

## W47S-M06 — 50 Percent Ownership Aggregation
Aggregate blocked ownership exactly per OFAC guidance.

Control alone without >=50% ownership is not automatically equivalent to 50 Percent Rule blocking.

## W47S-M07 — Ownership Vintage
Corporate ownership must be point-in-time and sourced.

## W47S-M08 — General License Parser
Extract:
covered parties,
covered transactions,
conditions,
start/effective time,
expiration/wind-down time,
exceptions.

## W47S-M09 — Federal Register Rule Diff
Machine-diff regulatory text/appendices, then manually validate material scope changes.

## W47S-M10 — Entity List Footnote Versioning
Preserve footnotes and license requirements/policies at each historical date.

## W47S-M11 — ECCN Evidence Gate
Do not assign a company's product to an ECCN without direct technical/regulatory evidence.

## W47S-M12 — FDPR Causality Gate
Foreign Direct Product Rule exposure requires validated production/technology lineage.

## W47S-M13 — Order-Scope Parsing
Temporary Denial Orders and denial orders can have party- and activity-specific terms.

Parse the operative text.

## W47S-M14 — Effective-Date Backtest Mask
No rule/list state is visible before first public availability.

## W47S-M15 — Media Leak Separation
If credible media precedes official publication, treat media as a separate source/event, never backdate the official state.

## W47S-M16 — Supply-Chain Relationship Vintage
Customer/supplier relationships change over time.

Use point-in-time public relationship evidence.

## W47S-M17 — Substitute Capacity Proof
Potential substitute supplier is not real substitute capacity unless product qualification, geography and scaling evidence support it.

## W47S-M18 — Trade-Flow Validation
Validate legal restriction against later shipments/customs/port/inventory where possible.

## W47S-M19 — Common-Geopolitical Control
Separate broad geopolitical risk-off moves from entity/product-specific restriction effects.

## W47S-M20 — Intermediate Promotion Gate
Before financial alpha, require OOS improvement in:
transaction eligibility,
shipment/order flow,
trade volume,
supplier/customer revenue,
inventory,
or substitution.
