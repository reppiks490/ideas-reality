# Wave 8R Research Methods

Namespace: **W8R**

## W8R-M01 — Installed-Base Denominator
Raw complaint/event counts are invalid across products with different installed bases. Normalize by units sold/in service, fleet exposure, prescriptions or another defensible exposure denominator.

## W8R-M02 — Severity-Weighted Hazard
Predeclare severity weights for crash, fire, injury, death, malfunction and non-injury complaint classes. Test robustness to alternate weights.

## W8R-M03 — Public-Availability Clock
Maintain incident_time, submit_time, regulator_receive_time, QC/approval_time, posted_time and first_ingested_time separately. Only posted/available information can enter a historical feature.

## W8R-M04 — Administrative Record Versioning
NHTSA complaint records and other administrative records can change. Hash and archive each observed version; never overwrite history.

## W8R-M05 — Reporting-Delay Survival Correction
Estimate source-specific reporting-delay distributions and condition hazard models on them. A recent apparent drop may simply be right-censoring.

## W8R-M06 — Regulator Lifecycle State Machine
Use multi-state survival/competing-risk models for complaint -> investigation -> recall, SDR -> AD, event -> recall, and trial transitions.

## W8R-M07 — Next-Truth-Layer Validation
An early warning feature must first predict the next observable regulatory/operational state before it is allowed into a return-prediction experiment.

## W8R-M08 — Duplicate / Linked-Case Resolution
Resolve multiple reports tied to the same underlying incident, complaint, crash or product event. Keep provenance without double-counting.

## W8R-M09 — Reporting-Regime Breaks
Explicitly mark rule/schema/reporting changes such as new NHTSA fields, revised SGO requirements, FAA processing changes or FDA schema changes.

## W8R-M10 — Quality-Control Delay Model
For FAA SDR and similar feeds, model time from underlying report to public processed record. Do not backdate to difficulty date.

## W8R-M11 — Point-in-Time Clinical Trial Reconstruction
Rebuild each study from versions actually posted by each decision time. Separate submitted date, posted date and record-verification date.

## W8R-M12 — Trial Change Taxonomy
Classify record changes as administrative, operational, design, outcome, enrollment, timeline, safety or results. Administrative changes are a mandatory negative-control category.

## W8R-M13 — Sponsor-to-Issuer Mapping
Map trial sponsor/collaborator to public issuer with ownership/effective dates and economic materiality. Subsidiaries/licensing partners require explicit relationship records.

## W8R-M14 — Trial Portfolio Materiality
Weight a study by phase, indication, probability-adjusted value, company size and pipeline concentration rather than treating every trial equally.

## W8R-M15 — Therapeutic Substitution Graph
For shortages, distinguish exact generic substitution, formulation/strength substitution and clinical therapeutic alternatives. Encode substitution confidence.

## W8R-M16 — Shortage Vintage Archive
Archive FDA shortage snapshots/diffs daily. Use initial posting and first-seen status, not a later resolved record projected backward.

## W8R-M17 — Regulatory Action Materiality
Normalize recalls/ADs/actions by affected units/fleet/product revenue, remedy cost and operational downtime where measurable.

## W8R-M18 — Case-Control Event Matching
Match escalations to products with similar age, installed base, complaint baseline and category to reduce lifecycle/size confounding.

## W8R-M19 — Public-Complaint Bias Calibration
Account for publicity/notoriety effects: media coverage can alter complaint/adverse-event reporting intensity after a headline. Separate pre-event signal from post-event reporting reflex.

## W8R-M20 — Cross-Regulator Negative Controls
A vehicle complaint feature should not predict unrelated drug shortages; a clinical-trial administrative change should not predict unrelated aviation ADs. Use unrelated regulatory systems as placebo outcomes.
