# Wave 28M — Research Methods

Namespace: **W28M**

## W28M-M01 — Weekly 107(a) Vintage Archive
MSHA states Open Government files are generally updated Friday afternoon.

Archive each complete replacement file and diff it against prior vintage.

## W28M-M02 — Final-Violations Quarantine
MSHA general Violations dataset includes only final citations/orders under current documentation.

Do NOT use it as a near-real-time enforcement feed.

## W28M-M03 — Dedicated-Order Priority
Use dedicated 107(a)/POV sources for severe-order timing when available; use final violations for later classification/validation.

## W28M-M04 — Issue-vs-Publication Clock
Store order issue date and first public dataset appearance separately.

Backtests use public appearance.

## W28M-M05 — Termination Vintage
An order's termination date may appear in a later weekly file.

Do not backfill termination information into earlier vintages.

## W28M-M06 — Area Scope Uncertainty
If the source does not quantify affected capacity, retain lower/base/upper affected-capacity estimates.

## W28M-M07 — Inspection Exposure Normalization
Mine enforcement counts depend on inspection exposure.

Normalize repeated-order features by inspection hours/events where available.

## W28M-M08 — Mine Identity Versioning
Use Mine ID as durable key; mine/operator/controller names can change.

## W28M-M09 — Operator/Controller Mapping
Keep mine operator and controller distinct and point-in-time.

## W28M-M10 — Quarterly Production Availability Mask
MSHA quarterly production is published after quarter-end.

Never make it visible during the quarter in live-style tests.

## W28M-M11 — Metal/Nonmetal Production Caveat
MSHA quarterly production field does not provide equivalent production coverage for all metal/nonmetal mines.

Use other official/industry sources for commodity tonnage when needed.

## W28M-M12 — Planned-vs-Forced Capacity
Mine status changes, maintenance and enforcement withdrawal are separate event types.

## W28M-M13 — Accident Common-Event Deduplication
A fatality, 103(k) control order and 107(a) order may describe one physical incident.

Parent them under one incident ID.

## W28M-M14 — POV State Versioning
POV notification and termination dates are point-in-time states.

## W28M-M15 — Commodity Exposure Confidence
A mine may produce multiple products/byproducts.

Require verified commodity mapping before market attribution.

## W28M-M16 — Lost-Tonnage Estimation
Estimate lost production from historical daily-equivalent production × affected-capacity fraction × duration, with uncertainty.

## W28M-M17 — Inventory/Transport Counterfactual
Validate whether lost mine output actually constrained delivered supply.

## W28M-M18 — Recovery Target
Define recovery using later physical output/shipment where possible, not merely order termination.

## W28M-M19 — Weekly Timing Stress Test
Because public 107(a) file refresh is weekly, test whether signal survives 0–7 day information lag distribution.

## W28M-M20 — Physical Promotion Gate
Before market testing, require OOS improvement in:
capacity unavailable,
lost output,
shipment shortfall,
inventory draw,
or substitute flow.
