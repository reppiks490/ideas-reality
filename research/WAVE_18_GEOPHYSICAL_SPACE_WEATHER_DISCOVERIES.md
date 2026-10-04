# Wave 18G — Geophysical & Space-Weather Exposure

Namespace: **W18G**

Thesis: physical hazards are most useful when translated from headline magnitude into machine-readable exposure at the actual infrastructure location, then into the probability of operational impairment and substitute-capacity stress. This wave covers earthquake shaking, aftershock risk, tsunami state, volcanic ash and geomagnetic/space-weather stress.

All candidates are research hypotheses only. Claude owns any later implementation.

## W18G-E01 — USGS Real-Time Earthquake Shock

Primary source:
USGS Earthquake Hazards Program real-time GeoJSON/ATOM feeds.

Build initial event state from:
origin time,
first-public time,
magnitude,
depth,
location,
review status,
tsunami flag,
available product types.

This is a discovery layer, not the final exposure metric.

Priority: A+

## W18G-E02 — ShakeMap Facility Intensity

Primary source:
USGS ShakeMap.

For each critical facility/route:
sample point-in-time ShakeMap
MMI,
PGA,
PGV,
spectral acceleration,
and uncertainty.

Targets:
refineries,
LNG terminals,
pipelines,
ports,
data centers,
power plants,
rail chokepoints,
semiconductor fabs,
mines,
warehouses.

Priority: S

## W18G-E03 — Magnitude-vs-Local-Shaking Reality Gap

Feature:
local ShakeMap intensity
-
intensity expected from headline magnitude/epicentral-distance heuristic.

Goal:
detect events that are operationally worse or milder at specific assets than broad news framing suggests.

Priority: S-

## W18G-E04 — Multi-Facility Shaking Breadth

Measure:
critical capacity exposed above selected MMI/PGA thresholds
weighted by facility importance.

Example:
one refinery at high shaking
versus
many Gulf/West Coast assets under moderate shaking.

Priority: A+

## W18G-E05 — PAGER Impact Revision

Primary source:
USGS PAGER.

PAGER provides rapid shaking/exposure and estimated fatality/economic-loss ranges, generally within tens of minutes, and versions update as shaking/source information improves.

Feature:
change in alert level / loss distribution
between public PAGER versions.

Priority: A+

## W18G-E06 — ShakeMap Revision Surprise

All ShakeMap versions/timestamps are archived in ComCat.

Research:
first map
-> revised source
-> added stations/DYFI
-> final-ish stabilized map.

Feature:
newly exposed critical capacity between versions.

Priority: S

## W18G-E07 — Operational Aftershock Hazard

Primary source:
USGS Operational Aftershock Forecasts.

USGS forecasts probability/expected counts for magnitude thresholds over one day, one week, one month and one year.

Candidate:
P(M5+/M6+ aftershock)
× already-damaged capacity
× repair/restart stage.

Priority: S

## W18G-E08 — Aftershock Re-Disruption State

State:
INITIAL_DAMAGE
EARLY_RECOVERY
HIGH_AFTERSHOCK_HAZARD
REPEATED_SHAKING
STABILIZING.

Question:
Does elevated aftershock probability materially lengthen outage/recovery expectations for exposed infrastructure?

Priority: A+

## W18G-E09 — Earthquake Supply Substitution Pressure

Graph:
shaking-exposed asset
-> lost capacity
-> substitute asset/route
-> spare capacity.

Use existing Critical Infrastructure Substitution Quotient framework:
unexpected capacity loss / available substitute capacity.

Priority: S

## W18G-E10 — Earthquake Headline-to-Physical Confirmation Gap

Fuse:
USGS event
+ ShakeMap
+ grid status
+ port/rail/FAA
+ facility thermal/flare/telecom status.

Purpose:
separate alarming earthquakes with little industrial consequence from moderate events that strike critical infrastructure directly.

Priority: S

## W18G-E11 — Tsunami Alert State Machine

Primary source:
U.S. Tsunami Warning Centers CAP/ATOM feeds.

States:
INFORMATION
WATCH
ADVISORY
WARNING
OBSERVED_WAVE
DOWNGRADE
CANCELLED.

Preserve every message/version and geographic alert zone.

Priority: S-

## W18G-E12 — Tsunami Forecast-to-Observed Revision

Tsunami messages can progress from preliminary earthquake-driven forecasts to observed coastal/deep-ocean gauge measurements.

Feature:
observed wave height
-
previously forecast height/range.

Priority: S-

## W18G-E13 — Tsunami Port / Coastal Facility Exposure

Map alert/forecast zone and ETA to:
ports,
refineries,
LNG,
coastal power plants,
rail yards,
airports,
warehouses,
subsea cable landings.

Include elevation/flood-zone data where available.

Priority: A+

## W18G-E14 — Tsunami Lead-Time-to-Mitigation

Feature:
forecast arrival time
-
first actionable alert time.

Then map available lead to:
port evacuation,
ship repositioning,
terminal shutdown,
rail/road closure,
plant safe-state actions.

Priority: A

## W18G-E15 — Tsunami Operational Reality Gap

Forecast warning severity
vs
observed wave
vs
actual port/facility closure.

Research both:
false-positive operational caution
and underestimated realized disruption.

Priority: A+

## W18G-E16 — Volcanic Ash Advisory Pulse

Primary sources:
NOAA/NWS Volcanic Ash Advisory Centers and aviation weather products.

Build:
volcano
eruption/advisory time
ash altitude/flight levels
observed/forecast plume
movement
next-advisory state.

Priority: A+

## W18G-E17 — Ash Plume × Cargo/Aviation Route Exposure

Intersect ash polygon/flight levels with:
major air-cargo hubs,
international routes,
ETOPS/polar corridors,
airport approach/departure corridors.

Goal:
estimate capacity/rerouting burden, not merely count advisories.

Priority: S-

## W18G-E18 — Ash Forecast-to-Observed State

State:
ERUPTION_SIGNAL
ASH_NOT_IDENTIFIED
OBSERVED_ASH
FORECAST_PLUME
SIGMET/ROUTE_RESTRICTION
NO_FURTHER_ADVISORY.

Research forecast error and duration.

Priority: A

## W18G-E19 — SWPC Geomagnetic Storm State

Primary source:
NOAA Space Weather Prediction Center.

Separate:
WATCH = forecast possibility
WARNING = threshold expected
ALERT = threshold reached
plus observed Kp/G-scale state.

Priority: S

## W18G-E20 — Upstream Solar-Wind Shock

Use SWPC real-time solar-wind plasma and interplanetary magnetic-field measurements.

Features:
speed jump,
density shock,
total field,
southward Bz magnitude/duration,
dynamic-pressure proxy,
arrival/regime transition.

These are upstream physical drivers, not market indicators.

Priority: S

## W18G-E21 — Solar-Wind-to-G-Scale Lead

Research:
L1 solar-wind/IMF shock
-> geospace response
-> estimated/observed Kp
-> G-scale alert.

Question:
How much reliable operational lead exists before grid/GNSS/satellite mitigation becomes relevant?

Priority: S

## W18G-E22 — Geomagnetic Grid Vulnerability

Fuse:
G-scale / geoelectric field proxy
× geomagnetic latitude
× geology/conductivity
× long transmission lines
× transformer/grid topology
× current reserve state.

Output:
LOW
WATCH
GIC_STRESS
MITIGATION_ACTIVE
GRID_OPERATIONAL_RISK.

Priority: S

## W18G-E23 — Grid Mitigation Activation State

Engineering evidence from major storms shows grid operators can suspend maintenance, alter system configuration or call additional generation.

Research public RTO/utility actions during strong geomagnetic events.

The mitigation action itself may change reserve/fuel needs even without an outage.

Priority: A+

## W18G-E24 — GNSS / HF Communications Stress

Space weather can degrade:
GNSS positioning,
HF communications,
aviation polar communications,
satellite links.

Fuse SWPC state with:
FAA rerouting,
maritime navigation,
precision agriculture,
telecom/satellite status.

Priority: A+

## W18G-E25 — LEO Satellite Drag / Operations Stress

Geomagnetic heating increases upper-atmosphere density and can increase drag on low-Earth-orbit satellites.

Research:
storm severity
× constellation altitude
× orbit-maintenance response
× service degradation.

Priority: A

## W18G-E26 — Space Weather × Infrastructure Collision

Examples:
geomagnetic storm + already-tight grid
GNSS degradation + severe aviation weather
satellite degradation + terrestrial telecom outage.

Composite only after individual mechanisms validate.

Priority: S-

## W18G-E27 — Geophysical Multi-Hazard Chain

Earthquake
-> tsunami
-> port/power/telecom disruption
-> logistics rerouting
-> supply substitution.

Preserve causal order and event timestamps.

Priority: A+

## W18G-E28 — Physics-Before-News Exposure Engine

General framework:

PHYSICAL_SENSOR
-> HAZARD_FIELD
-> ASSET EXPOSURE
-> OPERATING STATE
-> SUBSTITUTE CAPACITY
-> ECONOMIC CONSEQUENCE.

This wave promotes physics-based exposure ahead of narrative sentiment whenever the source clock permits.

Priority: S architecture

## Highest-priority W18G tests

1. W18G-E02 ShakeMap Facility Intensity
2. W18G-E05 PAGER Impact Revision
3. W18G-E06 ShakeMap Revision Surprise
4. W18G-E07 Operational Aftershock Hazard
5. W18G-E11 Tsunami Alert State Machine
6. W18G-E13 Tsunami Port / Coastal Facility Exposure
7. W18G-E17 Ash Plume × Cargo/Aviation Exposure
8. W18G-E20 Upstream Solar-Wind Shock
9. W18G-E21 Solar-Wind-to-G-Scale Lead
10. W18G-E22 Geomagnetic Grid Vulnerability
