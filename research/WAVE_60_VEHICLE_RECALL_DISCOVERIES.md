# Wave 60V — Vehicle Defect, Recall & Production Spillover

Namespace: **W60V**

Thesis: road-vehicle safety defects progress through complaints, manufacturer communications, NHTSA investigations, recall decisions, remedy availability, completion, and sometimes production/sales restrictions. The financially relevant object is not simply recall count; it is **population × hazard severity × remedy cost × production disruption × supplier contagion × completion friction**.

All candidates are research hypotheses only. Claude owns later implementation.

## W60V-E01 — NHTSA Investigation State
Primary source:
NHTSA Office of Defects Investigation.

Normalize:
PRELIMINARY_EVALUATION
ENGINEERING_ANALYSIS
RECALL_QUERY
AUDIT_QUERY
INVESTIGATION_CLOSED
RECALL_INITIATED.

Priority: S

## W60V-E02 — Investigation Escalation Hazard
Estimate P(PE -> EA -> recall) from:
complaint trend,
crashes/injuries/fire allegations,
vehicle population,
manufacturer communications,
prior similar defects.

Priority: S

## W60V-E03 — Investigation Duration Surprise
Feature:
actual open duration
-
expected duration for comparable defect category.

Priority: A+

## W60V-E04 — Complaint Acceleration
Primary source:
NHTSA complaints API/data.

Measure new complaint velocity normalized by estimated vehicles in service.

Priority: S-

## W60V-E05 — Severe Complaint Mix
Weight:
death,
injury,
fire,
crash,
loss-of-propulsion,
steering/braking,
airbag/seatbelt,
electrical thermal event.

Priority: S-

## W60V-E06 — Manufacturer Communication Pulse
Primary source:
NHTSA manufacturer communications/TSBs.

Track emerging technical-service themes before formal recall.

Priority: A+

## W60V-E07 — Communication-to-Recall Conversion
Estimate probability a cluster of TSB/manufacturer communications becomes formal safety recall/investigation.

Priority: A

## W60V-E08 — Recall Population Shock
Primary source:
NHTSA recall campaign data.

Feature:
affected units
/
estimated U.S. parc or model-year sales.

Priority: S

## W60V-E09 — Hazard Severity State
Classify:
ROUTINE_REPAIR
FIRE_RISK
CRASH_RISK
LOSS_OF_CONTROL
AIRBAG
BRAKE/STEERING
DO_NOT_DRIVE
PARK_OUTSIDE
OTHER_HIGH_SEVERITY.

Priority: S

## W60V-E10 — Remedy Availability Gap
State:
RECALL_ANNOUNCED
INTERIM_NOTICE
REMEDY_NOT_AVAILABLE
REMEDY_AVAILABLE
PARTS_CONSTRAINED
REMEDY_COMPLETE.

Priority: S

## W60V-E11 — Recall Completion Friction
Use NHTSA completion-rate data where available.

Feature:
expected completion
-
actual completion
by age/population/severity/remedy.

Priority: A+

## W60V-E12 — Parts Demand Shock
Estimate replacement-part demand:
affected population
× expected completion
× parts per repair.

Map to known supplier where sourced.

Priority: S-

## W60V-E13 — Supplier Common-Mode Defect
Identify same component/supplier across multiple OEM recall campaigns.

Output:
OEM breadth,
vehicle breadth,
supplier concentration.

Priority: S

## W60V-E14 — Supplier Contagion Graph
Graph:
supplier/component
-> OEM
-> models
-> factories
-> recall campaigns.

Priority: S

## W60V-E15 — Production-Halt Probability
Some severe quality/safety defects can halt production or shipment.

Estimate probability using:
defect location in current model,
remedy part availability,
regulatory severity,
manufacturer communications.

Priority: S-

## W60V-E16 — Stop-Sale / Delivery-Hold State
Track public OEM/dealer/regulatory evidence of:
stop sale,
delivery hold,
quality hold,
port hold,
factory containment.

Priority: S

## W60V-E17 — Current-Model Exposure
A recall on current production has different operational risk from an old vehicle population.

Feature:
share of recall population from current/latest model years.

Priority: A+

## W60V-E18 — Warranty-Cost Envelope
Estimate:
parts
+ labor hours
+ logistics
+ dealer reimbursement
+ potential buyback
× expected completion.

Use ranges, not point certainty.

Priority: S

## W60V-E19 — Recall Reserve Reality Gap
Compare estimated recall/warranty exposure to company-disclosed warranty reserve/accrual revisions.

Priority: A+

## W60V-E20 — Dealer Inventory Immobilization
A stop-sale on in-stock vehicles creates dealer inventory that cannot be delivered.

Estimate:
affected dealer units
× days until remedy.

Priority: S-

## W60V-E21 — Sales Substitution to Competitors
Measure whether severe current-model recall/stop-sale shifts retail registrations to direct substitutes.

Priority: A+

## W60V-E22 — Used-Vehicle Price Spillover
Large recalls may alter used-vehicle pricing for affected models and substitutes.

Priority: B+

## W60V-E23 — EV Battery Thermal-Defect State
Specialize for EV packs:
fire risk,
state of charge restrictions,
park-outside instructions,
software mitigation,
module/pack replacement.

Priority: S-

## W60V-E24 — Software-Only vs Hardware Recall
Separate:
OTA/software remedy
from
dealer hardware replacement.

Cost and downtime differ materially.

Priority: S methodology/edge hybrid

## W60V-E25 — Recall Remedy Supply-Chain Constraint
If remedy depends on scarce component capacity:
estimate repair backlog and production competition for same part.

Priority: S

## W60V-E26 — Foreign Recall Lead
NHTSA manufacturer systems include foreign recalls/campaigns.

Research whether a foreign safety action precedes U.S. recall for globally shared platform/component.

Priority: A+

## W60V-E27 — Cross-OEM Defect Lead
When one OEM recalls a shared component:
estimate hazard for peer OEMs using same supplier/part/platform.

Priority: S

## W60V-E28 — Investigation / Recall Surprise
Compare event to ex ante hazard model.

States:
EXPECTED
EARLY
LATE
BROADER_THAN_EXPECTED
MORE_SEVERE_THAN_EXPECTED.

Priority: A+

## W60V-E29 — Production-Loss Quotient
PLQ =
estimated immobilized production/delivery capacity
/
available substitute inventory + alternate factories/models.

Priority: S

## W60V-E30 — Recall Financial-Loss Quotient
RFLQ =
expected retained recall/warranty/settlement cost
/
automotive segment earnings/cash generation.

Priority: S-

## W60V-E31 — OEM-Supplier Attribution Posterior
Maintain probability defect responsibility lies with:
OEM design,
supplier design,
supplier manufacturing,
software,
integration,
unknown.

Do not assign liability from rumor.

Priority: A

## W60V-E32 — Vehicle Defect Truth Ladder
COMPLAINT/COMMUNICATION
-> NHTSA INVESTIGATION
-> RECALL/STOP-SALE
-> REMEDY
-> COMPLETION
-> PRODUCTION/SALES LOSS
-> WARRANTY/CASH COST
-> RECOVERY.

Priority: S architecture

## Highest-priority W60V tests

1. W60V-E02 Investigation Escalation Hazard
2. W60V-E04 Complaint Acceleration
3. W60V-E08 Recall Population Shock
4. W60V-E10 Remedy Availability Gap
5. W60V-E13 Supplier Common-Mode Defect
6. W60V-E15 Production-Halt Probability
7. W60V-E18 Warranty-Cost Envelope
8. W60V-E25 Remedy Supply-Chain Constraint
9. W60V-E27 Cross-OEM Defect Lead
10. W60V-E29 Production-Loss Quotient
