# RDX05 — Manufacturing Quality & Regulatory Capacity Risk

Thesis: regulated manufacturing capacity can become economically impaired before a recall or shortage appears. FDA inspection observations, final inspection classification, warning letters, import alerts and application-withholding consequences form a regulatory state machine that can remove or constrain productive capacity.

## RDX05-E01 — Inspection Event State
Facility inspection start/end, program area and surveillance/for-cause context.

## RDX05-E02 — 483 Observation Severity
Where a public Form 483 is actually available, classify observation count/type/risk significance without assuming every 483 becomes enforcement.

## RDX05-E03 — 483 Systemic-Quality Cluster
Detect recurring themes: data integrity, sterility/aseptic control, contamination, OOS investigations, quality-unit authority, validation, maintenance, supplier control.

## RDX05-E04 — Public-483 Availability Bias
Treat proactive/FOIA-posted 483s as a selected sample; absence is not clean inspection evidence.

## RDX05-E05 — Inspection Classification State
NAI / VAI / OAI by project area from FDA final classification database.

## RDX05-E06 — Classification Latency
Inspection-end -> public final classification. FDA says it strives to complete human-drug CGMP classification within ~90 days.

## RDX05-E07 — OAI Transition Shock
OAI = official/admin action recommended; quantify facility/product exposure.

## RDX05-E08 — VAI Persistence
Repeated VAI across inspections may indicate chronic but voluntarily correctable weakness.

## RDX05-E09 — OAI Recurrence
Repeated OAI at same facility or network may indicate persistent quality-system failure.

## RDX05-E10 — Multi-Project-Area Divergence
One inspection can have multiple project-area classifications. Preserve disagreement instead of collapsing to one label.

## RDX05-E11 — Warning-Letter Hazard
Estimate P(warning letter | inspection history, OAI, public observations, prior response).

## RDX05-E12 — Inspection-to-Warning-Letter Clock
Track inspection end, 483 response, warning-letter issue/publication separately.

## RDX05-E13 — Warning-Letter Severity Tensor
CGMP/systemic quality, sterility, data integrity, repeat violation, management responsibility, recall request, production suspension, application withholding.

## RDX05-E14 — Regulatory Escalation State
INSPECTION -> 483 -> VAI/OAI -> UNTITLED/WARNING LETTER -> IMPORT ALERT/INJUNCTION/SEIZURE/CONSENT DECREE.

## RDX05-E15 — Approval-Withholding Risk
FDA warning letters can state that new applications/supplements listing a noncompliant facility may be withheld until remediation/reinspection.

## RDX05-E16 — Pipeline/Product Approval Exposure
Map facility to pending/approved products relying on that site; estimate revenue/project timing at risk.

## RDX05-E17 — Export-Certificate Constraint
Some warning letters state FDA may withhold export certificates; map international distribution exposure.

## RDX05-E18 — Import Alert / DWPE State
For foreign facilities/products, Detention Without Physical Examination can block routine U.S. entry without shipment-by-shipment physical exam.

## RDX05-E19 — Import-Alert Entry Date
First public firm/product appearance on an Import Alert as a capacity/access shock.

## RDX05-E20 — Import-Alert Removal Hazard
Estimate time to removal from Red List / return to normal admissibility.

## RDX05-E21 — U.S.-Market Capacity Loss
Facility production capacity × U.S.-market dependence × regulatory access state.

## RDX05-E22 — Site Concentration Risk
Product portfolio dependence on one FEI/manufacturing site.

## RDX05-E23 — Alternate-Site Substitution
Estimate approved alternate manufacturing capacity and transfer/supplement time.

## RDX05-E24 — Sterile-Manufacturing Fragility
Sterile injectable/aseptic sites receive separate risk treatment because quality failures can create harder substitution/shortage dynamics.

## RDX05-E25 — API vs Finished-Dose Constraint
Separate active ingredient, excipient and finished-dose facilities; map which stage is binding.

## RDX05-E26 — Quality Shock × Shortage State
Fuse OAI/warning/import restriction with existing drug/device shortage layers.

## RDX05-E27 — Quality Shock × Competitor Spare Capacity
Same quality event is more material if substitutes lack spare approved capacity.

## RDX05-E28 — Facility-to-Product Graph
FEI -> product/application -> sponsor/marketer -> therapeutic class -> substitute products.

## RDX05-E29 — Contract Manufacturer Contagion
One CMO/CDMO quality event can affect multiple sponsors; build customer exposure with source confidence.

## RDX05-E30 — Quality-System Network Contagion
Common owner/quality system/process across facilities can create multi-site risk, but require evidence before propagating.

## RDX05-E31 — Reinspection Recovery Clock
Warning/OAI -> corrective action -> reinspection -> acceptable classification -> normal approval/import state.

## RDX05-E32 — Regulatory Recovery Half-Life
Measure time from enforcement shock to operational/regulatory normalization.

## RDX05-E33 — Production Suspension Confirmation
Some warning letters explicitly acknowledge/seek suspension or recall. Distinguish actual suspension from theoretical enforcement risk.

## RDX05-E34 — Recall/Shortage Escalation
Quality event -> recall -> supply interruption -> shortage -> substitute-demand transfer.

## RDX05-E35 — Data-Integrity Risk State
Data integrity findings can undermine broader release/validation confidence than one batch defect.

## RDX05-E36 — Remediation Cost Envelope
Consultants/remediation + batch rejection + revalidation + idle capacity + alternate sourcing + delayed approvals + recalls.

## RDX05-E37 — Quality Event / Equity Reaction Residual
Actual market reaction minus expected reaction conditioned on site/product materiality and substitution.

## RDX05-E38 — Regulatory Reality Gap
Facility receives severe regulatory status while market/products imply little operational effect—or market fears severe disruption while approved substitutes/alternate sites absorb it.

## RDX05-E39 — Supply-Critical Quality Quotient
SCQQ = probability-weighted capacity unavailable / approved substitute capacity.

## RDX05-E40 — Manufacturing Quality Truth Ladder
INSPECTION -> OBSERVATION -> FINAL CLASSIFICATION -> ENFORCEMENT -> MARKET-ACCESS/APPROVAL CONSTRAINT -> PRODUCTION LOSS -> SHORTAGE/RECALL -> FINANCIAL IMPACT.

## Highest-priority tests
E05, E07, E11, E15, E18, E21, E24, E29, E39, E40.
