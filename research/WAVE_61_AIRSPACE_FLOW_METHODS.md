# Wave 61F — Research Methods

Namespace: **W61F**

## W61F-M01 — Advisory Lineage
Archive every ATCSCC advisory, revision and cancellation with send/effective times.

## W61F-M02 — Possible vs Active
Operations-plan references to possible initiatives are forecasts, not active restrictions.

## W61F-M03 — UTC Discipline
FAA operational clocks often use Zulu time. Preserve source timezone and normalize correctly.

## W61F-M04 — Airport/Facility Mapping
Map ARTCC/TRACON/airport identifiers to affected commercial flows.

## W61F-M05 — Normal Capacity Baseline
Expected arrival/departure rate depends on runway configuration, weather and time of day.

## W61F-M06 — Cause Parser
Use FAA-stated cause where present; do not infer staffing from delay alone.

## W61F-M07 — NOTAM Vintage
Archive issue/start/end/cancel time and exact affected facility/runway/procedure.

## W61F-M08 — Scheduled vs Unplanned Closure
Construction known in advance is a different population from emergency closure.

## W61F-M09 — Schedule Exposure
Use point-in-time scheduled flights when estimating carrier capacity at risk.

## W61F-M10 — Rotation Graph
Track aircraft tail/rotation only from lawful/public data; otherwise use probabilistic schedule connectivity.

## W61F-M11 — Crew Constraint Uncertainty
Crew legality/availability is generally not fully public.
Use scenario bounds.

## W61F-M12 — Throughput Validation
Validate predicted capacity against actual departures/arrivals where source rights allow.

## W61F-M13 — BTS Lag Gate
BTS on-time data are monthly retrospective truth, not live state.

## W61F-M14 — Weather Common-Cause Control
Weather simultaneously drives FAA initiatives and customer demand/operations.

## W61F-M15 — Airport Substitution
Nearby airports are substitutes only if slots, gates, surface access and carrier network support diversion.

## W61F-M16 — Cargo vs Passenger Split
Cargo hub economics differ from passenger banks.

## W61F-M17 — Recovery Separation
FAA cancellation of a program does not imply network normalization.

## W61F-M18 — Multi-Initiative Deduplication
One storm can create several FAA advisories for the same underlying constraint.

## W61F-M19 — Constraint Collision
Estimate interaction effects for simultaneous runway/weather/staffing/route limitations.

## W61F-M20 — Operational Promotion Gate
Before financial alpha require OOS improvement in:
airport throughput,
delay,
cancellation,
diversion,
network recovery,
or cargo/seat capacity.
