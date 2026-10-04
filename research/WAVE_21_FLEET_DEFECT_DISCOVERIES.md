# Wave 21D — Fleet Defect & Mandatory Remediation

Namespace: **W21D**

Thesis: a discovered defect becomes economically meaningful when it changes the legally/operationally available fleet, inspection burden, repair-part demand, or utilization. Mandatory remediation creates explicit compliance clocks that can be mapped to exposed equipment and operator capacity.

All candidates are research hypotheses only. Claude owns implementation.

## W21D-E01 — FAA Emergency Airworthiness Directive Pulse

Primary source:
FAA Emergency Airworthiness Directives / Dynamic Regulatory System.

FAA states an Emergency AD is issued when an unsafe condition requires immediate action.

Build:
issue/public time,
affected make/model/product,
unsafe condition,
required action,
compliance clock.

Priority: S

## W21D-E02 — Emergency AD Immediate-Capacity Risk

Classify requirements:
BEFORE_FURTHER_FLIGHT
WITHIN_N_FLIGHT_HOURS/CYCLES
WITHIN_N_DAYS
INSPECT_THEN_CONDITIONAL_REPAIR
OPERATING_LIMITATION.

Estimate fraction of exposed fleet temporarily unavailable until compliance.

Priority: S

## W21D-E03 — Emergency AD Actual-Notice/Public-Notice Split

FAA states Emergency ADs can first become effective to recipients via actual notice before follow-up Federal Register publication.

For public research store:
EAD issue time,
public DRS/FAA availability time,
Federal Register follow-up.

Never use private recipient receipt time unless lawfully available to the strategy.

Priority: S methodology/edge hybrid

## W21D-E04 — Ordinary AD Compliance Compression

For non-emergency ADs:
extract effective date and mandatory action deadline.

Candidate:
required maintenance burden
/
available maintenance window.

Priority: A+

## W21D-E05 — Aircraft Model Fleet Exposure

Primary source:
FAA Releasable Aircraft Database, refreshed daily.

Estimate affected U.S.-registered population by:
make/model/series,
serial applicability where possible,
registration state/owner class.

Priority: A+

## W21D-E06 — Operator Capacity Exposure

Registry owner is not always operator.

Map affected tails to actual carrier/operator using verified operational sources.

Feature:
affected available seat/cargo tonnage
/
operator fleet capacity.

Priority: S

## W21D-E07 — Spare-Aircraft Substitution Buffer

An AD impact depends on:
spare ratio,
fleet commonality,
lease/substitution options,
route gauge flexibility,
maintenance capacity.

Candidate:
required aircraft removals / spare equivalent capacity.

Priority: S

## W21D-E08 — Maintenance-Slot Congestion

A fleetwide short compliance deadline can create scarce:
MRO bays,
technicians,
inspection equipment,
replacement parts.

Research queue formation and completion rate.

Priority: S-

## W21D-E09 — Supplier-Part Common-Mode Exposure

Map affected component/part number to:
aircraft models,
engine variants,
operators,
supplier,
production batches.

Goal:
identify multi-fleet common-mode defect risk.

Priority: A+

## W21D-E10 — FAA Service Difficulty Defect Cluster

Primary source:
FAA Service Difficulty Reporting System.

Reports contain:
aircraft/engine/part,
difficulty date,
JASC/ATA code,
stage of operation,
problem description,
corrective action and related fields.

Build abnormal defect counts by part/model.

Priority: A+

## W21D-E11 — SDR-to-AD Escalation Hazard

Target:
probability that an emerging defect cluster is followed by:
manufacturer action,
FAA investigation,
AD,
Emergency AD.

Important:
public SDR availability begins only after FAA processing/approval.

Priority: S-

## W21D-E12 — Defect Severity Mix

Weight SDR clusters by operational consequence:
engine shutdown,
unscheduled landing,
fire/smoke,
structural crack,
flight-control issue,
repeat defect.

Priority: A+

## W21D-E13 — Cycles/Hours Failure Surface

Use aircraft/component total cycles/hours and time-since-overhaul fields where available.

Research whether defect probability concentrates in a measurable operating-age band.

Priority: A

## W21D-E14 — AD Remedy Completion Hazard

Estimate time from:
effective date
to inspection
to repair
to return to service.

Inputs:
action complexity,
parts,
labor,
fleet size,
MRO geography.

Priority: A+

## W21D-E15 — FAA Defect-to-Cargo Network Shock

For cargo aircraft/engines:
affected fleet fraction
× critical overnight network role
× spare capacity
× FAA NAS constraints.

Priority: S-

## W21D-E16 — NHTSA Recall Population Shock

Primary source:
NHTSA recall data/API.

Manufacturers that determine a safety defect/noncompliance must notify NHTSA within five business days.

Fields include:
campaign,
make/model/year,
potential units affected,
defect/consequence,
remedy,
report date,
owner notification.

Priority: A+

## W21D-E17 — Stop-Drive / Park-Outside Severity

Separate urgent consumer advisories:
DO_NOT_DRIVE
PARK_OUTSIDE
NORMAL_RECALL.

These can create immediate usable-fleet loss or behavioral demand for alternative transport.

Priority: A

## W21D-E18 — Vehicle Recall Repair-Capacity Gap

Candidate:
affected units
× remedy labor/part requirement
/
dealer/service/part capacity.

Question:
Does a huge recall with a constrained remedy create measurable parts/service backlog?

Priority: A+

## W21D-E19 — Recall Remedy-Lag State

Track:
manufacturer determination
NHTSA report
dealer notice
interim owner notice
final remedy notice
parts availability
completion.

Priority: A+

## W21D-E20 — Automotive Supplier Common-Mode Defect

Map component defect to:
supplier,
OEMs/models,
production plants,
manufacturing date ranges.

Research cross-OEM exposure where public filings support identity.

Priority: S-

## W21D-E21 — Production Containment Spillover

A defect found in field units can also trigger:
plant containment,
supplier sorting,
line inspection,
rework,
shipment hold.

Only include when public evidence exists.

Priority: A

## W21D-E22 — Mandatory Remediation × Inventory State

A recall/AD is more economically disruptive when:
finished inventory is low,
spares are low,
replacement parts constrained,
demand high.

Priority: A+

## W21D-E23 — Safety Action Revision / Expansion

Track:
initial affected population
-> expansion
-> added models/serials
-> amended remedy
-> termination/supersedure.

Revision velocity may reveal uncertainty about defect scope.

Priority: S-

## W21D-E24 — Fleet Capacity Loss Realization

For every safety action distinguish:
potentially affected equipment
from
actually removed/unavailable equipment.

Validate using:
flight activity,
cancellations,
registrations,
maintenance/return-to-service evidence.

Priority: S

## W21D-E25 — Mandatory Defect Response Graph

DISCOVERY
-> regulator/manufacturer action
-> fleet/equipment exposure
-> inspection
-> failed units
-> repair queue
-> return to service.

Research every transition explicitly.

Priority: S architecture

## W21D-E26 — Defect Shock Substitution Quotient

DSSQ =
estimated unavailable capacity
/
available substitute fleet/equipment capacity.

Targets:
airline/cargo throughput,
rental/vehicle demand,
supplier production risk.

Priority: S

## Highest-priority W21D tests

1. W21D-E02 Emergency AD Immediate-Capacity Risk
2. W21D-E05 Aircraft Model Fleet Exposure
3. W21D-E06 Operator Capacity Exposure
4. W21D-E08 Maintenance-Slot Congestion
5. W21D-E11 SDR-to-AD Escalation Hazard
6. W21D-E15 FAA Defect-to-Cargo Network Shock
7. W21D-E16 NHTSA Recall Population Shock
8. W21D-E18 Vehicle Recall Repair-Capacity Gap
9. W21D-E23 Safety Action Revision / Expansion
10. W21D-E26 Defect Shock Substitution Quotient
