# Wave 14I — Critical Infrastructure Substitution & Chokepoints

Namespace: **W14I**

Thesis: abrupt loss or restriction of critical infrastructure changes the marginal resource that must replace it. The most useful signal may be the substitution requirement, not the outage itself. This wave targets nuclear generation, reservoir/hydropower flexibility, Panama Canal capacity, and Great Lakes navigation.

All candidates are research hypotheses only.

## W14I-E01 — NRC Daily Nuclear Output Shock

Primary source:
U.S. Nuclear Regulatory Commission Power Reactor Status Reports.

Status:
DAILY PUBLIC.

NRC reports unit-level power percentage and status. The NRC states status data are collected between roughly 4 a.m. and 8 a.m. ET each day.

Feature:
actual power
-
expected power from prior status/refueling schedule.

Classify:
NORMAL
COASTDOWN
PLANNED_OUTAGE
FORCED_DOWNPOWER
FORCED_OUTAGE
RESTART
RAMP_UP.

Priority: S

## W14I-E02 — Reactor Scram / Trip First Alert

Primary source:
NRC Event Notification Reports.

Event reports contain:
event time,
notification time,
facility/unit,
initial/current reactor power/mode,
reportability category,
event narrative and updates.

Mechanism:
An unexpected reactor trip can remove a large block of baseload generation abruptly.

Priority: S

## W14I-E03 — Event-Notification-to-Daily-Status Gap

Compare:
intraday NRC event notification
versus
next NRC daily reactor-status report.

Question:
How much information becomes actionable before the next morning's systemwide status snapshot?

This is an availability-timing study, not an assumption that all events publish instantly.

Priority: A+

## W14I-E04 — Planned vs Forced Nuclear Outage Separation

Planned refueling/coastdown should not be modeled as surprise scarcity.

Build:
expected planned outage calendar
versus
unexpected scram/trip/derate.

Candidate:
unexpected_MW_loss.

Priority: S

## W14I-E05 — Regional Nuclear Generation Deficit

Map each reactor to its balancing authority/RTO and nameplate capacity.

Feature:
sum(unexpected unavailable nuclear MW)
/
regional load.

Condition on:
reserve margin,
weather,
interchange,
renewables,
gas generation availability.

Priority: S

## W14I-E06 — Nuclear-to-Gas Substitution Pressure

Mechanism:
When nuclear generation falls unexpectedly, replacement energy may come from natural gas, imports, coal, storage or demand response depending on the region/state.

Candidate:
unexpected_nuclear_MW_loss
× marginal_gas_share_probability
× expected_outage_duration.

First validate against actual regional fuel mix and gas burn before NG futures.

Priority: S

## W14I-E07 — Nuclear Outage × Grid Scarcity Collision

Fuse:
NRC forced outage
+ EIA/PJM/ERCOT load residual
+ reserve state
+ neighboring interchange
+ generator outage state.

Hypothesis:
the same nuclear outage has much larger marginal price/fuel impact during low reserve/high load states.

Priority: S

## W14I-E08 — Reactor Restart Hazard

Model:
P(restart within 1d/3d/7d)
and
expected ramp profile.

Inputs:
outage reason,
planned/forced status,
event updates,
historical unit restart behavior,
maintenance/refueling context.

Potential edge:
market may price outage onset better than recovery duration.

Priority: A+

## W14I-E09 — NRC Degraded-Condition Severity Graph

Not all NRC event notifications are generation losses.

Separate:
SCRAM/TRIP
LOSS_OF_OFFSITE_POWER
DEGRADED_SAFETY_SYSTEM
MAINTENANCE_FINDING
NON-POWER-RELEVANT EVENT.

Only generation-relevant events enter energy models.

Priority: A

## W14I-E10 — Reservoir Storage Flexibility State

Primary source:
Bureau of Reclamation RISE.

Status:
PUBLIC; cadence varies by item, many key western reservoir series update daily.

RISE time series can include:
storage,
elevation,
inflow,
total release,
powerplant release,
spillway/outlet release.

Feature:
usable storage percentile
× seasonal inflow
× downstream obligation
× forecast demand.

Priority: A+

## W14I-E11 — Hydro Dispatch Buffer

Concept:
stored water is not equivalent to immediately dispatchable hydropower.

Estimate:
powerplant-capable release headroom
relative to
recent release
storage/elevation
seasonal constraints.

Output:
HIGH_FLEX / NORMAL / CONSTRAINED / WATER_SCARCITY.

Priority: A+

## W14I-E12 — Hydro-to-Gas Substitution State

Fuse:
reservoir/hydro flexibility
+ regional load
+ gas generation share
+ renewable output.

Hypothesis:
gas demand sensitivity to heat/load is higher when hydro flexibility is constrained.

Priority: S-

## W14I-E13 — Reservoir Recovery / Drawdown Velocity

Track:
storage percentile,
inflow surprise,
release rate,
drawdown acceleration,
recovery half-life.

Avoid raw level-only signals.

Priority: A

## W14I-E14 — Western Water-Power Constraint Graph

Graph:
reservoir
-> hydropower plant
-> balancing region
-> agricultural/municipal release obligations
-> regional generation substitutes.

Goal:
distinguish water scarcity from actual power scarcity.

Priority: A+

## W14I-E15 — Panama Canal Slot Capacity State

Primary source:
Panama Canal Authority Advisories to Shipping and booking/transit pages.

Status:
EVENT-DRIVEN / OPERATIONAL.

ACP advisories can announce explicit future changes to:
- daily Panamax/Neopanamax transit slots
- booking-period slot allocation
- vessel-category allocation
- auction availability.

Feature:
future slot capacity
relative to
normal capacity and observed demand.

Priority: S

## W14I-E16 — Panama Draft Constraint State

ACP can alter maximum authorized Neopanamax draft as Gatun Lake/watershed conditions change.

Economic mechanism:
reduced draft can force less cargo per transit, cargo offload/reload, alternative routing or scheduling changes.

Candidate:
effective cargo-capacity loss
=
draft_restriction
× affected vessel class
× route/cargo exposure.

Priority: S

## W14I-E17 — Canal Reservation Scarcity / Waiting State

ACP's reservation system is the guaranteed-transit mechanism during constrained periods; unreserved vessels may wait depending on capacity/demand.

Research:
- projected booking availability
- vessels waiting
- booked vs unbooked pressure
- slot utilization
- rule/auction changes.

Priority: S-

## W14I-E18 — Panama Capacity Revision Velocity

Track every advisory vintage:
future daily slots
maximum draft
effective dates
booking rules
postponements/reversals.

Feature:
change in expected future canal throughput, not only current level.

Priority: S

## W14I-E19 — Segment-Specific Canal Scarcity

ACP booking allocation can differ by market segment including container, LNG, LPG, vehicle/RoRo, bulkers and others.

Build segment-specific pressure rather than treating one canal slot as economically identical to another.

Targets:
LNG/LPG freight, grains/bulk, container trade, vehicle logistics.

Priority: A+

## W14I-E20 — Panama Route Substitution Pressure

Graph:
Panama constraint
-> Suez/Cape/other route
-> voyage distance
-> fuel use
-> vessel-days consumed
-> freight capacity.

The signal is the extra vessel-time/capacity required to bypass the constraint.

Priority: S

## W14I-E21 — Great Lakes Daily Ice Constraint

Primary:
NOAA GLERL / U.S. National Ice Center.

Status:
DAILY during ice season.

NOAA provides daily Great Lakes ice concentration data and machine-readable services/files.

Feature:
ice concentration
× channel geography
× vessel route
× icebreaker requirement
× current lock/port availability.

Priority: A

## W14I-E22 — Great Lakes Ice Navigation State

Use USNIC ice type/floe information and Coast Guard/USACE operational context.

States:
OPEN
ASSISTANCE_LIKELY
ICEBREAKER_DEPENDENT
SEVERE_CONSTRAINT
LOCK_CLOSED/SEASONAL_SHUTDOWN.

Do not infer commerce loss from ice cover alone.

Priority: A+

## W14I-E23 — Great Lakes Iron-Ore / Steel Logistics Risk

Graph:
upper-lake ore origin
-> vessel route
-> Soo Locks
-> lower-lake steel mill.

Fuse:
ice state
+ lock status
+ vessel flow
+ stockpile seasonality
+ steel/ore demand.

Important negative evidence:
GAO found aggregate ice coverage was not generally associated with selected regional economic indicators, partly because operators stockpile and adapt. This makes substitution/stockpile controls mandatory.

Priority: A

## W14I-E24 — Critical Infrastructure Substitution Quotient

General form:

CISQ =
unexpected capacity loss
/
available substitute capacity.

Examples:
nuclear MW loss / gas-import-storage reserve
hydro shortfall / thermal reserve
Panama cargo capacity loss / alternate-route vessel capacity
Great Lakes restriction / inventory + rail alternatives.

Priority: S

## W14I-E25 — Constraint Announcement vs Physical Realization

For every infrastructure constraint separate:
announcement
effective time
physical utilization
actual backlog/scarcity
recovery.

Examples:
Panama advisory can precede future slot reduction.
NRC event notification can precede daily status.
Reservoir trend can precede hydro scarcity.

Priority: S research architecture

## Highest-priority W14I tests

1. W14I-E02 Reactor Scram / Trip First Alert
2. W14I-E05 Regional Nuclear Generation Deficit
3. W14I-E06 Nuclear-to-Gas Substitution Pressure
4. W14I-E07 Nuclear Outage × Grid Scarcity
5. W14I-E10 Reservoir Storage Flexibility
6. W14I-E12 Hydro-to-Gas Substitution
7. W14I-E15 Panama Canal Slot Capacity
8. W14I-E16 Panama Draft Constraint
9. W14I-E20 Panama Route Substitution
10. W14I-E24 Critical Infrastructure Substitution Quotient
