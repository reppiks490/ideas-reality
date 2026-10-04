# Wave 31C — Research Methods

Namespace: **W31C**

## W31C-M01 — Daily OpenFEMA Vintage Archive
Archive every RI-IHP/Housing Assistance snapshot by first-public time.

## W31C-M02 — Dataset Refresh != Source-System Event Time
OpenFEMA lastRefresh is API-store update time, not necessarily original FEMA system update time.

## W31C-M03 — Coverage Window Contract
Some rich FEMA datasets exclude very recent declarations or have special refresh rules.

Encode dataset-specific coverage explicitly.

## W31C-M04 — Registration Selection Bias
FEMA applicants are not all damaged households.

Model eligibility/application propensity.

## W31C-M05 — Inspection Completion Bias
Early inspections can be geographically/severity selected.

## W31C-M06 — Damage-Definition Versioning
FEMA program/rule changes alter assistance and damage fields across time.

## W31C-M07 — Disaster Declaration Geography
Only compare registrations within eligible/designated geographies at each point in time.

## W31C-M08 — Revision-as-Information
Every material change in cumulative claims/assistance estimate is a new event.

## W31C-M09 — NFIP Delay Gate
NFIP public claims refresh every 30–60 days under FEMA guidance.

Never expose them at storm onset.

## W31C-M10 — Coverage Scope Match
NFIP flood claims cannot validate wind loss directly.

## W31C-M11 — State Regulatory Snapshot Archive
Archive each Florida OIR catastrophe data call snapshot/report date.

## W31C-M12 — Incurred-vs-Paid Separation
Estimated/case incurred loss includes reserves plus paid amounts and differs from cash paid.

## W31C-M13 — Claim Count Deduplication
Track same catastrophe/line consistently across snapshot revisions.

## W31C-M14 — Public Insurer Exposure Gate
Require sourced state/line/geographic exposure before assigning catastrophe loss to a listed insurer.

## W31C-M15 — Reinsurance Terms Uncertainty
Do not infer exact retained loss without attachment/limit/participation data.

Use ranges.

## W31C-M16 — Inflation / Property-Value Normalization
Historical disaster comparisons require current-value normalization.

## W31C-M17 — Hazard-Type Split
Flood, wind, wildfire, convective storm and earthquake have different coverage structures.

## W31C-M18 — Physical Sensor Cross-Validation
Use existing Black Marble, FCC, grid, weather and infrastructure layers to test early damage nowcasts.

## W31C-M19 — Loss-Development Survival/Curve Model
Treat claim arrival and closure as time-to-event processes with right censoring.

## W31C-M20 — Financial Promotion Gate
Before return testing require OOS improvement in eventual:
damage,
claim count,
insured loss,
assistance,
restoration cost,
or credit loss.
