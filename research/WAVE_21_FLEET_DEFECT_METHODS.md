# Wave 21D — Research Methods

Namespace: **W21D**

## W21D-M01 — Safety-Action Clock
Store:
defect occurrence/discovery,
manufacturer determination,
regulator receipt,
public issue,
effective date,
compliance deadline.

## W21D-M02 — Emergency Actual-Notice Rights Gate
Emergency AD private/actual notice to an operator is not public market information by default.

Use only public availability for public-data backtests.

## W21D-M03 — Applicability Parser
Parse make/model/series/serial/product applicability exactly.

Do not score the entire model family if only a subset is affected.

## W21D-M04 — Compliance Severity Taxonomy
Normalize:
before further flight,
flight-hour/cycle deadline,
calendar deadline,
repetitive inspection,
conditional repair.

## W21D-M05 — Registry Vintage Archive
FAA registry refreshes daily; archive snapshots.

Current registry cannot reconstruct past fleet composition perfectly.

## W21D-M06 — Owner-vs-Operator Gate
Do not equate registered owner/lessor with operating airline.

Require operator mapping confidence.

## W21D-M07 — Tail-Level Capacity Weight
Weight aircraft by seat/cargo capability and normal utilization.

## W21D-M08 — MRO Capacity Model
Estimate maintenance bottlenecks from:
task hours,
special tooling,
qualified shops,
parts,
geography.

## W21D-M09 — SDR Public-Availability Mask
FAA warns recently submitted SDRs are not public until approved.

Archive first-public time if using SDR as a precursor.

## W21D-M10 — SDR Reporting-Lag Model
Part 121/135 reports can be submitted within the next 96 hours; repair stations similarly have 96-hour requirements for serious defects.

Event date != public date.

## W21D-M11 — Duplicate Defect Clustering
Multiple reports may describe the same aircraft/part/event.

Deduplicate before estimating incidence.

## W21D-M12 — Exposure Denominator
Defect counts require fleet/cycle exposure denominator.

Raw report counts favor common aircraft.

## W21D-M13 — AD Precursor Leakage Guard
Once an AD investigation is public, later SDRs are not valid "pre-AD" evidence for that same event without timestamp discipline.

## W21D-M14 — NHTSA Recall Vintage
Archive Part 573 reports and amendments by public date.

## W21D-M15 — Potential-vs-Actual Units
Potential units affected is not confirmed defective count.

Keep both.

## W21D-M16 — Remedy Availability State
Separate:
remedy designed,
parts/tool available,
dealer/MRO ready,
owner notified,
repair completed.

## W21D-M17 — Supplier Identity Confidence
Use explicit public supplier attribution only.

No inference from part similarity alone.

## W21D-M18 — Production/Field Separation
A field recall and production-line containment can have different effects.

Model separately.

## W21D-M19 — Physical Utilization Validation
Validate fleet-capacity hypotheses against actual flights/vehicle activity/maintenance outcomes where available.

## W21D-M20 — Financial Promotion Gate
Promote only after demonstrating incremental prediction of unavailable capacity, maintenance backlog or operational throughput.
