# Wave 52P — Pipeline Integrity Enforcement & Forced Capacity

Namespace: **W52P**

Thesis: pipeline capacity can be legally and physically reduced after a failure or integrity finding even when the asset remains nominally "in service." PHMSA Corrective Action Orders, Safety Orders, pressure restrictions, restart approvals, integrity assessments and remedial work plans create explicit operating envelopes that can reduce crude, refined-product or natural-gas throughput before ordinary monthly statistics reveal the change.

This wave complements W22 gas transport by modeling **regulator-forced capacity state** after safety/integrity events.

All candidates are research hypotheses only. Claude owns any later implementation.

## W52P-E01 — Corrective Action Order State

Primary source:
PHMSA Pipeline Enforcement Data.

State:
NO_CASE
PROPOSED_CAO
CAO_ACTIVE
AMENDED_CAO
CLOSURE_PENDING
CLOSED.

Priority: S

## W52P-E02 — Expedited CAO Shock

A CAO may be issued expeditiously when PHMSA determines continued operation is hazardous and serious harm is likely.

Feature:
first public/order-service time
-> legally effective corrective state.

Priority: S

## W52P-E03 — Segment Shutdown State

Parse whether order requires:
full affected-segment shutdown,
isolated-subsegment shutdown,
restricted operation only,
or no direct capacity restriction.

Priority: S

## W52P-E04 — Forced Pressure Reduction

Extract:
pre-failure actual pressure,
mandated pressure cap,
percentage reduction,
affected mileage.

Priority: S

## W52P-E05 — Pressure-to-Capacity Translation

Estimate throughput impact from pressure restriction using pipeline-specific hydraulic characteristics where public/modelable.

Never equate a 20% pressure reduction to a 20% flow reduction automatically.

Priority: S

## W52P-E06 — Restart Approval Clock

Track:
shutdown time
restart-plan filing
regulator approval
actual restart
full-pressure approval.

Priority: S

## W52P-E07 — Incremental Restart Ramp

Orders may require staged pressure increases with surveillance/hold periods.

Model available capacity as a ramp rather than binary OFF/ON.

Priority: A+

## W52P-E08 — Daylight / Surveillance Restart Constraint

Some restart plans require daylight operation, patrols and emergency-response coordination.

Estimate operational delay relative to immediate technical readiness.

Priority: A

## W52P-E09 — Pressure Restriction Persistence

Feature:
days under restricted pressure after restart.

Priority: S-

## W52P-E10 — Restriction Removal Probability

Estimate:
P(PHMSA approves pressure restoration by horizon)
from:
root-cause progress,
repairs,
ILI results,
hydrotest,
regulator amendments,
prior CAO outcomes.

Priority: S

## W52P-E11 — Additional Pressure Reduction Hazard

Some orders require further pressure reductions if monthly review identifies continuing integrity risk.

Target:
P(restriction tightens | active CAO).

Priority: A+

## W52P-E12 — CAO Amendment Shock

Compare amended order to prior order:
segment scope,
pressure limit,
testing,
deadlines,
restart conditions,
required repairs.

Priority: S

## W52P-E13 — Corrective Action Milestone Clock

Extract deadlines for:
testing protocol,
metallurgical analysis,
root-cause analysis,
ILI review,
remedial work plan,
restart plan,
documentation report.

Priority: A+

## W52P-E14 — Root-Cause Completion State

State:
UNKNOWN
TESTING
PRELIMINARY_CAUSE
FINAL_RCFA
REGULATOR_ACCEPTED.

Priority: A

## W52P-E15 — Repeated-Failure Escalation

Feature:
number/severity of recent failures on same system or segment.

Question:
does repeated failure increase probability of shutdown, broader order scope or slower restoration?

Priority: S

## W52P-E16 — Integrity-Tool Miss State

If failure location was not identified by prior ILI:
classify possible detection/interpretation failure.

Research:
risk of broader re-review and additional digs.

Priority: A+

## W52P-E17 — ILI Reanalysis Burden

Orders may require raw-data re-review of prior inspections and identification of similar features elsewhere.

Estimate:
number of potential anomalies
× excavation/repair burden.

Priority: S-

## W52P-E18 — Hydrotest Requirement State

Track whether restart/remediation requires hydrostatic testing and whether test coverage spans full affected segment.

Priority: A+

## W52P-E19 — Remedial Work Plan Scope

Parse required:
inspection,
excavation,
repair,
replacement,
corrosion mitigation,
monitoring,
management-of-change.

Priority: S-

## W52P-E20 — Immediate-Repair Integrity Signal

PHMSA hazardous-liquid IM reporting defines some urgent repairs as important enough to require temporary pressure reduction or shutdown until completed.

Use as a structural severity class.

Priority: A+

## W52P-E21 — Safety Order State

Separate PHMSA Safety Orders from CAOs.

A Safety Order can direct corrective/remedial action after opportunity to respond to alleged integrity risk.

Priority: A

## W52P-E22 — Consent Order State

Track consent-order resolution and mandated corrective actions separately from adversarial final orders.

Priority: B+

## W52P-E23 — Incident-to-Enforcement Lead Time

Feature:
incident time
-> NRC/reportable incident
-> 30-day report
-> CAO/order publication.

Priority: S

## W52P-E24 — 30-Day Incident Revision Layer

PHMSA enforcement pages can link official 30-day incident reports.

Use later detailed fields as delayed truth/validation, never at accident onset.

Priority: A+

## W52P-E25 — Pipeline Mileage Exposure

Use PHMSA annual/operator mileage and NPMS summaries to estimate affected segment share of operator/system.

Priority: A

## W52P-E26 — High-Consequence-Area Severity

Weight event by whether affected pipeline can impact:
population,
drinking-water/ecological sensitive areas,
commercially navigable waterways.

Priority: A

## W52P-E27 — Commodity-Specific Capacity Loss

Separate:
dry gas,
wet gas/NGL context where known,
crude,
refined product,
CO2,
other hazardous liquid.

Priority: S

## W52P-E28 — Natural-Gas Basis Exposure

Map constrained gas segment to:
receipt/delivery points,
storage,
LNG,
power burn,
interstate alternatives.

Fuse with W22 gas transport.

Priority: S

## W52P-E29 — Crude / Product Basis Exposure

Map hazardous-liquid constraint to:
production basin,
refinery,
terminal,
storage hub,
export dock,
alternate pipeline/rail/barge.

Priority: S

## W52P-E30 — Pipeline Substitution Quotient

PSQ =
forced unavailable/restricted throughput
/
credible substitute transport capacity.

Priority: S

## W52P-E31 — Operator Network Redundancy

Estimate ability to reroute within same operator network.

Do not infer from corporate ownership alone; require topology/capacity evidence.

Priority: A+

## W52P-E32 — Restart-to-Flow Reality Gap

Legal restart approval
vs
actual nominations/flows/shipments.

A line can legally restart yet remain materially underutilized.

Priority: S

## W52P-E33 — Closure-to-Normalization Gap

PHMSA closes a CAO only after required actions are satisfactorily completed and facility is no longer considered hazardous, but commercial flow may normalize earlier or later.

Track separately.

Priority: A+

## W52P-E34 — Pipeline Integrity Risk Breadth

Aggregate active CAOs/Safety Orders by:
operator,
basin,
commodity,
interconnect,
region.

Priority: A

## W52P-E35 — Forced Pipeline Capacity Quotient

FPCQ =
probability-weighted capacity unavailable under regulatory/integrity constraints
/
available reroute + alternate transport capacity.

Priority: S

## W52P-E36 — Pipeline Enforcement Truth Ladder

INCIDENT/ANOMALY
-> REGULATOR ACTION
-> LEGAL OPERATING ENVELOPE
-> RESTART/RESTRICTION
-> ACTUAL FLOW
-> SUBSTITUTION
-> INVENTORY/BASIS
-> MARKET.

Priority: S architecture

## Highest-priority W52P tests

1. W52P-E03 Segment Shutdown State
2. W52P-E04 Forced Pressure Reduction
3. W52P-E05 Pressure-to-Capacity Translation
4. W52P-E06 Restart Approval Clock
5. W52P-E10 Restriction Removal Probability
6. W52P-E12 CAO Amendment Shock
7. W52P-E15 Repeated-Failure Escalation
8. W52P-E28 Natural-Gas Basis Exposure
9. W52P-E30 Pipeline Substitution Quotient
10. W52P-E32 Restart-to-Flow Reality Gap
