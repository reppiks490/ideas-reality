# Wave 35C — Subsea Connectivity & Repair Capacity

Namespace: **W35C**

Thesis: international digital capacity can remain apparently functional after a submarine-cable fault because traffic reroutes onto alternate paths. The economically relevant state is therefore not simply UP/DOWN; it is the amount of physical path diversity and spare capacity remaining, the latency/cost penalty of rerouting, and the time required to restore the failed physical link.

Public-source limitation: FCC NORS submarine-cable outage filings are presumptively confidential. They are not a public live signal and must not be reconstructed or treated as observable.

All candidates are research hypotheses only. Claude owns later implementation.

## W35C-E01 — Public Cable Fault Pulse
Create incident only from a public operator/carrier/regulator fault notice or independently validated network anomaly with later confirmation.
Priority: S

## W35C-E02 — Fault Localization State
UNKNOWN
LAND_SEGMENT
LANDING_STATION
SHALLOW_WATER
DEEP_WATER
POWER/REPEATER
MULTIPLE_SEGMENTS.
Priority: A+

## W35C-E03 — Cable Corridor Capacity Loss
Estimate unavailable design/activated capacity with lower/base/upper ranges.
Do not assume nominal design capacity equals carried traffic.
Priority: S

## W35C-E04 — Physical Redundancy Loss
Feature:
normal independent paths - currently available independent paths.
Priority: S

## W35C-E05 — Restored-but-Degraded State
Traffic may be restored over alternate paths while original cable remains physically failed.
State:
HARD_DOWN
PARTIAL_REROUTE
LOGICALLY_RESTORED
PHYSICALLY_UNREPAIRED
FULL_REDUNDANCY_RESTORED.
Priority: S

## W35C-E06 — Reroute Latency Penalty
Measure path/RTT change after fault using independent network telemetry.
Priority: S-

## W35C-E07 — Reroute Congestion Penalty
Measure packet loss, throughput degradation and time-of-day latency under rerouted load.
Priority: A+

## W35C-E08 — Cloud Inter-Region Path Shock
Fuse W34D cloud-region dependencies with subsea corridor impairment.
Priority: S-

## W35C-E09 — Financial-Network Corridor Exposure
Map only verified network/colo/cloud dependencies of exchanges, payment processors, banks or trading venues to affected corridors.
Priority: A

## W35C-E10 — Landing-Point Concentration
Count independent cables sharing one landing region/station/shore approach.
Priority: S-

## W35C-E11 — Common-Route Hazard
Two cables can be logically independent but physically co-located near landing zones or along marine corridors.
Estimate shared-hazard exposure.
Priority: S

## W35C-E12 — Multi-Cable Common-Cause Event
Detect near-simultaneous faults sharing geography/cause:
anchor,
fishing,
landslide,
earthquake,
power,
sabotage/unknown.
Priority: S

## W35C-E13 — Repair Vessel Assignment
State:
NO_VESSEL
VESSEL_RESERVED
MOBILIZING
TRANSIT
ON_STATION
RECOVERING_CABLE
SPLICING/TESTING
COMPLETE.
Priority: S

## W35C-E14 — Vessel Transit Clock
Expected time from public assignment/departure to repair area.
Priority: A+

## W35C-E15 — Permit / Clearance Delay
Public operator updates often identify permits/clearances as a gating dependency.
Feature:
expected repair delay attributable to regulatory access.
Priority: S-

## W35C-E16 — Weather / Sea-State Repair Hazard
Fuse marine forecast/operability with repair-vessel location and repair window.
Priority: A+

## W35C-E17 — Preceding-Repair Dependency
One repair may be intentionally sequenced ahead of another to restore redundancy before taking temporary routes offline.
Represent repair DAG dependencies.
Priority: S

## W35C-E18 — Estimated Time to Repair Revision
Archive every ETR vintage.
Feature:
current ETR - prior ETR.
Priority: S

## W35C-E19 — Repair Completion Surprise
Actual restoration time minus latest point-in-time ETR.
Priority: A

## W35C-E20 — Physical Redundancy Recovery
Do not mark recovered when customer traffic resumes.
Recovery target is restored physical path/diversity where confirmable.
Priority: S

## W35C-E21 — BGP Path-Length Shift
Use RIPE RIS/RouteViews to detect AS-path changes after fault.
Priority: A+

## W35C-E22 — Traffic-Path Geography Shift
Where lawful/public measurement supports it, infer traffic rerouting geography from RTT/path changes.
Priority: A

## W35C-E23 — Cable Fault Reality Gap
Compare:
operator narrative
vs
routing/traffic measurements
vs
customer service state.
Priority: S

## W35C-E24 — Spare-Capacity Exhaustion Hazard
Estimate:
rerouted demand
/
remaining alternate-corridor capacity.

Priority: S

## W35C-E25 — Second-Fault Fragility
Probability-weighted impact of a second cable/corridor loss while primary redundancy is already degraded.
Priority: S

## W35C-E26 — Repair-Fleet Scarcity
Track simultaneous public cable faults and known repair-vessel commitments where available.
Question:
is marine repair capacity itself becoming the bottleneck?
Priority: A+

## W35C-E27 — Cable Landing License / Ownership Graph
Primary structural source:
FCC U.S. submarine cable landing licenses and landing points.
Map:
cable
-> landing point
-> licensee/owner/operator
-> connected regions.
Priority: S infrastructure

## W35C-E28 — U.S.-International Capacity Structure
Use FCC public compiled Section 43.82 capacity/landing-point tables where available.
Preserve confidentiality gaps for individually withheld filings.
Priority: A

## W35C-E29 — Cable Corridor Resilience Quotient
CCRQ =
remaining independent usable corridor capacity
/
normal required traffic capacity.

Priority: S

## W35C-E30 — Physical Connectivity Truth Ladder
PUBLIC FAULT / NETWORK ANOMALY
-> FAULT CONFIRMATION
-> CAPACITY/REROUTE EFFECT
-> REPAIR DEPENDENCIES
-> PHYSICAL REPAIR
-> REDUNDANCY RESTORATION
-> CUSTOMER/ECONOMIC NORMALIZATION.

Priority: S architecture

## Highest-priority W35C tests
1. W35C-E04 Physical Redundancy Loss
2. W35C-E05 Restored-but-Degraded State
3. W35C-E06 Reroute Latency Penalty
4. W35C-E11 Common-Route Hazard
5. W35C-E13 Repair Vessel Assignment
6. W35C-E17 Preceding-Repair Dependency
7. W35C-E18 ETR Revision
8. W35C-E24 Spare-Capacity Exhaustion Hazard
9. W35C-E25 Second-Fault Fragility
10. W35C-E29 Cable Corridor Resilience Quotient
