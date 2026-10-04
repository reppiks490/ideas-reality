# Wave 36P — Pharmaceutical Manufacturing & Drug Availability

Namespace: **W36P**

Thesis: medicine supply can deteriorate through manufacturing quality failures, recalls, import restrictions, discontinuations, API/component shortages or demand surges before financial statements show the effect. The research target is physical product availability and substitution capacity, not generic FDA headline sentiment.

All candidates are research hypotheses only. Claude owns later implementation.

## W36P-E01 — FDA National Shortage Entry
Primary source:
FDA Drug Shortages database / openFDA Drug Shortages endpoint.

Detect first-public transition to CURRENTLY_IN_SHORTAGE.
Priority: S

## W36P-E02 — Shortage Resolution
Detect FDA transition to RESOLVED using public update date.
Priority: S-

## W36P-E03 — Presentation-Level Availability
Within one drug/active ingredient, track manufacturer and NDC/presentation states:
AVAILABLE
LIMITED_AVAILABILITY
BACKORDER
DISCONTINUED
OTHER_PUBLIC_STATE.
Priority: S

## W36P-E04 — Manufacturer Breadth Loss
Count active supplying manufacturers/presentations before and during shortage.
Priority: S

## W36P-E05 — Supply Concentration Shock
Feature:
share of public presentations/manufacturers unavailable
× pre-event supplier concentration estimate.
Priority: S

## W36P-E06 — Shortage Reason State
Use FDA-defined/public reasons such as:
CGMP requirement,
regulatory delay,
active ingredient shortage,
inactive component shortage,
discontinuation,
shipping delay,
demand increase.
Priority: A+

## W36P-E07 — Shortage Update Velocity
Count revisions/reverification events and availability-state changes over time.
Priority: A

## W36P-E08 — Estimated Resupply Revision
Archive manufacturer-provided estimated shortage/resupply statements.
Feature:
new expected availability - prior expected availability.
Priority: S-

## W36P-E09 — Persistent Shortage Age
Days from initial public posting to resolution/current date.
Priority: A+

## W36P-E10 — Therapeutic Substitution Capacity
Map therapeutically substitutable products where medically/regulatorily defensible.
Estimate:
remaining substitute supply / disrupted demand.
Priority: S

## W36P-E11 — Sole / Few-Supplier Fragility
Identify products with very low manufacturer/presentation redundancy.
Priority: S-

## W36P-E12 — Sterile-Injectable Fragility
Condition shortage risk on complex sterile injectable manufacturing and limited line substitution.
Priority: A+

## W36P-E13 — Recall Supply Removal
Primary source:
FDA Enforcement Reports/openFDA drug enforcement.

Estimate units/lots/geography removed when publicly quantifiable.
Priority: S-

## W36P-E14 — Recall Classification Severity
Separate Class I / II / III and market withdrawal where source supports it.
Severity is not equivalent to supply volume.
Priority: A

## W36P-E15 — Recall-to-Shortage Escalation
Target:
P(FDA national shortage after public recall/manufacturing action).
Priority: S

## W36P-E16 — Inspection OAI Manufacturing-Risk State
Primary source:
FDA Inspections Data Dashboard.

OAI indicates official action recommended for the classified project area.
Use only once final classification is public.
Priority: A+

## W36P-E17 — VAI/OAI Transition
Track facility compliance history:
NAI -> VAI -> OAI
and recovery classifications where later available.
Priority: A

## W36P-E18 — Form 483 Observation Pulse
Use publicly posted Form 483s only, with publish date.
A 483 contains inspectional observations and is not a final enforcement conclusion.
Priority: A

## W36P-E19 — Warning Letter Escalation
Track drug-manufacturing warning letters by firm/facility and cited quality systems.
Priority: A+

## W36P-E20 — Import Alert Supply Gate
Primary source:
FDA Import Alerts.

State:
NOT_LISTED
RED_LIST / DWPE where applicable
EXCEPTION/GREEN_LIST where applicable
REMOVED.
Priority: S-

## W36P-E21 — Foreign Facility Import Dependence
Map U.S. products/manufacturers to foreign manufacturing sites only with verified regulatory/product identifiers.
Priority: S

## W36P-E22 — Import Restriction × Low Redundancy
Import alert affecting a high-dependence site with few alternate suppliers.
Priority: S

## W36P-E23 — API vs Finished-Dose Bottleneck
Separate:
API manufacturing disruption
from
finished dosage manufacturing disruption.
Priority: S-

## W36P-E24 — Demand-Surge Shortage
Classify shortages driven primarily by demand increase separately from quality/supply failure.
Priority: A+

## W36P-E25 — Competitor Substitution Opportunity
For firms with approved substitute presentations and spare capacity:
estimate addressable volume transferred from constrained supplier.
Priority: S-

## W36P-E26 — Hospital Procurement Pressure
For hospital-critical injectables:
shortage breadth
× substitute scarcity
× clinical criticality.
Target procurement/usage outcomes before equity.
Priority: A+

## W36P-E27 — Shortage Recovery Half-Life
After FDA resolution:
measure normalization of presentation availability, wholesaler/procurement state and manufacturer shipments/revenue where observable.
Priority: A

## W36P-E28 — Regulatory-to-Supply Reality Gap
Compare:
inspection/warning/import action
vs
actual public product availability and shortage state.
Priority: S

## W36P-E29 — Drug Supply Resilience Quotient
DSRQ =
verified available substitutable supply capacity
/
current and projected treatment demand.

Priority: S

## W36P-E30 — Pharmaceutical Supply Truth Ladder
FACILITY/INPUT RISK
-> PRODUCT AVAILABILITY
-> NATIONAL SHORTAGE
-> SUBSTITUTE UTILIZATION
-> PROCUREMENT/PRICE EFFECT
-> REVENUE/MARGIN EFFECT
-> MARKET.

Priority: S architecture

## Highest-priority W36P tests
1. W36P-E01 FDA National Shortage Entry
2. W36P-E03 Presentation-Level Availability
3. W36P-E04 Manufacturer Breadth Loss
4. W36P-E08 Estimated Resupply Revision
5. W36P-E10 Therapeutic Substitution Capacity
6. W36P-E15 Recall-to-Shortage Escalation
7. W36P-E16 Inspection OAI Manufacturing-Risk State
8. W36P-E22 Import Restriction × Low Redundancy
9. W36P-E29 Drug Supply Resilience Quotient
10. W36P-E30 Pharmaceutical Supply Truth Ladder
