# Wave 66D — Medical Device Safety, Recall & Procedure Capacity

Namespace: **W66D**

Thesis: medical-device failures can create a sequence from adverse-event accumulation to safety communication, correction/removal, formal recall, replacement/repair burden, hospital procedure disruption, shortage and revenue/cost impact. The economic object is not raw MAUDE count; it is **installed-base exposure × severity × remediation mode × substitute availability × clinical workflow dependence**.

W36P owns pharmaceutical manufacturing/shortage. W45F owns drug/biologic market entry. W66D owns **postmarket medical-device safety and device availability**.

All candidates are research hypotheses only. Claude owns later implementation.

## W66D-E01 — MAUDE Adverse-Event Pulse
Primary source:
FDA MAUDE / openFDA device event.

Build abnormal report velocity by:
manufacturer,
brand,
model,
product code,
problem code,
clinical outcome.

Priority: S-

## W66D-E02 — Death / Serious-Injury Mix
Separate:
DEATH
SERIOUS_INJURY
MALFUNCTION
OTHER/UNKNOWN.

Do not combine severity classes.

Priority: S

## W66D-E03 — Five-Day Report Share
Manufacturer MDR records can identify special five-day reporting category where public fields permit.

Feature:
five-day report share / change
within device family.

Priority: S-

## W66D-E04 — Thirty-Day Report Acceleration
Measure abnormal growth in ordinary mandatory manufacturer reports.

Priority: A+

## W66D-E05 — Supplemental-Report Revision
Follow-up reports can add investigation/cause information later.

Treat supplementation as new public information at update time.

Priority: A

## W66D-E06 — Problem-Code Concentration
Cluster recurring device failure modes:
battery,
software,
fracture,
occlusion,
leak,
false result,
alarm,
sterility,
other.

Priority: S-

## W66D-E07 — Model-Specific Common-Mode Hazard
Same problem code across many units/models can indicate common design/manufacturing failure.

Priority: S

## W66D-E08 — MAUDE-to-Safety-Communication Escalation
Target:
P(FDA safety communication | abnormal MDR cluster, severity, model breadth).

Priority: A+

## W66D-E09 — FDA Safety Communication State
Track:
INITIAL
UPDATE
RECOMMENDATIONS_CHANGED
RESOLVED/SUPERSEDED.

Priority: S

## W66D-E10 — Clinical Recommendation Severity
Normalize FDA recommendations:
MONITOR
SOFTWARE_UPDATE
INSPECT
STOP_USE
REMOVE/REPLACE
AVOID_NEW_IMPLANTATION
OTHER.

Priority: S

## W66D-E11 — Firm-Initiated Correction/Removal
Primary source:
FDA medical-device recall database.

State can appear before final FDA classification for some actions.

Priority: S

## W66D-E12 — Recall Classification
CLASS_I
CLASS_II
CLASS_III
UNCLASSIFIED/PENDING where source supports.

Priority: S

## W66D-E13 — Recall Posting-Lag Gap
FDA notes recall posting/create date may occur after the firm has already initiated and communicated the correction/removal.

Store:
firm initiation date
vs
FDA classification/posting date.

Priority: S methodology/edge hybrid

## W66D-E14 — Recall Population Exposure
Feature:
units affected
/
estimated installed or shipped population.

Use source-specific population estimates.

Priority: S

## W66D-E15 — Implanted-Device Exposure
Implanted devices have different remediation economics than external/disposable products.

Estimate active implanted population where public.

Priority: S-

## W66D-E16 — Recall Remedy Mode
Classify:
SOFTWARE/OTA
FIELD_CORRECTION
INSPECTION
ACCESSORY_REPLACEMENT
DEVICE_REPLACEMENT
EXPLANT/REVISION_SURGERY
RETURN/DESTROY.

Priority: S

## W66D-E17 — Remedy Burden Quotient
RBQ =
expected units needing remediation
× procedure/time/cost burden
/
available clinical/service capacity.

Priority: S

## W66D-E18 — Installed-Base Downtime
Estimate device-days unavailable or degraded during remediation.

Priority: A+

## W66D-E19 — Procedure Capacity Loss
For devices integral to procedures:
unavailable devices
× substitute-device scarcity
× hospital workflow dependence.

Examples:
oxygenators,
biopsy systems,
surgical devices,
imaging,
infusion,
dialysis.

Priority: S

## W66D-E20 — Device Shortage Entry
Primary source:
FDA Medical Device Shortages List.

State:
NORMAL
SHORTAGE_INITIAL
REVERIFIED/EXTENDED
IMPROVING
REMOVED.

Priority: S

## W66D-E21 — Shortage Duration Revision
Feature:
new estimated end
-
prior estimated end.

Priority: S-

## W66D-E22 — Permanent Discontinuance Shock
FDA maintains a public discontinuance list under device-shortage authorities.

Map manufacturer/device/product-code and substitute availability.

Priority: A+

## W66D-E23 — Recall × Shortage Collision
A device can be recalled while substitutes are already constrained.

This may create nonlinear procedure-capacity loss.

Priority: S

## W66D-E24 — Supplier Component Common-Mode Risk
Shortage/recall reason may identify shared components/accessories.

Graph:
component
-> manufacturers
-> devices
-> procedure types.

Priority: A+

## W66D-E25 — Hospital Substitute Capacity
Estimate:
alternative models/vendors
× compatibility
× training
× installed infrastructure
× inventory.

Priority: S-

## W66D-E26 — Consumable Dependency Shock
Capital equipment can become unusable when proprietary consumables/accessories are recalled or discontinued.

Priority: S

## W66D-E27 — Revenue-at-Risk Installed Base
Estimate:
affected installed units
× consumable/service/replacement revenue
rather than only shipment value.

Priority: A+

## W66D-E28 — Replacement Demand Transfer
Severe recall/discontinuance can shift demand to competitor devices if clinically substitutable.

Priority: S-

## W66D-E29 — Warranty / Field-Action Cost Envelope
Estimate:
field labor
+ software/support
+ replacement hardware
+ freight
+ procedure reimbursement
+ inventory write-off
+ legal/regulatory cost.

Priority: A+

## W66D-E30 — Procedure Deferral Signal
Where public operational data permit:
measure delayed/cancelled procedures linked to device scarcity or stop-use recommendations.

Priority: A

## W66D-E31 — Safety Reality Gap
Compare:
adverse-event severity
vs
recall class/remedy/shortage outcome.

Priority: S-

## W66D-E32 — Device Safety Truth Ladder
ADVERSE EVENT
-> MDR PUBLICATION
-> FDA/COMPANY SAFETY COMMUNICATION
-> CORRECTION/REMOVAL
-> RECALL CLASSIFICATION
-> REMEDIATION
-> DEVICE/PROCEDURE CAPACITY LOSS
-> SHORTAGE/SUBSTITUTION
-> COST/RECOVERY.

Priority: S architecture

## Highest-priority W66D tests

1. W66D-E01 MAUDE Adverse-Event Pulse
2. W66D-E03 Five-Day Report Share
3. W66D-E07 Model-Specific Common-Mode Hazard
4. W66D-E08 MAUDE-to-Safety-Communication Escalation
5. W66D-E13 Recall Posting-Lag Gap
6. W66D-E17 Remedy Burden Quotient
7. W66D-E19 Procedure Capacity Loss
8. W66D-E23 Recall × Shortage Collision
9. W66D-E26 Consumable Dependency Shock
10. W66D-E32 Device Safety Truth Ladder
