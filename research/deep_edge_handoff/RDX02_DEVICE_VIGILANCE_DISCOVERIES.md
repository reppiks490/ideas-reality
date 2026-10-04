# RDX02 — Medical Device Vigilance & Remediation

Thesis: a medical-device recall is often preceded by a sequence of mandatory adverse-event reporting, safety communications, corrections/removals and remediation. FDA exposes a mix of weekly MAUDE/openFDA data, 5-day and 30-day manufacturer reporting clocks, early alerts, recall/correction records, shortage/discontinuance state and UDI/product identity.

## RDX02-E01 — MAUDE Adverse-Event Pulse
Use openFDA device-event weekly data. Normalize reports by device/product code, manufacturer, installed-base proxy and time-in-market.

## RDX02-E02 — Death / Serious-Injury / Malfunction Mix
Separate event-type composition rather than raw report count.

## RDX02-E03 — Adverse-Event Acceleration
Short-window event arrival rate and acceleration versus product-specific historical baseline.

## RDX02-E04 — New Failure-Mode Cluster
Cluster device problem codes, patient problem codes and narrative fields to detect emerging failure modes.

## RDX02-E05 — UDI-Level Defect Concentration
Use public UDI where present to localize events to a device family/version rather than whole manufacturer.

## RDX02-E06 — 30-Day MDR Clock
Manufacturers must report qualifying death, serious injury and malfunction events within 30 calendar days of awareness.

## RDX02-E07 — 5-Day Remedial-Action MDR
Events requiring remedial action to prevent unreasonable risk of substantial harm must be reported within 5 work days.

## RDX02-E08 — 5-Day / 30-Day Mix Shift
A rise in 5-day-type severe/remedial reports relative to ordinary 30-day MDRs may indicate escalating risk.

## RDX02-E09 — Reporter-Type Consensus
Compare manufacturer, user-facility, importer and voluntary reporter evidence for the same device/failure mode.

## RDX02-E10 — Device-Problem / Patient-Outcome Coupling
Estimate whether a device problem cluster is increasingly associated with serious patient outcomes.

## RDX02-E11 — Early Alert Before Confirmed Recall
FDA Medical Device Early Alerts can describe high-risk company actions before FDA has determined the action meets the regulatory definition of recall.

State: EARLY_ALERT -> RECALL_CONFIRMED / CORRECTION / CLOSED_OTHER.

## RDX02-E12 — Early-Alert Conversion Hazard
Target P(Early Alert becomes confirmed recall/correction) by product class, severity and event trajectory.

## RDX02-E13 — Safety Communication Escalation
FDA Safety Communication publication can signal agency-level concern beyond routine adverse-event accumulation.

## RDX02-E14 — Letter-to-Providers Escalation
Track FDA Letters to Health Care Providers for safety or availability concerns and later recall/shortage outcomes.

## RDX02-E15 — Correction vs Removal State
Separate field correction/software update/instruction change from physical market removal.

## RDX02-E16 — 21 CFR 806 Ten-Day Clock
Manufacturers/importers must report risk-to-health corrections/removals within 10 working days after initiating action.

## RDX02-E17 — Correction/Removal Scope Expansion
Predict amendment/extension to additional lots, serials or device families.

## RDX02-E18 — Recall Classification Severity
Class I / II / III classification changes economic and safety burden. Preserve classification-publication timing separately from company action date.

## RDX02-E19 — Recall Action Before FDA Classification
FDA recall database may include firm-initiated correction/removal before FDA classification. Treat action start and classification as distinct events.

## RDX02-E20 — Installed-Base Exposure
Estimate affected installed base using registration/listing, UDI, PMA/510(k), public company disclosures and procedure-volume proxies.

## RDX02-E21 — Consumable vs Capital-Equipment Burden
A disposable recall creates supply substitution; a capital-device correction can constrain installed clinical capacity.

## RDX02-E22 — Software vs Hardware Remediation
OTA/software/firmware corrections can have very different downtime and service economics from field replacement.

## RDX02-E23 — Service Technician Capacity Bottleneck
For field corrections, estimate devices requiring on-site service relative to certified/service capacity.

## RDX02-E24 — Device Shortage Interaction
Fuse recall/correction with FDA Medical Device Shortage List. Same defect is more economically consequential when substitutes are already scarce.

## RDX02-E25 — Discontinuance Interaction
A recalled product near permanent discontinuance may shift demand structurally rather than temporarily.

## RDX02-E26 — Substitute Manufacturer Demand Transfer
Map recalled/short device product code to verified substitute manufacturers/devices.

## RDX02-E27 — Clinical Procedure Capacity Loss
Translate unavailable device stock/capital equipment to procedure capacity for affected hospitals/therapeutic area.

## RDX02-E28 — Hospital Inventory Buffer
Estimate days of inventory/alternate devices before clinical capacity is impaired.

## RDX02-E29 — Device Recall Cost Envelope
Field service + replacement + freight + inventory write-down + warranty + customer credits + legal/regulatory + lost procedure/product revenue.

## RDX02-E30 — Supplier / Kit Contagion
A defective component can propagate into multiple finished devices or convenience kits. Build supplier-component-device graph.

## RDX02-E31 — Shared Sterility / Packaging Failure Graph
Certain recalls stem from packaging/sterility vendors affecting multiple manufacturers. Detect cross-manufacturer cluster.

## RDX02-E32 — Manufacturing-Site Risk State
Map recall/event clusters to manufacturing establishment where public; detect site-level quality contagion.

## RDX02-E33 — Warning-Letter Confirmation
FDA warning letters can later validate quality-system/correction-removal reporting failures; use publication time, not inspection date, in market-style research.

## RDX02-E34 — Recall-to-Shortage Cascade
RECALL/CORRECTION -> AVAILABLE STOCK LOSS -> SUBSTITUTE DEMAND -> SECONDARY SHORTAGE.

## RDX02-E35 — Shortage-to-Recall Fragility
Existing shortage can amplify the operational cost of a later safety correction.

## RDX02-E36 — Device Vigilance Truth Ladder
ADVERSE EVENT -> CLUSTER -> 5/30-DAY MDR -> EARLY ALERT/SAFETY COMMUNICATION -> CORRECTION/REMOVAL -> FDA RECALL CLASSIFICATION -> SHORTAGE/CLINICAL CAPACITY EFFECT -> FINANCIAL IMPACT.

## Highest-priority tests
E03, E07, E08, E11, E12, E16, E19, E24, E30, E36.
