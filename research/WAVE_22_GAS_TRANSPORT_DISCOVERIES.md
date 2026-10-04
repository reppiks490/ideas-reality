# Wave 22G — Gas Transport Constraint & Nomination Exhaust

Namespace: **W22G**

Thesis: natural-gas markets are constrained not only by production and storage, but by the physical transport network and the contractual/scheduling machinery that moves gas through it. Interstate and major non-interstate pipelines publish unusually rich operational exhaust: scheduled volumes, available capacity, critical notices, maintenance, force majeure, operational flow orders, linepack conditions, capacity releases, and nomination-cycle changes.

All candidates are research hypotheses only. Claude owns implementation.

## W22G-E01 — Pipeline Critical-Notice Pulse

Primary sources:
interstate pipeline Informational Postings / EBBs.

Build a normalized event stream:
MAINTENANCE
CONSTRAINT
FORCE_MAJEURE
OFO
CRITICAL_DAY
CAPACITY_OFFERING
OPEN_SEASON
OTHER.

Store post/effective/end times, affected points/segments, flow direction and notice lineage.

Priority: S

## W22G-E02 — Public Linepack Draft State

Some operators publish linepack level and day-over-day change in operational notices.

Example class:
current system linepack
minus
prior gas-day start linepack.

State:
PACKING
BALANCED
DRAFTING
SEVERE_DRAFT.

Mechanism:
linepack is the short-horizon physical buffer between receipts and deliveries.

Priority: S

## W22G-E03 — Linepack Cause Decomposition

Parse operator-stated cause:
deliveries above schedule
supply underperformance
weather/load
maintenance
compressor outage
storage injection/withdrawal
other.

Question:
does cause predict persistence and basis impact differently?

Priority: A+

## W22G-E04 — Operational Flow Order Severity

Normalize OFO states:
ADVISORY
STRAINED_OPERATING_CONDITION
SCHEDULING_OFO
IMBALANCE_OFO
CRITICAL_DAY_I
CRITICAL_DAY_II
METER_SPECIFIC
HOURLY_OFO
OTHER.

Capture tolerance, penalty and affected zone/points.

Priority: S

## W22G-E05 — OFO Directionality

Separate:
SHORTAGE / DUE_FROM shipper
versus
SURPLUS / DUE_TO shipper.

Economic meaning differs:
undersupply pressure can imply scarce gas/linepack,
while oversupply can indicate weak demand or downstream restriction.

Priority: S

## W22G-E06 — OFO Escalation Hazard

Model:
notice
-> tighter tolerance
-> broader geography
-> higher penalty
-> critical-day escalation
-> relief/lift.

Output:
probability of escalation within next nomination cycle/gas day.

Priority: S

## W22G-E07 — Constraint Capacity Delta

Official notices can provide explicit before/after or available-throughput quantities.

Feature:
new_available_capacity
-
prior_available_capacity

normalized by:
historical utilization,
design capacity,
firm scheduled demand.

Priority: S

## W22G-E08 — Directional Capacity Asymmetry

A maintenance event can constrain one direction while leaving reverse flow unaffected.

Represent capacity by:
segment
direction
cycle
priority class.

Do not treat pipeline capacity as a scalar.

Priority: A+

## W22G-E09 — Estimated Shipper-Cut Pressure

Some critical notices publish estimated percentage cuts based on historical utilization and anticipated nominations.

Research:
operator-estimated cut %
versus
later realized scheduled-flow reduction.

Priority: A+

## W22G-E10 — Planned Maintenance Constraint Calendar

Pipeline operators publish maintenance schedules and revisions, sometimes months ahead.

Build:
planned start/end
expected available capacity
affected path
revision history.

Use as expected capacity, not surprise.

Priority: S-

## W22G-E11 — Maintenance Revision Surprise

Feature:
change in outage start/end
+
change in available capacity
+
change in affected direction/points.

Unexpected extension or deeper capacity reduction may be more informative than initial planned maintenance.

Priority: S

## W22G-E12 — Force-Majeure Transport Shock

Unplanned compressor/equipment failure can trigger force-majeure notices with immediate capacity restrictions and uncertain return-to-service windows.

Build:
capacity loss
estimated restoration range
revision velocity
affected firm/interruptible service.

Priority: S

## W22G-E13 — Compressor-Station Criticality Graph

Map compressor station:
-> pipeline segment
-> upstream supply basin
-> downstream demand centers
-> storage
-> LNG/power/citygate points.

Feature:
lost station throughput
/
available reroute capacity.

Priority: S

## W22G-E14 — Gas-Day Nomination Cycle State

FERC Order 809 standardized key nomination deadlines:
Timely at 1:00 p.m. CCT,
Evening at 6:00 p.m. CCT,
Intraday 1 at 10:00 a.m. CCT,
Intraday 2 at 2:30 p.m. CCT,
Intraday 3 at 7:00 p.m. CCT.

Track each operational notice relative to the next available scheduling cycle.

Priority: S

## W22G-E15 — Constraint Timing vs Nomination Opportunity

Candidate:
time from notice publication
to
next nomination deadline/effective transport adjustment.

Hypothesis:
the same constraint has different price/flow impact depending on how much scheduling flexibility remains.

Priority: S

## W22G-E16 — Scheduled-Volume Shock

FERC rules require major non-interstate pipelines to post daily scheduled-flow information at qualifying points; interstate operators also publish extensive capacity/scheduling data on their websites.

Build point-level:
scheduled receipts
scheduled deliveries
design/operational capacity where available
day-over-day revision.

Priority: S-

## W22G-E17 — Operationally Available Capacity Pressure

Where operators publish OAC:
OAC / design capacity
and
scheduled quantity / OAC.

State:
OPEN
TIGHT
FULLY_SUBSCRIBED
CONSTRAINED
CURTAILED.

Priority: S

## W22G-E18 — Firm-vs-Interruptible Rationing State

Many notices identify which service priorities are limited:
primary firm
secondary firm
interruptible
no-notice swing
park/loan.

Constraint severity is higher when restrictions reach higher-priority firm service.

Priority: A+

## W22G-E19 — Capacity Release Scarcity Auction

FERC-regulated capacity release allows holders of firm rights to release transport capacity through public posting/bidding mechanisms.

Research:
offered MDQ
bid rate
term
path
awarded quantity
competition
discount/premium to tariff cap.

Priority: S-

## W22G-E20 — Released-Capacity Price of Scarcity

Candidate:
awarded reservation rate
relative to
maximum tariff rate
and
recent comparable path releases.

Interpretation:
transport rights can acquire option-like value when physical path capacity tightens.

Priority: A+

## W22G-E21 — Right-of-First-Refusal Capacity Retention

ROFR postings expose expiring/available firm transport capacity and incumbent retention decisions.

Research:
retained vs relinquished capacity
by path/zone/season.

Potentially useful as a forward view of transport demand expectations.

Priority: A

## W22G-E22 — Park-and-Loan Flexibility State

Some pipelines offer interruptible Park and Loan services only when operating conditions permit.

Availability/suspension can proxy for system flexibility.

State:
PAL_OPEN
PAL_LIMITED
PAL_SUSPENDED.

Priority: A+

## W22G-E23 — Storage Transport Access State

FERC rules require equal/timely information relevant to availability of transportation services, including storage-related capacity.

Research:
injection/withdrawal transport constraints
× storage inventory
× weather/load.

Priority: A+

## W22G-E24 — No-Notice Service Historical Validator

FERC requires interstate pipelines to post no-notice transportation flow estimates after gas flow, with later updates.

Because timing is delayed, use this as:
historical validation of surprise demand/flexibility,
not same-day live trigger.

Priority: B+/validation

## W22G-E25 — LNG Feedgas Path Constraint

Graph:
upstream basin
-> interstate pipeline
-> compressor/segment
-> LNG terminal delivery point.

Fuse:
scheduled flow
capacity
maintenance/OFO
terminal operational state.

Question:
is feedgas reduction caused by LNG terminal demand or upstream transport constraint?

Priority: S

## W22G-E26 — Gas-Fired Power Constraint Collision

Fuse:
pipeline constraint/OFO
+ gas-fired generator regional load
+ ISO dispatch/reserve state
+ weather.

Hypothesis:
gas-basis and power-price sensitivity rise when transport is constrained during high gas-generator dependence.

Priority: S

## W22G-E27 — Citygate Cold-Weather Scarcity

Map:
pipeline path
-> LDC/citygate
-> weather-driven heating load
-> storage/local supply
-> OFO/critical notices.

Measure shortage pressure at the delivery system rather than national gas balance.

Priority: S-

## W22G-E28 — Constraint × Basis Reality Check

For each physical path, pair operational constraint state with the most relevant spot/basis location.

Promotion requires:
constraint timing
-> flow/capacity effect
-> local basis response.

Do not jump directly to Henry Hub direction.

Priority: S

## W22G-E29 — Constraint Propagation Graph

A constrained segment can redistribute flow to:
alternate pipelines
storage
different receipt basins
LNG/power load curtailment
regional basis.

Build path-specific network propagation.

Priority: S

## W22G-E30 — Gas Transport Substitution Quotient

GTSQ =
lost transport capacity
/
available alternate transport + storage + linepack flexibility.

This is the transport-network version of the repo's broader substitution-capacity principle.

Priority: S

## W22G-E31 — Pipeline Flexibility State Vector

Combine:
LINEPACK
OFO_SEVERITY
OAC
MAINTENANCE
FORCE_MAJEURE
PAL_AVAILABILITY
STORAGE_ACCESS
CAPACITY_RELEASE_SCARCITY
NOMINATION_FLEXIBILITY.

Output:
ABUNDANT
NORMAL
TIGHT
STRESSED
CRITICAL.

Priority: S

## Highest-priority W22G tests

1. W22G-E02 Public Linepack Draft State
2. W22G-E04 Operational Flow Order Severity
3. W22G-E06 OFO Escalation Hazard
4. W22G-E07 Constraint Capacity Delta
5. W22G-E12 Force-Majeure Transport Shock
6. W22G-E15 Constraint Timing vs Nomination Opportunity
7. W22G-E17 Operationally Available Capacity Pressure
8. W22G-E20 Released-Capacity Price of Scarcity
9. W22G-E25 LNG Feedgas Path Constraint
10. W22G-E30 Gas Transport Substitution Quotient
