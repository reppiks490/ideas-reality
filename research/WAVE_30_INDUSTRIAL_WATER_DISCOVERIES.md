# Wave 30W — Industrial Water Constraint & Thermal Capacity

Namespace: **W30W**

Thesis: water can become the binding constraint on production even when electricity, labor, equipment and feedstock remain available. The relevant state is not generic drought; it is whether a facility can lawfully and physically withdraw, cool, discharge, irrigate or process enough water to sustain output.

All candidates are research hypotheses only. Claude owns any later implementation.

## W30W-E01 — Real-Time Intake Sufficiency

Primary source:
USGS high-frequency streamflow/gage/water-temperature observations.

For a water-dependent facility:
intake_available_flow
relative to
historical/estimated required withdrawal and minimum-operating envelope.

Priority: S

## W30W-E02 — Cooling-Water Temperature Stress

Feature:
observed intake water temperature
relative to
plant/cooling-system historical operating envelope.

Higher intake temperature reduces cooling effectiveness and can tighten thermal-discharge headroom.

Priority: S-

## W30W-E03 — Thermal Discharge Headroom

Using point-in-time NPDES permit terms where extractable:
allowable discharge-temperature/thermal condition
-
modeled/observed discharge requirement.

Do not assume one national temperature limit.

Priority: S

## W30W-E04 — Low-Flow × High-Temperature Collision

Composite:
low streamflow
× high water temperature
× high power demand.

This is the core thermoelectric cooling-risk state.

Priority: S

## W30W-E05 — Once-Through Cooling Vulnerability

Map EIA plant cooling-system type and water source.

Once-through and recirculating systems have different withdrawal/consumption and temperature sensitivities.

Priority: A+

## W30W-E06 — Plant Water-Dependency Exposure

Estimate plant-specific:
withdrawal requirement,
consumption requirement,
water source,
cooling technology,
generation capacity.

Use EIA/USGS historical data as exposure, not as live telemetry.

Priority: S-

## W30W-E07 — Water-Constrained Generation Hazard

Target:
P(derate/outage | current hydrology/temperature/load).

Validate against:
EIA generation,
RTO outage/dispatch,
NRC events for nuclear,
company/operator notices.

Priority: S

## W30W-E08 — Thermal Plant Substitution Pressure

When water-sensitive generation is constrained:
estimate which generation must replace it.

Substitutes:
gas,
coal,
imports,
storage,
renewables,
demand response.

Priority: S

## W30W-E09 — Cooling Constraint × Gas Burn

Candidate:
water-constrained non-gas MW
× probability gas is marginal replacement.

Target:
regional gas generation and later NG basis/futures.

Priority: S-

## W30W-E10 — Nuclear Cooling-Water Collision

Fuse W14I nuclear status with water temperature/flow.

Separate:
reactor internal/safety event
from
external cooling-water constraint.

Priority: A+

## W30W-E11 — Hydropower vs Thermal Water Competition State

Low water can reduce hydro flexibility while simultaneously stressing thermoelectric cooling.

Composite:
hydro shortfall
+ thermal cooling risk
+ load.

Priority: S

## W30W-E12 — U.S. Drought Monitor Industrial Exposure

Primary source:
U.S. Drought Monitor weekly GIS/REST data.

Intersect drought severity with:
power plants,
fabs,
refineries,
chemical plants,
agricultural regions,
mines,
data centers.

Use drought only as slow contextual state; operational hydrology remains primary.

Priority: A

## W30W-E13 — Drought Acceleration / Breadth

Feature:
week-over-week D0-D4 area/population change
and facility-weighted drought exposure.

Priority: B+

## W30W-E14 — California Water-Right Curtailment State

Primary source:
California State Water Resources Control Board public curtailment orders/addenda/status pages.

States:
AVAILABLE
CONDITIONAL_DIVERSION
PARTIAL_CURTAILMENT
FULL_CURTAILMENT
SUSPENDED
REINSTATED.

Priority: S-

## W30W-E15 — Water-Right Priority Exposure

For facilities/agriculture with resolvable water rights:
map right priority/group
to current curtailment order.

No exposure claim without verified right/facility mapping.

Priority: A+

## W30W-E16 — Curtailment Revision Velocity

California orders/addenda can suspend/reinstate curtailments as flow changes.

Feature:
change in legally available diversion capacity
between public order vintages.

Priority: S-

## W30W-E17 — Flow-Threshold Crossing Hazard

Some curtailment systems explicitly reference streamflow thresholds.

Use USGS current flow + forecast context to estimate probability of:
restriction reinstatement,
conditional suspension,
or release.

Priority: A+

## W30W-E18 — Agricultural Irrigation Capacity Loss

Map curtailed water availability to:
crop acreage,
crop water demand,
growth stage,
alternative groundwater/surface supply.

Target:
physical crop stress/yield expectation before futures returns.

Priority: A+

## W30W-E19 — Industrial Water Curtailment Graph

Graph:
watershed/right
-> intake/diversion
-> facility
-> product
-> customer/supply chain.

Potential sectors:
semiconductors,
chemicals,
refining,
food processing,
mining,
power.

Priority: A

## W30W-E20 — Semiconductor Fab Water-Risk State

For verified fab locations/sources:
water availability
× production dependence
× recycle/reuse capacity
× alternative supply.

Do not infer outage directly from regional drought.

Priority: A

## W30W-E21 — Refinery/Chemical Water-Risk State

Fuse:
hydrology/curtailment
+ W15X plant-upset state
+ facility water dependence.

Question:
does water stress increase outage/restart risk or constrain throughput?

Priority: A

## W30W-E22 — Data-Center Water Cooling Exposure

Map only facilities with verified cooling/water dependence.

Feature:
water stress
× cooling technology
× alternative cooling/reclaimed-water access.

Priority: B+

## W30W-E23 — Colorado River Allocation Shock

Primary source:
Bureau of Reclamation annual/24-month operating studies and shortage declarations.

State:
allocation/shortage tier
× affected state/sector entitlement
× reservoir forecast.

Priority: A

## W30W-E24 — Water Allocation Forecast Revision

Track successive Reclamation 24-Month Study vintages.

Feature:
change in projected reservoir elevation/release/shortage condition.

Priority: A+

## W30W-E25 — Water Stress Substitution Quotient

WSSQ =
water-dependent capacity at risk
/
capacity available through alternate water source, substitute facility, imports or alternative generation.

Priority: S

## W30W-E26 — Water Constraint Recovery Half-Life

After flow/temperature improves or curtailment suspends:
measure time to actual operational recovery.

Priority: A

## W30W-E27 — Water Reality Gap

Compare:
drought narrative/category
vs
facility-specific hydrology,
legal diversion state,
actual operational consequence.

Priority: A+

## W30W-E28 — Industrial Water Truth Ladder

DROUGHT/HYDROLOGY
-> LEGAL/PHYSICAL WATER AVAILABILITY
-> FACILITY OPERATING ENVELOPE
-> DERATE/OUTPUT LOSS
-> SUBSTITUTE FLOW
-> INVENTORY/BASIS
-> MARKET.

Priority: S architecture

## Highest-priority W30W tests

1. W30W-E01 Real-Time Intake Sufficiency
2. W30W-E03 Thermal Discharge Headroom
3. W30W-E04 Low-Flow × High-Temperature Collision
4. W30W-E07 Water-Constrained Generation Hazard
5. W30W-E08 Thermal Plant Substitution Pressure
6. W30W-E11 Hydropower vs Thermal Water Competition
7. W30W-E14 California Water-Right Curtailment State
8. W30W-E17 Flow-Threshold Crossing Hazard
9. W30W-E25 Water Stress Substitution Quotient
10. W30W-E28 Industrial Water Truth Ladder
