# Wave 7T — Research Methods

Namespace: W7T

## W7T-M01 — Telemetry Availability Timestamp
Store measurement_time, source_publish_time, first_seen_time, revision_time and finalization_status.

## W7T-M02 — Weather / Calendar Residualization
Remove hour, weekday, holiday, season, weather, scheduled maintenance and delivery-cycle effects before testing residuals.

## W7T-M03 — Hierarchical Physical Baseline
Build sensor/facility -> region -> national baselines.

## W7T-M04 — Physics-First Target Ladder
Predict physical intermediates before price:
river -> draft/queue;
grid -> gas burn;
FAA -> throughput;
thermal -> outage confirmation;
rail -> shipment delay.

## W7T-M05 — Bottleneck Centrality
Weight locks, airports, terminals, balancing authorities and ports by network centrality and economic throughput.

## W7T-M06 — Recovery-Asymmetry Test
Estimate shock onset and restoration separately.

## W7T-M07 — Sensor Quality Gate
Track provisional status, staleness, missingness, impossible jumps, neighbor consistency and revision frequency.

## W7T-M08 — Spatial Exposure Join
Use explicit geospatial distance/intersection rules for facility and company exposure.

## W7T-M09 — Common-Weather Confound Control
Condition on shared weather drivers before claiming cross-system causality.

## W7T-M10 — Network Propagation Timing
Test whether downstream impacts follow network topology and plausible travel/processing time.

## W7T-M11 — Delayed Holdings Availability Mask
N-PORT holdings are unavailable before public dissemination regardless of portfolio date.

## W7T-M12 — Crowding Null Model
Match null portfolios on size, sector, liquidity, beta, fund size and style.

## W7T-M13 — Substitution Capacity Model
Impact = disruption severity × lack of substitute capacity.

## W7T-M14 — Operational Severity Scale
NORMAL / DEGRADED / RESTRICTED / PARTIAL_CLOSURE / FULL_CLOSURE / RECOVERING.

## W7T-M15 — Multi-Cadence Fusion
Never forward-fill slow sources as though they were live. Every feature has native cadence and expiry.

## W7T-M16 — Counterfactual Throughput
Impact = expected throughput absent shock - realized throughput.

## W7T-M17 — Thermal False-Positive Control
Require facility geofence, historical baseline, sensor confidence, view geometry and preferably independent confirmation.

## W7T-M18 — Public-vs-Licensed Layering
PUBLIC_LIVE / PUBLIC_DELAYED / LICENSED_LIVE / LICENSED_DELAYED / RETROSPECTIVE_ONLY.

## W7T-M19 — Source Health as a Feature
Differentiate true zero, unscheduled, sensor offline, publication delayed and API unavailable.

## W7T-M20 — Mechanism Promotion Gate
Require clean availability, physical-intermediate validation, OOS market value, cost/capacity viability and incremental value over existing ICARUS features.
