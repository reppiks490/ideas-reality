# Wave 13H — Source Notes

Namespace: **W13H**

## W13H-D01 — U.S. Department of Labor WARN
Primary:
https://www.dol.gov/agencies/eta/layoffs/warn
https://www.dol.gov/general/topic/termination/plantclosings

Federal WARN generally requires covered employers to provide at least 60 calendar days advance notice for qualifying events, with statutory/regulatory exceptions.

There is no single complete federal public WARN event database. Research must ingest official state workforce-agency publications individually.

## W13H-D02 — Official State WARN Publications
Examples differ by state in schema and revision handling.

Prefer state labor/workforce agency CSV/API/table/file sources.

Useful fields can include:
company,
city/county,
affected workers,
notice date,
layoff/closure type,
effective date,
NAICS,
revision type.

Coverage is incomplete by design because not every layoff triggers WARN.

## W13H-D03 — DOL Weekly Unemployment Insurance Claims
Primary low-latency release:
https://www.dol.gov/ui/data.pdf

Open data:
https://dataportal.dol.gov/datasets/10305

DOL describes initial claims as a leading economic indicator. Advance data are followed by revised state reporting.

## W13H-D04 — Federal Reserve Labor-Market Stress Evidence
2025 FRBSF research:
"A New Labor Market Stress Indicator"

The paper uses the breadth/depth of accelerating state UI claims to build a high-frequency labor-stress measure. Treat as methodological evidence, not proof of market alpha.

## W13H-D05 — CDC National Wastewater Surveillance System
Primary:
https://www.cdc.gov/wastewater/about-data/
https://data.cdc.gov/

CDC says public wastewater dashboards are generally updated every Friday with the previous week's data and provides downloadable/API datasets.

Coverage includes SARS-CoV-2, Influenza A and RSV, among other pathogens/dashboards.

## W13H-D06 — Wastewater Lead-Time Evidence
Peer-reviewed 2024 U.S. research found SARS-CoV-2 wastewater concentrations often preceded hospitalization admissions by several days, with heterogeneous state-level lags.

Use to motivate lead-state research; independently re-estimate in point-in-time CDC data.

## W13H-D07 — Workforce-Absence Evidence
Recent research has linked COVID wastewater viral activity to health-related work absences.

2026 research also reports predictive information from community influenza wastewater for school attendance, but it is exploratory and should not be generalized automatically to workplace absence.

## W13H-D08 — FCC Disaster Information Reporting System
Primary:
https://www.fcc.gov/general/disaster-information-reporting-system-dirs-0

DIRS collects operational/restoration status from communications providers during major disasters. Mandatory reporting for cable, wireless, wireline and interconnected VoIP providers took effect in 2025 under the current framework.

## W13H-D09 — FCC Communications Status Reports
FCC publishes event-specific status reports during DIRS activations.

Recent reports include:
cell sites served/out,
cause categories,
backup-power sites,
cable/wireline subscribers out,
911/PSAP impact,
broadcast status.

During active events the FCC has published daily updates until deactivation.

## W13H-D10 — Public Infrastructure Cross-Checks
Use W13H together with existing repo sources:
Cloudflare Radar,
NASA Black Marble,
EIA/PJM/ERCOT grid data,
FAA/port/rail telemetry,
weather/disaster sources.

Do not duplicate their raw-source implementations in this wave.
