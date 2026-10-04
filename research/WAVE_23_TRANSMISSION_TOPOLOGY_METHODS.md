# Wave 23T — Research Methods

Namespace: **W23T**

## W23T-M01 — Constraint Identity Graph
Normalize facility/contingency aliases without deleting source-native names.

## W23T-M02 — Five-Minute Availability Ledger
Store source interval, publication/update time, first ingest and revision status.

## W23T-M03 — Day-Ahead / Real-Time Separation
Never expose real-time constraints to a day-ahead decision timestamp.

## W23T-M04 — Shadow-Price Sign Discipline
Market conventions differ. Preserve native sign and derive absolute/intuitive metrics separately.

## W23T-M05 — Market-Specific Normalization
Normalize shadow prices, penalty caps and topology within each ISO before cross-market comparison.

## W23T-M06 — Outage Vintage Archive
Archive proposed/accepted/withdrawn/rejected/active/completed transmission outages as separate states.

## W23T-M07 — Market-Sensitive Data Boundary
PJM excludes market-sensitive outages from public TFOL. Treat public outage data as incomplete by design.

## W23T-M08 — Topology-Aware Matching
Match constraint to outages/regions using explicit facility topology, voltage and contingency identity.

## W23T-M09 — Planned-Outage Baseline
Expected scheduled outages enter the baseline, not surprise.

## W23T-M10 — Limit Change vs Flow Change
Separate operator limit/derate changes from physical flow changes.

## W23T-M11 — Contingency-Specific Recurrence
The same monitored element under a different contingency is a distinct state.

## W23T-M12 — Constraint Duration Stitching
Merge consecutive intervals only with identical/compatible constraint identity and no publication gap.

## W23T-M13 — Common Load/Weather Control
Load, wind, solar and weather jointly affect flows and congestion.

## W23T-M14 — Generation-Outage Control
A generator outage can create or remove congestion; model jointly.

## W23T-M15 — Nodal-to-Asset Exposure
Map congestion effects to generators/load/storage only with network/location evidence.

## W23T-M16 — Day-Ahead Expectation Model
Use the actual published day-ahead grid outcome as the expectation baseline where available.

## W23T-M17 — Unforeseen Event Classification
Classify DA->RT divergence into transmission outage, generation outage, load/weather miss, renewable miss or unresolved.

## W23T-M18 — Price Validation Ladder
constraint
-> dispatch/interchange
-> local congestion component
-> local fuel/storage consequence
-> financial target.

## W23T-M19 — Cross-ISO Rule Versioning
Market definitions, caps and reporting formats change. Version protocol/tariff semantics historically.

## W23T-M20 — Physical Promotion Gate
Promote only after incremental OOS prediction of topology, dispatch, congestion or transfer behavior.
