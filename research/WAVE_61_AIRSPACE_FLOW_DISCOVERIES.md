# Wave 61F — Airspace Flow & Airport Capacity

Namespace: **W61F**

Thesis: airline and cargo capacity can collapse even when aircraft are fully airworthy. FAA traffic-management initiatives, NOTAMs, runway closures, route constraints, staffing triggers and airport-construction restrictions create real-time capacity states that propagate through hubs and networks before monthly transportation statistics reveal the outcome.

W48 owns aircraft airworthiness. W61F owns **network/airport operational capacity**.

All candidates are research hypotheses only. Claude owns later implementation.

## W61F-E01 — ATCSCC Ground Stop State
Normalize FAA ATCSCC ground-stop advisories:
airport,
start/end,
cause,
revision/cancellation,
scope.

Priority: S

## W61F-E02 — Ground Delay Program State
Track GDP:
airport,
program period,
arrival-rate target where public,
EDCT window,
revision,
cancellation.

Priority: S

## W61F-E03 — Proposed-to-Active Transition
FAA advisories can move:
POSSIBLE
-> PROPOSED
-> ACTIVE
-> REVISED
-> CANCELLED.

Estimate probability of escalation before activation.

Priority: S

## W61F-E04 — Arrival-Rate Capacity Delta
Where advisory text gives constrained arrival rate:
new rate - normal/expected airport rate.

Priority: S

## W61F-E05 — Constraint Cause Taxonomy
WEATHER
WIND
LOW_CEILING
THUNDERSTORM
CONSTRUCTION
PROCEDURAL
STAFFING
EQUIPMENT
SECURITY/TFR
VOLCANIC
OTHER.

Priority: S-

## W61F-E06 — Staffing Trigger State
ATCSCC operations plans list staffing triggers by facility/area.

Build:
triggered facility
× time
× downstream airport/route exposure.

Priority: S-

## W61F-E07 — Route Closure State
Track:
oceanic,
Gulf,
Atlantic,
regional,
special-use,
weather-avoidance route closures.

Priority: A+

## W61F-E08 — Reroute Burden
Estimate added distance/time/fuel from mandatory/recommended reroute structure.

Priority: A+

## W61F-E09 — Flow-Constrained Area State
Track FCA/AFP/CTOP constraints and affected traffic streams.

Priority: A

## W61F-E10 — Airport NOTAM Capacity Shock
Primary source:
FAA NOTAM.

Parse:
runway closed,
partial runway,
taxiway/ramp restriction,
navaid failure,
procedure restriction,
airport closure.

Priority: S

## W61F-E11 — Runway-Capacity Fraction
Estimate available runway configuration capacity after closure/construction.

Priority: S

## W61F-E12 — Construction Calendar Risk
FAA airport-construction notices can create scheduled capacity reductions.

Separate expected construction from unplanned closure.

Priority: A+

## W61F-E13 — Hub Connection Cascade
For constrained hub:
estimate missed-connection/cancellation propagation using bank structure and carrier schedule.

Priority: S

## W61F-E14 — Aircraft Rotation Propagation
Delay at one hub can make downstream aircraft legs late even after local constraint clears.

Priority: S

## W61F-E15 — Crew Duty-Time Cascade
Long irregular operations can push crew beyond legal/contract duty windows and turn delays into cancellations.

Use public/airline operational evidence where available.

Priority: A+

## W61F-E16 — Network Recovery Half-Life
After GDP/ground stop cancellation:
measure time until departures/arrivals/cancellations normalize.

Priority: S

## W61F-E17 — Airport Constraint Breadth
Aggregate simultaneous constrained hub share by:
carrier,
region,
cargo network,
national departures.

Priority: S

## W61F-E18 — Carrier-Specific Exposure
Weight airport/route constraints by carrier schedule share and hub dependence.

Priority: S

## W61F-E19 — Cargo Hub Capacity Shock
Specialize for MEM/SDF/IND/CVG/ANC and other major cargo hubs.

Map:
capacity loss
-> package/airfreight network propagation.

Priority: S-

## W61F-E20 — Express Logistics Spillover
Estimate impact on time-sensitive:
semiconductors,
pharma,
e-commerce,
critical parts
from cargo-hub disruption.

Priority: A+

## W61F-E21 — Jet Fuel Demand Shortfall
Large cancellation/ground-stop events reduce flight fuel burn.

Estimate:
cancelled/delayed flight-hours
× aircraft mix
× stage length.

Priority: A

## W61F-E22 — Weather vs ATC Residual
Weather forecast alone may over/underpredict actual FAA intervention.

Feature:
realized traffic-management severity
-
weather-implied expected severity.

Priority: S

## W61F-E23 — Staffing vs Weather Decomposition
Same delays can arise from storms or ATC staffing.

Explicitly separate causal categories using ATCSCC text.

Priority: A+

## W61F-E24 — NOTAM × ATCSCC Collision
A runway closure plus weather/traffic-management constraint can produce nonlinear capacity loss.

Priority: S

## W61F-E25 — Special Event / TFR Flow Shock
Track event-related TFR/route structures where they materially alter commercial traffic.

Priority: B+

## W61F-E26 — Volcanic Airspace Shock
ATCSCC publishes volcanic activity bulletins and route changes.

Fuse ash hazard with route/airport state.

Priority: A

## W61F-E27 — BTS Outcome Validation
Use monthly BTS on-time records for:
actual delays,
cancellations,
diversions,
delay causes.

Validation only; not a live source.

Priority: Infrastructure

## W61F-E28 — Airline Capacity-Loss Quotient
ACLQ =
expected unavailable seat/cargo-flight capacity
/
available alternate airport + carrier + route capacity.

Priority: S

## W61F-E29 — Airspace Truth Ladder
FORECAST/PLAN
-> FAA POSSIBLE/PROPOSED INITIATIVE
-> ACTIVE GS/GDP/ROUTE/NOTAM
-> FLIGHT DELAY/CANCEL/DIVERT
-> NETWORK CASCADE
-> CARGO/PASSENGER CAPACITY LOSS
-> RECOVERY.

Priority: S architecture

## Highest-priority W61F tests

1. W61F-E03 Proposed-to-Active Transition
2. W61F-E04 Arrival-Rate Capacity Delta
3. W61F-E06 Staffing Trigger State
4. W61F-E10 Airport NOTAM Capacity Shock
5. W61F-E11 Runway-Capacity Fraction
6. W61F-E13 Hub Connection Cascade
7. W61F-E14 Aircraft Rotation Propagation
8. W61F-E18 Carrier-Specific Exposure
9. W61F-E24 NOTAM × ATCSCC Collision
10. W61F-E28 Airline Capacity-Loss Quotient
