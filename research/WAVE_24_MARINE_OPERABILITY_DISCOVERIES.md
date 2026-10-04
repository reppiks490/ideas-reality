# Wave 24M — Marine Operability & Navigable Capacity

Namespace: **W24M**

Thesis: a port or waterway can be technically open while effective cargo capacity is sharply reduced by draft, tide, current, wave, wind, visibility, bridge air-gap, pilotage, or formal Captain-of-the-Port restrictions. The relevant edge is therefore not OPEN/CLOSED; it is the amount of vessel/cargo capacity that can safely and legally move through the waterway at each moment.

All candidates are research hypotheses only. Claude owns implementation.

## W24M-E01 — NOAA PORTS Real-Time Navigability State

Primary source:
NOAA Physical Oceanographic Real-Time System (PORTS) / CO-OPS Data API.

NOAA exposes frequently updated:
water level,
currents,
wind,
visibility,
air pressure,
salinity,
air gap at instrumented bridges,
and related observations.

Build port-specific state from the subset actually instrumented at each harbor.

Priority: S

## W24M-E02 — Under-Keel Clearance Capacity Envelope

For a vessel class/draft:
effective_under_keel_clearance =
observed_water_level
+ maintained_channel_depth
- vessel_draft
- squat/safety allowance.

Do not hard-code one safety allowance; use waterway/pilotage rules where public.

Output:
UNRESTRICTED
TIDAL_WINDOW
DRAFT_REDUCED
NO_SAFE_TRANSIT.

Priority: S

## W24M-E03 — Tidal-Window Compression

Some deep-draft vessels can transit only during specific water-level/current windows.

Feature:
safe_transit_minutes_next_24h
relative to
normal safe window.

Mechanism:
shrinking windows can create anchorage queues even with an officially open port.

Priority: S

## W24M-E04 — Current-Limited Transit Window

NOAA PORTS provides real-time currents and current predictions.

For vessel classes/routes with current restrictions:
safe_current_window
= periods where speed/direction remain within route-specific limits.

Priority: A+

## W24M-E05 — Air-Gap Bridge Clearance State

NOAA CO-OPS supports real-time air-gap observations at instrumented bridges.

Candidate:
observed_air_gap
-
required vessel air draft
-
safety margin.

Use:
container/cruise/specialty vessel transit constraints at relevant bridges.

Priority: A+

## W24M-E06 — Visibility-Limited Pilotage State

PORTS can expose visibility at instrumented stations.

Research:
visibility residual
× port/pilot restriction rules
× vessel class
× traffic queue.

Do not assume fog automatically stops traffic; use actual local operating restrictions.

Priority: A

## W24M-E07 — NDBC Offshore Sea-State Constraint

Primary source:
NOAA National Data Buoy Center.

NDBC real-time files provide current observations including standard meteorological data and spectral wave summaries; most stations report hourly, with many records available within roughly 25 minutes after the hour.

Build:
significant wave height
dominant/average period
wave direction
wind speed/gust/direction
pressure trend.

Priority: A+

## W24M-E08 — Wave-Period Severity, Not Height Alone

Equal significant wave height can have different vessel/berth consequences depending on period/direction.

Candidate:
operability severity
= f(Hs, period, direction, vessel/berth orientation).

Priority: A

## W24M-E09 — Entrance-Bar / Pilot Transfer Risk State

Fuse:
offshore NDBC sea state
+ PORTS currents/water level
+ pilot transfer/port restrictions where public.

Target:
probability of delayed pilot boarding or restricted deep-draft entry.

Priority: A+

## W24M-E10 — NOAA OFS Forward Navigability Forecast

Primary source:
NOAA Operational Forecast Systems.

OFS systems produce nowcasts and 48–120 hour forecasts depending on region, often multiple cycles per day, for water levels, currents, salinity, temperature and related fields.

Research:
future safe-transit capacity before restrictions/queues become observable.

Priority: S

## W24M-E11 — Forecast-to-Observed Marine Surprise

Compare latest point-in-time OFS forecast against later PORTS/NDBC observations.

Feature:
observed navigability
-
forecast navigability.

Use to measure unanticipated deterioration/improvement.

Priority: S-

## W24M-E12 — Coast Guard Port Condition State Machine

Primary source:
U.S. Coast Guard Captain of the Port / Homeport / MSIB notices.

Normalize hurricane conditions:
NORMAL/OPEN
WHISKEY
X-RAY
YANKEE
ZULU
RESTRICTED_REOPEN
FULL_REOPEN.

Official examples show:
YANKEE can restrict inbound commercial vessel traffic,
while ZULU can close ports to vessel traffic and suspend cargo operations except specific authorization.

Priority: S

## W24M-E13 — Restriction Lead-Time

Feature:
formal restriction effective time
-
first public Coast Guard notice.

Question:
How much actionable lead exists before vessel/cargo operations become restricted?

Priority: S-

## W24M-E14 — Restriction Revision Velocity

Track:
expected restriction
-> effective restriction
-> geographic expansion/contraction
-> daylight-only/restricted reopening
-> full reopening.

The recovery path is information, not administrative noise.

Priority: A+

## W24M-E15 — Weather-to-Formal-Restriction Gap

Fuse:
NHC/weather forecasts
+ NDBC sea state
+ PORTS water/current
+ Coast Guard port-condition notice.

Question:
Does observed physical deterioration imply a higher probability of formal closure before the official state changes?

Priority: S

## W24M-E16 — Port Reopening Readiness

After severe weather:
wind/wave improvement alone does not guarantee port reopening.

Model:
hydrographic/navigation assessment,
channel condition,
aids-to-navigation status,
debris,
power/terminal condition,
formal COTP state.

Priority: A+

## W24M-E17 — Effective Port Cargo Capacity

General candidate:

effective_port_capacity =
nominal_capacity
× vessel_class_eligibility
× safe_transit_window_fraction
× berth_availability
× formal_restriction_factor.

Priority: S

## W24M-E18 — Deep-Draft Capacity Loss

When water level/draft rules tighten, shallow vessels may remain unaffected while largest cargo vessels lose capacity.

Translate:
maximum permissible draft reduction
-> cargo-tonnage loss per call
-> extra vessel calls / delay requirement.

Priority: S

## W24M-E19 — Great Lakes–Seaway Maximum-Draft State

Primary source:
Great Lakes St. Lawrence Seaway notices.

Seaway notices publish exact maximum permissible draft and effective dates; 2026 notices show draft changes based on ice/water conditions.

Build:
permissible draft
× route section
× DIS eligibility
× vessel class.

Priority: S-

## W24M-E20 — Draft Information System Optionality

Seaway rules permit qualifying vessels with approved operational DIS to transit above the standard permissible draft by a specified increment under defined conditions.

Research:
capacity advantage of DIS-equipped vessels during shallow-water restrictions.

Priority: A

## W24M-E21 — Seaway Transit/Lock Queue State

Public Seaway operational pages expose vessel transit/order information and bridge/lock operational context.

Candidate:
vessel arrivals
vs
lock/transit completions
vs
expected passage time.

Priority: A

## W24M-E22 — Marine Queue Formation Hazard

Estimate:
P(queue growth over next N hours)
from:
safe-window shrinkage,
new arrivals,
berth/lock throughput,
formal restrictions.

Priority: S

## W24M-E23 — Marine Queue Recovery Half-Life

After restriction lifts:
measure anchorage/queue backlog liquidation separately from formal reopening.

A reopened port can remain operationally congested.

Priority: S-

## W24M-E24 — LNG / Energy Vessel Operability

Map marine envelope specifically to:
LNG carriers,
crude tankers,
product tankers,
LPG vessels.

Fuse with:
terminal exposure,
storage,
pipeline flows,
regional basis.

Priority: S

## W24M-E25 — Bulk Commodity Draft Sensitivity

Deep-draft bulk carriers lose cargo capacity nonlinearly when permissible draft falls.

Research:
draft reduction
-> tonnes lost per vessel
-> effective export/import capacity
for grain, ore, coal and other bulk flows.

Priority: S

## W24M-E26 — Marine Substitution Quotient

MSQ =
lost waterborne cargo capacity
/
available substitute capacity.

Substitutes:
other port,
rail,
truck,
pipeline,
alternate vessel size,
alternate route.

Priority: S

## W24M-E27 — Navigability Shock Before Queue

The highest-value event may occur when physical conditions cross an operability threshold before public vessel queues materially build.

Target:
threshold_crossing_time
-> queue_growth_time.

Priority: S research architecture

## W24M-E28 — Multi-Port Diversion Pressure

When one port loses deep-draft capacity:
estimate likely diversion to neighboring ports based on:
commodity compatibility,
channel depth,
berths,
rail/pipeline connections,
distance.

Priority: A+

## W24M-E29 — Marine Forecast Revision Alpha Candidate

Archive every OFS cycle.

Feature:
change in predicted safe-window/capacity
between consecutive forecast cycles.

Revision may be more informative than level.

Priority: S-

## W24M-E30 — Physical Operability Truth Layer

Use marine observations as a high-truth layer to validate:
shipping news,
AIS congestion,
terminal statements,
weather narratives.

If narrative and physical-operability state disagree, preserve the disagreement as a feature.

Priority: S

## Highest-priority W24M tests

1. W24M-E02 Under-Keel Clearance Capacity Envelope
2. W24M-E03 Tidal-Window Compression
3. W24M-E10 NOAA OFS Forward Navigability Forecast
4. W24M-E12 Coast Guard Port Condition State Machine
5. W24M-E17 Effective Port Cargo Capacity
6. W24M-E18 Deep-Draft Capacity Loss
7. W24M-E22 Marine Queue Formation Hazard
8. W24M-E24 LNG / Energy Vessel Operability
9. W24M-E25 Bulk Commodity Draft Sensitivity
10. W24M-E26 Marine Substitution Quotient
