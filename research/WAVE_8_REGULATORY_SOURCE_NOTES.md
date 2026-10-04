# Wave 8R Source Notes

Namespace: **W8R**

## W8R-D01 — NHTSA Consumer Complaints

Primary:
https://www.nhtsa.gov/nhtsa-datasets-and-apis

Official NHTSA complaint data are public and described as daily-frequency administrative data. The flat-file schema includes complaint receive/add dates, incident date, manufacturer/model/component, crash/fire/injury/death indicators and narrative fields.

Critical:
records are updateable; archive vintages.

## W8R-D02 — NHTSA Defect Investigations

Primary:
https://www.nhtsa.gov/nhtsa-datasets-and-apis

The investigation flat file covers safety-related investigations opened since 1972 and includes open/close date, manufacturer/model/component, subject/summary and resulting recall campaign number when applicable.

## W8R-D03 — NHTSA SGO ADS/ADAS Crash Reports

Primary:
NHTSA Standing General Order public crash-report datasets.

Use as periodic/lagged research data. Reporting requirements vary by automation level and records can be incomplete, duplicated or revised.

## W8R-D04 — FAA Service Difficulty Reporting System

Primary:
https://sdrs.faa.gov/
https://www.faa.gov/av-info/download_SDR

Public processed SDRs can be searched and yearly CSVs downloaded. Recently submitted reports are not public until FAA approval/QC, so difficulty date is not public availability time.

## W8R-D05 — FAA Dynamic Regulatory System

Primary:
https://drs.faa.gov/

DRS exposes Airworthiness Directives and AD NPRMs with manufacturer/model/product, issue/citation/effective metadata. Search result lists and biweekly reports can be exported/downloaded.

## W8R-D06 — ClinicalTrials.gov

Primary:
https://clinicaltrials.gov/data-api/about-api
https://clinicaltrials.gov/data-api/api

Official site supports current structured study data and public History of Changes pages with successive record versions/submission dates and changed modules.

Caution:
an internal JSON history endpoint was observable during research, but it is not treated here as a stable production API unless ClinicalTrials.gov documents it. Production research should rely on officially supported interfaces/archive access or a prospectively maintained archive.

## W8R-D07 — FDA Drug Shortages / openFDA

Primary:
https://open.fda.gov/apis/drug/drugshortages/
https://www.fda.gov/drugs/drug-safety-and-availability/drug-shortages

API endpoint:
https://api.fda.gov/drug/shortages.json

FDA states the shortage list is updated daily. Searchable fields include company, drug names, presentation, availability, reason, therapeutic category, dosage/strength, status and posting/change/resolution dates.

## W8R-D08 — openFDA Medical Device Events

Primary:
https://open.fda.gov/apis/device/event/

Use with strong reporting-delay caveats. Published research has documented substantial late manufacturer reporting in MAUDE-derived data.

## W8R-D09 — openFDA Device Recall / Enforcement

Primary:
https://open.fda.gov/apis/device/recall/
https://open.fda.gov/apis/device/enforcement/

Device recall fields include initiation/created/posted/termination dates, recalling firm, product identifiers, reason/root cause and action. Enforcement reports include regulatory classification and are updated on their own publication schedule.

## W8R-D10 — Point-in-Time Company / Product Exposure

This is not one feed. Claude should construct an explicit mapping layer:
regulatory entity/product/trial/device/component
-> legal entity
-> public issuer
-> affected revenue/fleet/installed base
with effective dates and confidence.

## Availability rules

- incident date != public date
- report submission != regulator posting
- ClinicalTrials.gov submission date != necessarily public posting date
- processed FAA SDR availability can lag event/report date
- MAUDE/device-event reporting can be materially delayed
- shortage current-state pages must be archived because later resolution changes the visible state
- administrative-data corrections must never rewrite the historical information set
