# Wave 7 Discoveries

Wave 7 concentrates on infrastructure capacity constraints and forced substitution: nuclear availability, Panama Canal water/transit capacity, Western reservoirs/hydropower, refinery throughput, LNG infrastructure, and multi-chokepoint logistics.

## E147 — NRC Nuclear Availability Shock

Source:
U.S. Nuclear Regulatory Commission daily Power Reactor Status.

Status:
LIVE weekday/daily operating data.

Official NRC facts:
- unit-level power percentage is collected each morning, generally between 4 a.m. and 8 a.m. ET
- raw status data cover the recent rolling period
- some reports include change/scram indicators
- detailed reason/status information can appear later

Mechanism:
A nuclear derate/outage removes low-marginal-cost baseload generation and can force substitution from gas/coal/imported power depending on region and system state.

Features:
- MW-equivalent lost vs prior day
- unexpected derate vs scheduled outage expectation
- regional nuclear availability
- duration/hazard of restart
- fleet-wide availability percentile

Priority: S-

## E148 — Nuclear-to-Gas Substitution Pressure

Fuse:
NRC unit power
+ plant nameplate capacity
+ ISO/RTO load
+ renewable output/forecast
+ gas generation
+ regional pipeline/gas basis.

Candidate:
incremental gas burn required to replace unavailable nuclear MW.

Do not assume one-for-one substitution; account for imports, coal, hydro, storage and congestion.

Priority: S

## E149 — Nuclear Outage Geographic Basis Map

Map each reactor to:
ISO/RTO zone,
gas pipeline/basis region,
transmission interfaces,
replacement generation stack.

Question:
Does the same 1 GW nuclear outage have different gas/power effects depending on local substitute stack and congestion?

Priority: A+

## E150 — Panama Canal Capacity State

Source:
Panama Canal Authority (ACP) official advisories, booking pages, water indicators and operations summaries.

Status:
LIVE/forward operational data.

Official ACP sources expose:
- current/projected Gatun Lake levels
- official maximum draft
- booking slots
- projected booking-slot availability
- vessels waiting
- maintenance outages
- market-segment slot allocation
- advisories with future effective dates

State dimensions:
water
× draft
× slots
× lock maintenance
× waiting queue
× vessel mix.

Priority: S

## E151 — Panama Forward Transit Supply Curve

Mechanism:
ACP often announces capacity changes before their booking/effective date.

Build a forward curve:
expected daily slots by date and vessel class,
known lock outages,
draft limits,
reservation rules.

Research:
Does change in expected future transit capacity lead freight rerouting/rates, LNG/LPG flows, grains or containerized trade?

Priority: S

## E152 — Panama Draft-to-Cargo Capacity Shock

A reduction in maximum draft can reduce cargo per ship even if transit count is unchanged.

Features:
- draft delta
- vessel-class exposure
- deadweight/cargo sensitivity
- number of affected vessel classes
- expected tonnage displaced
- alternative-route cost

Key principle:
transit slots and cargo throughput are separate capacity dimensions.

Priority: S-

## E153 — Panama Water Forecast Revision

Official water-level projection vintages can change before formal capacity action.

Feature:
projection revision
-> expected future draft/slot probability.

Store every projection vintage and ACP advisory.

Goal:
test whether hydrological expectation changes lead operational restrictions before conventional freight data.

Priority: A+

## E154 — Canal Booking Scarcity / Queue Pressure

Inputs:
available/used booking slots,
auctioned slots where published,
vessels waiting,
expected slots,
maintenance schedule.

Candidate:
booking scarcity = demand for guaranteed passage / forward slot supply.

Output:
NORMAL / TIGHT / QUEUED / DISLOCATED.

Priority: A+

## E155 — Panama Commodity Exposure Graph

Map route dependence by cargo:
LNG/LPG,
grain,
container,
vehicle,
bulk,
energy products.

Research:
Canal constraint -> route substitution -> voyage time -> shipping capacity withdrawal -> freight/commodity basis.

Do not apply a generic "Panama bullish" sign.

Priority: A

## E156 — Western Reservoir / Hydropower State

Source:
Bureau of Reclamation RISE API.

Status:
LIVE machine-readable time series for participating datasets.

Official RISE supports queryable time-series JSON and reservoir/storage data across Western U.S. facilities.

Features:
- storage percentile
- elevation
- inflow/outflow
- release surprise
- seasonal snow/water context
- hydropower facility exposure

Priority: A+

## E157 — Hydro-to-Gas Substitution Pressure

Fuse:
reservoir/storage
+ hydro generation
+ load
+ wind/solar
+ transmission imports
+ gas generation.

Question:
When hydro availability is lower than expected, how much marginal gas burn is induced in CAISO/Western systems?

Priority: S-

## E158 — Water Scarcity Multi-Market Graph

Reservoir scarcity can affect:
hydropower,
irrigation/agriculture,
municipal supply,
river navigation,
industrial users.

Create separate exposure channels instead of one drought variable.

Priority: A

## E159 — Refinery Throughput Shock

Source:
EIA Weekly Petroleum Status Report.

Status:
LIVE weekly scheduled.

Official data include:
crude inputs,
gross inputs,
operable capacity,
utilization,
PADD-level detail,
product production/stocks.

Candidate:
regional refinery throughput surprise after controlling for seasonality, maintenance and storm state.

Effects:
crude demand,
gasoline/distillate supply,
crack spreads,
regional inventories.

Priority: A+

## E160 — Refinery Demand Offset During Supply Shock

Example:
A hurricane may shut crude production AND refineries.

Build:
net crude balance impact =
upstream production loss
-
refinery crude-demand loss
-
export/terminal disruption adjustments.

This prevents one-sided storm heuristics.

Priority: S

## E161 — LNG Project Ramp / Capacity State

Sources:
FERC eLibrary project status reports,
DOE/FERC authorizations,
EIA LNG/export data,
terminal/operator public data where official.

FERC project filings can provide construction/status reports with filed/posted/received timestamps.

Use:
slow/medium horizon capacity ramp and outage confirmation.

Do not label biweekly construction reports as real-time operations.

Priority: A-

## E162 — LNG Capacity-to-Basin Transmission

Graph:
terminal capacity
-> feedgas demand
-> pipeline constraint
-> producing basin
-> regional gas basis
-> Henry Hub.

Research:
capacity start-up/ramp or outage changes the marginal value of pipeline takeaway.

Priority: A+

## E163 — Infrastructure Maintenance Collision Calendar

Fuse forward:
Panama lock maintenance,
refinery seasonal maintenance,
nuclear planned outages,
pipeline maintenance where public,
grid outages,
port/channel maintenance.

Question:
Do overlapping planned constraints create nonlinear vulnerability to an otherwise ordinary shock?

Priority: S-

## E164 — Global Chokepoint Capacity Graph

Nodes:
Panama Canal,
major ports,
Mississippi locks,
rail corridors,
pipelines,
LNG terminals.

Edges:
cargo/commodity route substitution.

State:
available capacity,
queue,
maintenance,
weather,
recovery rate.

Goal:
measure where global logistics has the least spare capacity before a shock occurs.

Priority: S research architecture

## E165 — Spare-Capacity Fragility Index

General concept:
fragility = expected demand / remaining adaptive capacity.

Applied to:
canal slots,
refinery capacity,
power generation,
pipeline takeaway,
port throughput,
warehouse delivery.

A small shock near 100% utilization can matter more than a larger shock in a slack system.

Priority: S

## E166 — Infrastructure Recovery Half-Life

After outage/constraint, estimate restoration path:
- initial loss
- 50% recovery
- 90% recovery
- queue clearance
- persistent damage

Potential edge:
market may correctly price the initial shock but misprice restoration speed.

Priority: A+

## E167 — Chokepoint Forecast Error

For forward operational data:
actual constraint - previously forecast constraint.

Examples:
actual Gatun water vs projection,
actual reactor availability vs expected maintenance,
actual refinery utilization vs seasonal expectation.

Research whether forecast-error, not level, drives repricing.

Priority: A+

## E168 — Forced-Substitution Tensor

Represent a capacity loss as:
lost_source
× substitute_1 capacity/cost
× substitute_2
× network congestion
× inventory buffer
× response time.

This is a reusable framework across power, gas, freight and commodities.

Priority: S architecture

## Highest-priority Wave 7 tests

1. E148 Nuclear-to-Gas Substitution Pressure
2. E150 Panama Canal Capacity State
3. E151 Panama Forward Transit Supply Curve
4. E152 Panama Draft-to-Cargo Shock
5. E157 Hydro-to-Gas Substitution
6. E160 Refinery Demand Offset
7. E164 Global Chokepoint Capacity Graph
8. E165 Spare-Capacity Fragility Index
9. E166 Infrastructure Recovery Half-Life
10. E168 Forced-Substitution Tensor
