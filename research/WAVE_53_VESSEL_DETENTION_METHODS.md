# Wave 53V — Research Methods

Namespace: **W53V**

## W53V-M01 — IMO Number Primary Identity
Use IMO number as primary durable identity for eligible seagoing vessels where available.

Names/flags/owners can change.

## W53V-M02 — Detention Public-Time Ledger
Store detention occurrence, first USCG publication, validation update, appeal and release separately.

## W53V-M03 — Validated-List Revision Archive
USCG detention lists can change after validation/appeal.

Archive every public vintage.

## W53V-M04 — PSIX Weekly Snapshot Gate
PSIX represents a weekly FOIA snapshot, not a live complete operational-control feed.

## W53V-M05 — Open-Case Blind Spot
PSIX may omit unclosed/pending privileged cases.

Absence is not proof of no control action.

## W53V-M06 — Detention vs Deficiency
Not every deficiency causes detention.

Preserve deficiency and detention states separately.

## W53V-M07 — Safety vs Security vs Environmental
Classify legal basis; do not pool all detention causes without controls.

## W53V-M08 — Owner / Operator / ISM Manager Split
A ship's registered owner, beneficial owner, commercial operator and ISM manager may differ.

Version entity links.

## W53V-M09 — Flag Vintage
Use flag in effect at the event time.

## W53V-M10 — Recognized Organization Vintage
Class/RO relationships can change; use point-in-time association.

## W53V-M11 — Capacity Denominator
Use vessel-type-specific capacity:
DWT, TEU, cbm, lane meters, etc.

## W53V-M12 — Loaded-State Confidence
Cargo-loaded status requires AIS draft, port/cargo evidence or other sourced confirmation.

## W53V-M13 — Release-Time Uncertainty
If only monthly/weekly evidence exists, preserve censoring interval rather than invent a timestamp.

## W53V-M14 — Legal Release vs Physical Departure
A detention can be lifted while weather, cargo, repair or commercial constraints still delay sailing.

## W53V-M15 — Appeal Selection Bias
Appealed cases are not a random sample of detentions.

## W53V-M16 — Targeting Endogeneity
High-risk flags/managers receive more scrutiny, which increases detection probability.

Control exam intensity.

## W53V-M17 — Sister-Vessel Independence
Multiple vessels of one manager are correlated observations.

Use hierarchical models.

## W53V-M18 — Substitute-Vessel Proof
Potential substitute counts only if class, route, terminal compatibility and timing permit replacement.

## W53V-M19 — Common-Port Shock Control
A port campaign or concentrated inspection program can increase detentions across many ships at once.

## W53V-M20 — Physical Promotion Gate
Before market alpha, require OOS improvement in:
detention duration,
actual sailing,
fleet availability,
freight capacity,
or cargo delay.
