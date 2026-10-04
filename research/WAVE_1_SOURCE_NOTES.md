# Wave 1 — Source Notes and Availability Audit

Namespace: **W1**
Purpose: bring the legacy Edge Atlas under the current source-provenance standard.

## W1-D01 — FINRA TRACE Treasury
Primary:
https://www.finra.org/finra-data/browse-catalog/treasury-daily-aggregates
https://www.finra.org/finra-data/browse-catalog/treasury-transaction-level-data

Use exact product access/latency terms. The Edge Atlas already limits free/public transaction-level use to its documented delayed/next-day form.

## W1-D02 — U.S. Treasury Daily Treasury Statement
Primary:
https://fiscaldata.treasury.gov/datasets/daily-treasury-statement/

PUBLIC_SCHEDULED. Preserve record date and publication vintage.

## W1-D03 — Port of Los Angeles Signal/Horizon
Primary:
https://www.portoflosangeles.org/business/supply-chain/port-optimizer

PUBLIC_WEB_ONLY unless a production data/API contract is separately verified. Archive forecast vintages prospectively.

## W1-D04 — USGS Water Data / USACE Locks
Primary:
https://api.waterdata.usgs.gov/
https://ndc.ops.usace.army.mil/ords/r/lpms/corps-locks/home

Use source-specific telemetry/publication contracts from later physical-network waves.

## W1-D05 — Grid Sources
Primary:
https://www.eia.gov/electricity/gridmonitor/
https://www.pjm.com/
https://www.ercot.com/
https://www.caiso.com/

Do not collapse their different publication clocks. Reuse later W7T/W23T/W24A contracts.

## W1-D06 — NASA Black Marble
Primary:
https://blackmarble.gsfc.nasa.gov/

Near-real-time product availability and exact collection/product version must be pinned per product before live use.

## W1-D07 — Cloudflare Radar
Primary:
https://developers.cloudflare.com/radar/

API access requires current Cloudflare credentials/terms. Reuse W34D timing and outage-validation semantics.

## W1-D08 — OpenFEMA
Primary:
https://www.fema.gov/about/openfema/api

Dataset-specific refresh/coverage governs; do not label all OpenFEMA products equally live. Reuse W31C.

## W1-D09 — SEC EDGAR APIs
Primary:
https://www.sec.gov/search-filings/edgar-application-programming-interfaces

Use EDGAR acceptance/public dissemination timestamp and SEC fair-access policy.

## W1-D10 — NHTSA Recalls
Primary:
https://www.nhtsa.gov/nhtsa-datasets-and-apis

Use recall/publication timestamps, not manufacturer internal determination date unless public.

## W1-D11 — SEC Form N-PORT
Primary:
https://www.sec.gov/data-research/sec-markets-data/form-n-port-data-sets

PUBLIC_DELAYED/periodic under the rule effective at each date. Reuse W39F.

## W1-D12 — NY Fed Primary Dealer Statistics
Primary:
https://www.newyorkfed.org/markets/primarydealer_stats

PUBLIC_SCHEDULED weekly with publication lag; structural state only.

## W1-D13 — FINRA SLATE
Primary:
https://www.finra.org/filing-reporting/slate

WATCH_NOT_LIVE under the launch date currently documented by FINRA. No present-time feature use.

## W1-D14 — Korea Semiconductor Export Pulse

Status: PROVENANCE_PENDING in W1 until the exact reproducible official Korea Customs/Korean government source, machine access path, English/Korean field semantics, and first-10/20-day publication clock are pinned.

The hypothesis remains; live/source-verified status is withdrawn until that contract exists.

## W1-D15 — Indeed Hiring Lab Daily Labor Demand

Status: RIGHTS_TIMING_PENDING.

Do not assume public production/API rights or immutable historical vintages from a chart/article. Candidate may be researched only after exact dataset access, methodology and revision contract are archived.

## W1 source-quality consequence

Any W1 candidate relying on D14 or D15 is not DATA_VERIFIED. This is an intentional downgrade rather than invented provenance.
