# Wave 31C — Source Notes

Namespace: **W31C**

## W31C-D01 — OpenFEMA RI-IHP
Primary:
https://www.fema.gov/openfema-data-page/registration-intake-and-individuals-household-program-ri-ihp-v2

OpenFEMA metadata lists daily refresh. Aggregated fields include valid registrations and IHP/HA/ONA eligibility/amounts.

## W31C-D02 — Housing Assistance Owners/Renters
Primary:
https://www.fema.gov/openfema-data-page/housing-assistance-program-data-owners-v2
https://www.fema.gov/openfema-data-page/housing-assistance-program-data-renters-v2

Daily-refresh aggregated data include registration, inspection, severity and assistance fields by geography.

## W31C-D03 — Valid Registrations v2
Primary:
https://www.fema.gov/openfema-data-page/individuals-and-households-program-valid-registrations-v2

Rich applicant-level redacted fields include FEMA-determined damage, but documentation notes special coverage/refresh limitations for recent disasters. Treat as delayed richer truth layer.

## W31C-D04 — OpenFEMA API
Primary:
https://www.fema.gov/about/openfema/api

Free REST API. Preserve dataset metadata/last refresh semantics and source-specific update frequency.

## W31C-D05 — FEMA Disaster Declarations
Primary:
https://www.fema.gov/openfema-data-page/disaster-declarations-summaries-v2

OpenFEMA lists ~20-minute refresh for declaration summary data.

## W31C-D06 — NFIP Redacted Claims
Primary:
OpenFEMA FIMA NFIP Redacted Claims.

FEMA FAQ states NFIP claims/policy datasets are generally refreshed every 30–60 days and lag the system of record.

## W31C-D07 — Florida OIR Catastrophe Claims
Primary:
https://floir.com/office/hurricaneseason
https://floir.com/home/

OIR compels catastrophe claim data calls for designated storms and publishes aggregate snapshots with claim status and estimated/incurred losses.

## W31C-D08 — Florida Event Pages
Event-specific pages such as Hurricane Ian/Milton preserve cumulative claim/loss snapshots and reporting notices.

## W31C-D09 — Existing Physical-Damage Layers
Reuse W13H, W15X, W18G, W20E, W24M and FEMA/OpenFEMA physical/disaster sources for severity.

## W31C-D10 — Evidence Boundary
Academic catastrophe/insurer event studies motivate financial materiality. They do not substitute for current point-in-time exposure/loss reconstruction.
