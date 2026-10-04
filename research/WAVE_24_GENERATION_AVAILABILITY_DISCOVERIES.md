# Wave 24A — Generation Availability & Forced-Outage Scarcity

Namespace: **W24A**

Thesis: power-system scarcity is driven by *available* generation, not installed capacity. Public ISO/RTO data expose planned, maintenance and forced outages, derates, committed capacity, and projected reserve headroom on operational clocks. This wave isolates unexpected loss of dispatchable capability and the substitution burden it creates.

All candidates are research hypotheses only. Claude owns implementation.

## W24A-E01 — PJM Seven-Day Outage Stack

Primary source:
PJM Data Miner Generation Outage for Seven Days by Type.

PJM publishes actual/scheduled outage MW for today + next six days, split into:
planned,
maintenance,
forced,
total,
with region detail.

Priority: S

## W24A-E02 — Forced-Outage Surprise

Candidate:
actual forced outage MW
-
expected forced outage MW from seasonal/hour/fleet baseline.

Planned/maintenance MW belong in the expected state.

Priority: S

## W24A-E03 — Outage-Mix Shift

Feature:
forced / total outages
and
maintenance / total outages.

A high total outage stack caused by planned work is economically different from a sudden forced-outage spike.

Priority: A+

## W24A-E04 — Regional Forced-Outage Breadth

Measure forced outage acceleration across PJM regions.

Question:
local unit problem or systemwide stress?

Priority: A+

## W24A-E05 — Seven-Day Outage Revision Velocity

Archive each daily forecast vintage for each forecast date.

Feature:
change in expected outage MW
as operating day approaches.

Priority: S-

## W24A-E06 — Ninety-Day Planned-Outage Baseline

PJM publishes forecasted generation outage MW up to 90 days.

Use as:
expected maintenance/planned capacity withdrawal.

Research surprise relative to this slow forecast.

Priority: A

## W24A-E07 — Available-vs-Committed Capacity Gap

Fuse PJM daily generation capacity:
economic max
emergency max
total committed
with outages and load.

Candidate:
dispatchable headroom
=
available max
-
expected load
-
required reserve.

Priority: S

## W24A-E08 — Emergency-Max Dependence

Feature:
(emergency max - economic max)
/
reserve need.

High reliance on emergency capability may indicate thin normal dispatch headroom.

Priority: A+

## W24A-E09 — Projected Peak Reserve Compression

PJM morning operations summary provides projected peak:
scheduled capacity
tie flow
load forecast
operating reserve.

Track reserve margin revisions from 5–8 a.m. publication vintages.

Priority: S

## W24A-E10 — ERCOT Five-Minute Outage Pulse

Primary source:
ERCOT Generation Outages dashboard.

ERCOT states the dashboard shows current planned/forced outage MW, including full outages and qualifying partial derates, and updates every five minutes.

Priority: S

## W24A-E11 — ERCOT Dispatchable-vs-Renewable Outage Split

Separate:
planned dispatchable
forced dispatchable
planned renewable
forced renewable.

Mechanism differs:
thermal forced loss creates replacement dispatch pressure;
renewable outage may overlap with forecast/output conditions.

Priority: S-

## W24A-E12 — ERCOT Seasonal-Capability Loss

ERCOT outage values are measured as capability reduction relative to seasonal maximum capability.

Feature:
outage MW
/
relevant seasonal available fleet.

Priority: A+

## W24A-E13 — ERCOT Hourly 168-Hour Outage Surface

Primary source:
NP3-233-CD Hourly Resource Outage Capacity.

Public hourly report covers approved/accepted planned, forced and maintenance outages for the next 168 hours by load zone and resource class, including full outages and derates.

Priority: S

## W24A-E14 — Outage Curve Shape

For the next seven days, model:
outage MW by hour
rather than daily total.

Detect scarcity collisions with exact load/renewables/weather peaks.

Priority: S

## W24A-E15 — Planned-Outage Capacity Margin

ERCOT publishes planned-outage capacity-margin limits over short and long horizons.

Candidate:
requested/approved planned outages
relative to
system's permissible outage headroom.

Priority: A+

## W24A-E16 — Planned-to-Forced Reclassification

ERCOT notes that a planned outage extended beyond its expected end may be reclassified as forced.

Track:
PLANNED
-> EXTENDED
-> FORCED.

This can reveal unexpected maintenance failure/restart delay.

Priority: S

## W24A-E17 — Outage Reporting-Lag State

ERCOT notes outage information may be entered after an outage occurred.

Store:
physical start if available
source publication/first seen
later classification updates.

Never backdate public availability.

Priority: S methodology/edge hybrid

## W24A-E18 — Resource-Type Forced-Outage Hazard

Estimate forced outage probability conditional on:
resource class
season
temperature
age proxy
recent run intensity
weather.

Use aggregate public data where unit identity is not public.

Priority: A

## W24A-E19 — CAISO Unit-Level Non-Operational Snapshot

Primary source:
CAISO Curtailed and Non-Operational Generator report.

CAISO posts daily current-trade-date snapshots around 8:30 a.m. PT with unit/resource, planned/forced type, curtailment timing/MW, PMax, NQC, zone and balancing area where available.

Priority: S-

## W24A-E20 — CAISO Curtailment Fraction

Candidate:
curtailed MW
/
resource PMax

plus:
outage type
duration
zone
NQC importance.

Priority: A+

## W24A-E21 — Unit Outage Stacking

CAISO can report multiple outage breakpoints for a resource.

Reconstruct exact time-varying curtailed MW instead of summing daily records naively.

Priority: A+

## W24A-E22 — Current-vs-Prior-Trade-Date Reality Gap

CAISO publishes current snapshot and prior-trade-date retrospective report.

Use later report to validate what actually occurred, not as contemporaneous information.

Priority: A

## W24A-E23 — Thermal Forced-Outage Scarcity

Across ISOs:
forced thermal MW
× net load
× transmission constraint
× fuel availability.

Priority: S

## W24A-E24 — Renewable Outage × Forecast Error

A renewable outage matters differently from weather-driven low output.

Separate:
reported outage/derate
from
meteorological generation shortfall.

Priority: A

## W24A-E25 — Outage × Transmission Collision

Fuse:
W24A generation loss
+ W23T grid transport stress.

Mechanism:
losing generation on the import-constrained side of a bottleneck can have nonlinear local impact.

Priority: S

## W24A-E26 — Outage × Gas Transport Collision

Fuse:
forced gas-fired generation loss
+ W22G gas-pipeline constraint.

Question:
is the region losing generation while remaining gas units also face fuel-transport scarcity?

Priority: S

## W24A-E27 — Outage × Weather Stress

Extreme temperature can simultaneously:
raise load
increase forced outages
constrain fuel
reduce equipment capability.

Model common cause before claiming one-way causality.

Priority: S-

## W24A-E28 — Restart / Recovery Hazard

Estimate probability that forced outage MW returns within:
1h
6h
24h
72h.

Use outage-stack revisions and unit reports where public.

Priority: S

## W24A-E29 — Generation Substitution Quotient

GSQ =
unexpected unavailable MW
/
available replacement MW from
local generation + imports + storage + demand response.

Priority: S

## W24A-E30 — Dispatchable Availability State Vector

Combine:
FORCED_OUTAGE_MW
PLANNED_OUTAGE_MW
EMERGENCY_MAX_DEPENDENCE
RESERVE_HEADROOM
RESTART_HAZARD
TRANSMISSION_IMPORT_HEADROOM
FUEL_AVAILABILITY.

Output:
ABUNDANT
NORMAL
TIGHT
FRAGILE
CRITICAL.

Priority: S

## W24A-E31 — Structural Forced-Outage Prior

Use NERC GADS aggregated forced-outage/derate statistics as a slow structural prior by fuel/unit class.

Do not use GADS as a live trigger; reporting/publication is too slow.

Priority: B+/validation

## W24A-E32 — Availability Surprise to Fuel Demand

Research chain:
unexpected generation loss
-> replacement dispatch by technology
-> incremental fuel burn
-> local fuel/basis response.

Only test commodity futures after replacement dispatch is validated.

Priority: S research architecture

## Highest-priority W24A tests

1. W24A-E02 Forced-Outage Surprise
2. W24A-E07 Available-vs-Committed Capacity Gap
3. W24A-E09 Projected Peak Reserve Compression
4. W24A-E10 ERCOT Five-Minute Outage Pulse
5. W24A-E13 ERCOT Hourly 168-Hour Outage Surface
6. W24A-E16 Planned-to-Forced Reclassification
7. W24A-E23 Thermal Forced-Outage Scarcity
8. W24A-E25 Outage × Transmission Collision
9. W24A-E29 Generation Substitution Quotient
10. W24A-E30 Dispatchable Availability State Vector
