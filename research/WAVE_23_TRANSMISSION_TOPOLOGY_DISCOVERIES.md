# Wave 23T — Transmission Topology & Congestion Mechanics

Namespace: **W23T**

Thesis: electric systems can have adequate aggregate generation and still become economically stressed because power cannot move through the network. Binding transmission constraints, contingencies, outages, interface limits, and derates are direct measurements of transport scarcity inside the grid.

All candidates are research hypotheses only. Claude owns implementation.

## W23T-E01 — PJM Real-Time Binding Constraint Pulse

Primary source:
PJM Data Miner Real-Time Marginal Value / Transmission Limits.

PJM publishes binding transmission constraints at five-minute granularity with monitored facility, contingency facility, shadow price, transmission constraint penalty factor, and limit-control percentage.

Priority: S

## W23T-E02 — Constraint Shadow-Price Intensity

Feature:
absolute shadow price
× duration
× recurrence
× affected topology breadth.

Interpretation:
marginal economic value of relaxing a constraint, not a direct directional asset signal.

Priority: S

## W23T-E03 — Limit-Control Stress

PJM publishes limit-control percentage for relevant constraints.

Research:
how close operator control is set relative to the physical/emergency limit and whether tightening precedes stronger congestion.

Priority: A+

## W23T-E04 — Monitored-vs-Contingency Pair Graph

Represent each event as:
MONITORED_FACILITY
under
CONTINGENCY_FACILITY.

This is more informative than constraint name alone because the same line can bind under different contingencies.

Priority: S

## W23T-E05 — Real-Time Constraint Persistence

Measure:
first bind
continuous bind duration
intermittent recurrence
shadow-price peak
time-to-clear.

Priority: A+

## W23T-E06 — Day-Ahead-to-Real-Time Constraint Surprise

PJM publishes day-ahead transmission constraints and real-time binding constraints.

States:
EXPECTED_BIND
UNEXPECTED_REALTIME_BIND
EXPECTED_BUT_NOT_REALIZED
SEVERITY_UPSHIFT
SEVERITY_DOWNSHIFT.

Priority: S

## W23T-E07 — Unexpected Transmission Scarcity

Candidate:
real-time constraint intensity
-
day-ahead expected constraint intensity.

This isolates network surprise from known day-ahead congestion.

Priority: S

## W23T-E08 — PJM Transfer Headroom

PJM publishes RTO transfer limits and actual transfers.

Feature:
headroom =
transfer limit
-
actual transfer.

Track pre- and post-contingency transfer areas separately.

Priority: S-

## W23T-E09 — Transfer-Headroom Collapse

Research:
rate of headroom compression
× load
× generation outage
× neighboring interchange.

Priority: A+

## W23T-E10 — Transmission Outage Ticket State

PJM OASIS/eDART exposes current/future and historical transmission outage information for non-market-sensitive outages, including XML download capability.

Build:
PROPOSED
APPROVED
ACTIVE
COMPLETED
CANCELLED
EMERGENCY where public semantics permit.

Priority: S-

## W23T-E11 — Planned-vs-Forced Transmission Loss

Separate:
scheduled maintenance
from
unexpected/emergency outage.

Only residual/unplanned loss belongs in surprise research.

Priority: S

## W23T-E12 — Outage-to-Constraint Conversion Hazard

Question:
Given a transmission outage/derate, what is the probability it produces a binding market constraint?

Inputs:
facility voltage,
topology,
load,
generation pattern,
neighbor outages,
weather.

Priority: S

## W23T-E13 — Constraint-to-Outage Attribution

The inverse problem:
when a new constraint binds, identify whether it is explained by a known transmission outage, generation outage, weather, or load shift.

Priority: A+

## W23T-E14 — ERCOT SCED Constraint Pulse

Primary source:
ERCOT NP6-86-CD.

Public report includes:
constraint/contingency
overloaded element
from/to station and kV
shadow price
maximum shadow price
element limit
flow/value pair
violation amount.

Priority: S

## W23T-E15 — ERCOT Flow-to-Limit Ratio

Candidate:
abs(flow) / abs(limit)

conditioned on:
contingency
voltage class
constraint type.

Track approach to binding and persistence after bind.

Priority: S

## W23T-E16 — ERCOT Constraint Penalty Proximity

Compare realized shadow price to the applicable maximum shadow price / penalty curve.

Feature:
shadow_price / max_shadow_price.

High values may identify constraints with limited economically available redispatch.

Priority: A+

## W23T-E17 — ERCOT Transmission Outage Stack

Primary source:
ERCOT Consolidated Transmission Outage Report.

Fuse proposed, approved/accepted, withdrawn and rejected outages into a point-in-time outage schedule.

Priority: A+

## W23T-E18 — Outage-Stack Congestion Risk

Estimate topology-adjusted simultaneous outage burden:
outage MW/path importance
× overlap
× load forecast
× renewable/generator availability.

Priority: S-

## W23T-E19 — CAISO Real-Time Constraint Pulse

Primary source:
CAISO OASIS.

CAISO publishes shadow prices for transmission interfaces, intertie constraints, branches and nomograms in day-ahead and real-time market processes.

Priority: S-

## W23T-E20 — CAISO Transmission Outage Clock

CAISO tariff/public documentation specifies scheduled outage-information publications before operating day and intraday updates prior to the relevant trading hour.

Research the information arrival sequence separately from physical outage start.

Priority: A+

## W23T-E21 — Nomogram Constraint State

Some critical transmission limits are represented by multi-element nomograms rather than one line.

State:
ACTIVE
APPROACHING
BINDING
RELEASED.

Do not reduce nomograms to a single guessed asset.

Priority: A

## W23T-E22 — Cross-ISO Constraint Breadth

Construct comparable measures across PJM/ERCOT/CAISO:
number binding
aggregate shadow-price intensity
duration
unexpected-vs-day-ahead share
outage overlap.

Avoid pooling raw shadow prices without market-specific normalization.

Priority: A+

## W23T-E23 — Constraint Recurrence Memory

Certain facilities/contingencies bind repeatedly under similar load/generation states.

Estimate recurrence probability conditional on:
hour
season
weather
outage stack
renewables
load.

Priority: A+

## W23T-E24 — Congestion Recovery Half-Life

After a transmission shock:
peak shadow price
constraint count
price separation
50% normalization
full normalization.

Priority: A+

## W23T-E25 — Generator Redispatch Footprint

For a new constraint, infer which generation regions/types increase/decrease output because of topology.

Validate from dispatch/fuel mix before mapping to fuel demand.

Priority: S-

## W23T-E26 — Transmission × Gas Burn Collision

Fuse:
W23T constraint state
+ W22G gas transport state
+ regional gas-fired generation.

A grid constraint can require local gas generation exactly when gas transport is also constrained.

Priority: S

## W23T-E27 — Transmission × Storage Value

Congestion can raise the local value of batteries/hydro if they sit on the constrained side.

Research:
constraint topology
× storage location
× state of charge/headroom.

Priority: A+

## W23T-E28 — Congestion Export/Import Reversal

Track when normal import/export patterns reverse because of a constraint.

Feature:
unexpected interchange sign/magnitude change
× binding-constraint state.

Priority: A

## W23T-E29 — Constraint Centrality

Build a graph of facilities and contingencies.

Rank constraints by:
frequency
shadow-price intensity
network reach
load exposed
substitute paths.

Priority: S-

## W23T-E30 — Transmission Substitution Quotient

TSQ =
effective constrained transfer capacity
/
available alternate network + local generation + storage + demand response.

Lower substitute capacity implies greater economic impact.

Priority: S

## W23T-E31 — Topology Reality Gap

Compare:
day-ahead expected grid state
versus
real-time topology.

Residual causes:
unexpected outage
forecast error
generation loss
weather
operator limit change.

Priority: S

## W23T-E32 — Grid Transport Stress Vector

Combine:
BINDING_CONSTRAINT_COUNT
SHADOW_PRICE_INTENSITY
TRANSFER_HEADROOM
OUTAGE_STACK
CONTINGENCY_BREADTH
REALTIME_SURPRISE.

Output:
OPEN
NORMAL
TIGHT
FRAGMENTED
CRITICAL.

Priority: S

## Highest-priority W23T tests

1. W23T-E01 PJM Real-Time Binding Constraint Pulse
2. W23T-E06 Day-Ahead-to-Real-Time Constraint Surprise
3. W23T-E08 PJM Transfer Headroom
4. W23T-E12 Outage-to-Constraint Conversion Hazard
5. W23T-E14 ERCOT SCED Constraint Pulse
6. W23T-E15 ERCOT Flow-to-Limit Ratio
7. W23T-E17 ERCOT Transmission Outage Stack
8. W23T-E26 Transmission × Gas Burn Collision
9. W23T-E30 Transmission Substitution Quotient
10. W23T-E32 Grid Transport Stress Vector
