# Wave 48A — Airworthiness & Fleet Availability

Namespace: **W48A**

Thesis: aviation capacity can change abruptly when regulators or manufacturers identify unsafe conditions, mandate inspections/repairs, restrict operation, prohibit special-flight permits, or require repetitive maintenance. The useful edge is the fraction of economically relevant fleet capacity that becomes unavailable, for how long, and how quickly operators can comply.

The research target is not "aircraft problem = stock down." It is the exact path from defect evidence to mandatory action to tail-level fleet availability and operational substitution.

All candidates are research hypotheses only. Claude owns any later implementation.

## W48A-E01 — FAA Service Difficulty Defect Pulse

Primary source:
FAA Service Difficulty Reporting System (SDRS).

Build:
new reports
by make/model,
ATA/JASC system,
part number,
failure mode,
operator type,
difficulty date.

Priority: S-

## W48A-E02 — Repeated Part Failure Acceleration

Feature:
same part number / same failure mode
report-rate acceleration
normalized by installed-fleet exposure where possible.

Priority: S

## W48A-E03 — Cross-Operator Defect Breadth

A defect reported by multiple independent operators may be more informative than repeated reports from one operator.

Priority: A+

## W48A-E04 — SDR Narrative Severity Classifier

Classify public SDR narratives into:
inspection finding,
in-flight malfunction,
unscheduled landing,
engine shutdown,
smoke/fire,
structural damage,
control impairment,
other.

Priority: A

## W48A-E05 — SDR-to-FAA Action Hazard

Target:
P(SAIB/AD/Emergency AD within N days | defect pulse).

This is an intermediate regulatory outcome, not market alpha.

Priority: S

## W48A-E06 — SAIB Advisory State

FAA Special Airworthiness Information Bulletins are non-mandatory advisories.

State:
NO_ADVISORY
SAIB_ACTIVE
SAIB_REVISED
SAIB_WITHDRAWN.

Priority: A

## W48A-E07 — Advisory-to-Mandatory Escalation

Track:
SAIB / service difficulty evidence
-> AD NPRM
-> immediate final rule
-> Emergency AD.

Priority: S-

## W48A-E08 — AD NPRM Probability State

FAA may publish an AD NPRM before final rule.

Research:
probability proposed action becomes final,
scope changes,
compliance-time changes.

Priority: A

## W48A-E09 — Final Rule AD Effective Clock

Track:
publication,
effective date,
applicability,
required actions,
compliance deadline,
supersedure.

Priority: S

## W48A-E10 — Emergency AD Actual-Notice Clock

FAA Emergency ADs can become effective to affected owners/operators when actually received before Federal Register publication.

Maintain:
EAD issue time,
actual-notice uncertainty,
later universal Federal Register effective date.

Priority: S

## W48A-E11 — Immediate Grounding vs Inspection Distinction

Classify AD requirement:
NO_FLIGHT_UNTIL_COMPLIANT
INSPECT_WITHIN_HOURS/CYCLES
REPETITIVE_INSPECTION
OPERATING_LIMITATION
PART_REPLACEMENT
SOFTWARE/PROCEDURE
OTHER.

Priority: S architecture

## W48A-E12 — Compliance Window Compression

Feature:
required compliance hours/cycles/calendar time
relative to
operator utilization.

Short windows create more acute maintenance-capacity demand.

Priority: S

## W48A-E13 — Special Flight Permit Restriction

Some ADs prohibit special flight permits.

State:
FERRY_ALLOWED
FERRY_RESTRICTED
FERRY_PROHIBITED.

This affects ability to reposition aircraft for repair.

Priority: A+

## W48A-E14 — Repetitive Inspection Burden

Estimate:
inspection labor-hours
× affected tails
× interval frequency
× downtime per event.

Priority: S-

## W48A-E15 — Terminating Action Capacity Relief

Some ADs allow a modification/replacement that ends repetitive inspections.

Model:
temporary downtime
vs
persistent recurring burden.

Priority: A+

## W48A-E16 — Tail-Level Applicability Resolver

Map AD applicability to exact registered aircraft where possible using:
make,
model,
serial range,
installed component,
configuration,
modification state.

Priority: S

## W48A-E17 — FAA Registry Fleet Denominator

Primary source:
FAA aircraft registry / downloadable registration data.

Estimate active U.S.-registered exposure by make/model/serial.

Priority: S infrastructure

## W48A-E18 — Global Fleet Exposure

For non-U.S. fleets:
combine EASA/other authority applicability and public operator fleet data.

Use source confidence; do not extrapolate U.S. registry globally.

Priority: A+

## W48A-E19 — Operator Affected-Fleet Fraction

Feature:
affected compliant/noncompliant tails
/
operator active fleet.

Priority: S

## W48A-E20 — Seat / Cargo Capacity at Risk

Translate tails into:
available seat miles,
cargo payload,
route criticality,
spare-aircraft buffer.

Priority: S

## W48A-E21 — Spare Fleet Substitution Capacity

Estimate:
unaffected spare aircraft
+ wet lease/charter options
+ schedule flexibility
+ substitute gauge.

Priority: A+

## W48A-E22 — Maintenance-Slot Constraint

Mandatory work may bottleneck on:
MRO capacity,
parts,
certified technicians,
special tooling,
inspection equipment.

Priority: S-

## W48A-E23 — Parts Availability Constraint

Map AD-required replacement/repair to:
part number,
OEM/supplier,
lead time,
installed base,
alternate approved parts.

Priority: S

## W48A-E24 — Supplier Shock Propagation

An AD on an aircraft/engine/system can affect:
airframe OEM,
engine OEM,
component supplier,
MRO,
airline operator,
lessor.

Map causal exposure, not just industry labels.

Priority: S-

## W48A-E25 — Lessor Fleet Concentration Risk

Estimate lessor exposure to affected aircraft family/component.

Target:
lease-rate,
placement,
maintenance reserve,
return-condition stress.

Priority: A

## W48A-E26 — Fleet Grounding Breadth

Aggregate:
affected tails
× operator concentration
× airport/route concentration
× duration.

Priority: S

## W48A-E27 — Return-to-Service Velocity

After mandated work:
tails returned per day
/
affected fleet.

Priority: S

## W48A-E28 — Reinspection / Repeat-Failure Hazard

After compliance:
track repeated SDRs, revised ADs or new unsafe-condition findings.

Priority: A+

## W48A-E29 — Superseding AD Severity Change

When a new AD supersedes an older one:
compare:
scope,
compliance time,
required action,
special-flight restrictions,
repetitive interval.

Priority: S-

## W48A-E30 — FAA vs EASA Timing Gap

Same unsafe condition may produce EASA and FAA actions at different times/scopes.

Track:
first authority action,
second authority adoption,
scope difference.

Priority: S

## W48A-E31 — Authority Divergence State

If EASA requires action and FAA does not, or vice versa:
preserve divergence as uncertainty/research feature.

Do not assume one regulator is correct.

Priority: A+

## W48A-E32 — Incident-to-Directive Lead Time

Track:
occurrence/report
-> SDR/public safety evidence
-> regulator action
-> effective compliance.

Priority: S

## W48A-E33 — Fleet Availability Shock Quotient

FASQ =
economically relevant fleet capacity unavailable
/
credible substitute capacity.

Priority: S

## W48A-E34 — Aviation Reality Gap

Compare:
legal compliance state
vs
actual schedule/capacity recovery.

An AD can be complied with while operational disruption persists because of backlog/parts/MRO constraints.

Priority: A+

## W48A-E35 — Airworthiness Truth Ladder

DEFECT REPORT
-> REGULATORY CONCERN
-> AD/EAD
-> TAIL APPLICABILITY
-> COMPLIANCE ACTION
-> FLEET AVAILABILITY
-> SCHEDULE/CARGO IMPACT
-> FINANCIAL EFFECT.

Priority: S architecture

## Highest-priority W48A tests

1. W48A-E02 Repeated Part Failure Acceleration
2. W48A-E05 SDR-to-FAA Action Hazard
3. W48A-E10 Emergency AD Actual-Notice Clock
4. W48A-E12 Compliance Window Compression
5. W48A-E16 Tail-Level Applicability Resolver
6. W48A-E19 Operator Affected-Fleet Fraction
7. W48A-E22 Maintenance-Slot Constraint
8. W48A-E23 Parts Availability Constraint
9. W48A-E27 Return-to-Service Velocity
10. W48A-E33 Fleet Availability Shock Quotient
