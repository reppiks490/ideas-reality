# Wave 13H — Research Methods

Namespace: **W13H**

## W13H-M01 — WARN Coverage Mask
WARN does not capture all layoffs.

Encode:
employer-size coverage,
event-size thresholds,
temporary-project exclusions,
state mini-WARN differences,
known exception invocation.

Never interpret no WARN notice as no layoffs.

## W13H-M02 — Notice-Time vs Effective-Time
Store:
notice_received,
public_posted,
planned_effective,
revised_effective,
actual_effective when knowable.

## W13H-M03 — State-Source Provenance
WARN publication is decentralized.

Every notice records:
state agency,
source URL/file,
retrieval time,
source row/document identity,
revision lineage.

Third-party aggregators can aid discovery but may not replace official provenance in promoted research.

## W13H-M04 — Entity Resolution Gate
Company legal name, subsidiary and facility owner can differ.

Map:
legal employer
-> parent
-> ticker
with source/effective dates/confidence.

## W13H-M05 — Layoff Seasonality / Contract-Completion Control
Control for:
seasonal plants,
known contract completions,
temporary facilities,
M&A duplication,
annual restructurings.

## W13H-M06 — Expected Claims from WARN
Estimate historical WARN-to-UI conversion by state/industry/event type.

Use this as expected claims, not a one-for-one mapping.

## W13H-M07 — Claims Vintage Ledger
Store advance and revised UI claims separately.

Do not overwrite the advance release with revised history.

## W13H-M08 — Claims Holiday/Seasonality Control
State weekly claims are volatile and holiday-sensitive.

Use robust seasonal/holiday baselines and geographic breadth.

## W13H-M09 — Wastewater Publication Mask
Store:
sample collection period,
measurement/report period,
CDC publication date,
first ingested time,
later revisions.

## W13H-M10 — Sewershed Coverage Weight
Weight site-level wastewater by represented population and coverage reliability.

Do not treat 1,500 sites as equal-sized observations.

## W13H-M11 — Pathogen-Specific Model
SARS-CoV-2, Influenza A and RSV receive separate coefficients, lags and validation.

No generic "illness index" until incremental effects are established.

## W13H-M12 — Wastewater Lead-Lag Pre-Registration
Choose the lag-search range before the holdout.

Repeatedly mining many leads/lags without correction creates false discovery.

## W13H-M13 — Health Confound Control
Absence/utilization models control for:
season,
weather,
school calendars,
holidays,
baseline absenteeism,
other pathogens where available.

## W13H-M14 — DIRS Activation Mask
FCC DIRS reports exist only in activated disaster geographies/times.

No-report periods are NOT zeros.

## W13H-M15 — Telecom Cause Accounting
Cell-site outage causes can overlap.

Preserve multi-cause semantics rather than summing cause columns blindly.

## W13H-M16 — Cell-Site-Out != Consumer-Service-Out
FCC explicitly warns that site outages do not map directly to consumer service due to overlapping coverage and mitigation.

Use cell-site metrics as infrastructure state, not direct customer outage counts.

## W13H-M17 — Backup-Power Survival Model
Model hazard of:
backup-powered site -> outage
conditional on grid-restoration time and event severity.

## W13H-M18 — Disaster Daily-Vintage Archive
Archive each FCC daily report immutably.

A later recovery report must not overwrite what was known during peak impairment.

## W13H-M19 — Geographic Exposure Harmonization
Crosswalk:
county
state
sewershed
commuting zone
facility coordinates
market region.

Keep original geography and mapping confidence.

## W13H-M20 — Human-Capacity Intermediate Gate
Before testing returns, require candidate to improve prediction of a real intermediate variable:
claims,
absence,
hospitalization,
production,
throughput,
service outage,
or payroll.
