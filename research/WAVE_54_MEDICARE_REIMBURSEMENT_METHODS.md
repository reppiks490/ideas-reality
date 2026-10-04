# Wave 54C — Research Methods

Namespace: **W54C**

## W54C-M01 — Six-Clock Ledger
Store separate timestamps for:
coverage,
coding,
benefit category,
payment,
effective date,
claims observation.

## W54C-M02 — Proposed vs Final
Never expose proposed NCD/LCD/HCPCS determinations as final policy.

## W54C-M03 — Effective Date vs Publication
A favorable final decision may not be billable/effective immediately.

## W54C-M04 — National vs Local Coverage
NCD and LCD authority differ.

Preserve MAC jurisdiction and applicable contractor at event time.

## W54C-M05 — Weekly MCD Vintage Archive
Archive CMS current/retired NCD, LCD and Article datasets by public release date.

## W54C-M06 — LCD Version Chain
Track:
draft,
final,
effective,
retired,
reconsidered,
superseded.

## W54C-M07 — Coverage Population Denominator
Use Medicare FFS jurisdictional beneficiaries/providers when evaluating LCD breadth.

Do not silently include MA.

## W54C-M08 — HCPCS Decision Chain
Separate application, preliminary determination, public meeting, final determination, code-set publication and effective date.

## W54C-M09 — Code Identity Versioning
HCPCS codes can be revised/deleted/reused in evolving contexts.

Maintain code-description history.

## W54C-M10 — Code != Coverage
CMS explicitly distinguishes coding from insurer coverage.

Never infer coverage from code assignment.

## W54C-M11 — Benefit Category Gate
Payment requires statutory/benefit-category eligibility in addition to a code.

## W54C-M12 — OPPS Quarterly Vintage
Archive Addendum A/B/Q snapshots each quarter.

## W54C-M13 — Status Indicator Semantics
Interpret status indicators under the rule version effective for the quarter.

## W54C-M14 — Pass-Through Lifecycle
Track first effective quarter and termination/packaging transition.

## W54C-M15 — NTAP Fiscal-Year Lifecycle
Use IPPS fiscal-year final-rule implementation files; do not map calendar year casually.

## W54C-M16 — ASP Vintage Archive
Archive every quarterly payment file and later revision.

## W54C-M17 — ASP Payment Scope
ASP-based Part B payment applies to separately payable covered Part B drugs/biologicals under specific settings/rules.

Do not generalize to all drug revenue.

## W54C-M18 — Claims Maturity Model
Preliminary quarterly claims have runout and revisions.

Estimate completion using historical maturity curves.

## W54C-M19 — Privacy Suppression
CMS suppresses some low-volume beneficiary/claim counts.

Treat missing/suppressed separately from zero.

## W54C-M20 — MA Scope Boundary
FFS public claims/utilization is incomplete for Medicare Advantage.

## W54C-M21 — Launch Cohort Control
New products naturally ramp after launch.

Compare reimbursement changes against matched launch cohorts.

## W54C-M22 — Supply Constraint Control
Weak claims after favorable reimbursement may reflect manufacturing/distribution constraints.

Fuse W36 pharma supply where relevant.

## W54C-M23 — Clinical Eligibility Control
Coverage expansion matters only for patients meeting indication/coverage criteria.

## W54C-M24 — Competing Therapy Control
Substitute launch or guideline changes can dominate reimbursement effects.

## W54C-M25 — Site-of-Care Cost Model
Provider economics differ materially by care setting.

## W54C-M26 — Product-to-Code Entity Resolution
Map manufacturer product, NDC, HCPCS, procedure and indication with provenance.

## W54C-M27 — Same-Code Competitor Problem
Multiple drugs/products may share or transition through codes.

Avoid assigning code-level utilization to a single manufacturer without validated mapping.

## W54C-M28 — Coverage Language NLP Validation
Coverage criteria are legal/clinical text; machine extraction requires manual validation for material changes.

## W54C-M29 — Decision Calendar Pre-Registration
Known due/effective dates must be known before testing event-window effects.

## W54C-M30 — Intermediate Promotion Gate
Before financial alpha require OOS improvement in:
coverage breadth,
payment amount,
provider economics,
claims utilization,
or utilization-to-revenue translation.
