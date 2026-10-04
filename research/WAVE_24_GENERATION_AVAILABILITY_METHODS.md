# Wave 24A — Research Methods

Namespace: **W24A**

## W24A-M01 — Outage Vintage Archive
Archive every published outage forecast/snapshot; revisions are new information.

## W24A-M02 — Planned/Maintenance/Forced Hard Split
Never pool known planned work with forced outage surprise.

## W24A-M03 — Derate vs Full Outage
Represent capability loss MW, not binary unit state.

## W24A-M04 — Capability Denominator
Normalize outage MW to seasonal/available capacity appropriate to source semantics.

## W24A-M05 — Publication-Lag Mask
Physical outage start and public first-seen time are distinct.

## W24A-M06 — Resource-Class Normalization
Separate thermal, hydro, storage, wind, solar and other classes.

## W24A-M07 — Region/Zone Exposure
Use source-native regions/load zones and only map beyond them with explicit topology.

## W24A-M08 — Expected Outage Baseline
Build seasonal/day/hour/resource-class baseline from prior vintages and planned schedules.

## W24A-M09 — Forecast-to-Actual Revision
For each operating hour/day track how planned/forced outage expectation changed from long horizon to real time.

## W24A-M10 — Restart Censoring
Outages still active at sample end require survival-analysis censoring.

## W24A-M11 — Reclassification Ledger
Preserve planned->forced and other source reclassifications with timestamps.

## W24A-M12 — Common-Weather Control
Temperature/weather may cause both load and outages.

## W24A-M13 — Fuel-Cause Boundary
Do not infer gas/fuel failure from forced outage alone unless public cause evidence supports it.

## W24A-M14 — Reserve Accounting
Use the ISO's current reserve definitions and avoid mixing installed capacity with operational reserve.

## W24A-M15 — Emergency-Capacity Semantics
Emergency Max and similar fields may not imply normal economic availability. Preserve source definition.

## W24A-M16 — CAISO Outage Breakpoint Reconstruction
Do not sum overlapping curtailment breakpoints as simultaneous MW.

## W24A-M17 — Current-vs-Retrospective Separation
Prior-day corrected reports validate history; they cannot alter prior decisions.

## W24A-M18 — Cross-ISO Comparable Metric
Use normalized unavailable-capacity share and unexpected component, not raw MW, for cross-market work.

## W24A-M19 — Substitution Validation
Identify actual replacement generation/import/storage before attributing downstream fuel effects.

## W24A-M20 — Physical Promotion Gate
Promote only after OOS prediction of reserve headroom, dispatch substitution, scarcity or recovery.
