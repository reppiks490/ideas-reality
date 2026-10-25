# Wave 83A — Research Methods

Namespace: **W83A**

## W83A-M01 — Arrival Time, Not Cycle Label
Features keyed to first_seen_time of files; production-status averages (e.g. GFS 00Z ~05:13 UTC) only seed embargo.

## W83A-M02 — Complete Own Vintage Archive
Archive every cycle from day 1; ECMWF open data retains 12 runs only.

## W83A-M03 — DST-Safe Clocks
Convert UTC to ET with DST; verify 12Z arrival vs 13:14 EDT / 12:14 EST.

## W83A-M04 — Valid-Time vs Issue-Time Separation
Store issue_time, valid_time, lead; forbid joining on valid_time alone.

## W83A-M05 — Model Version Breaks
Flag NBM v5.0 (2026-05-05), HRRR/GFS upgrades, ECMWF cycle changes; segment fits.

## W83A-M06 — Population-Weight Basis
Document 2010 Census weights in CPC; test alternate weights.

## W83A-M07 — Normals Basis
Document 1981-2010 CPC normals; compare newer normal.

## W83A-M08 — Revision Ledger
Store original and revised degree-day, SWE, drought values.

## W83A-M09 — Release-Clock Event Studies
Weekly USDM Thursday event windows, HMS twice-daily windows, with placebo weekdays.

## W83A-M10 — Staleness Control
USDM valid Tuesday; control for model rainfall in between.

## W83A-M11 — Analyst-Product Subjectivity
Author/analyst effect tests for USDM/HMS.

## W83A-M12 — Cloud Missingness
Do not interpolate satellite indices silently; carry missing flag.

## W83A-M13 — AIS Coverage Adjustment
Normalize vessel counts by receiver coverage and gap rate.

## W83A-M14 — Spoofing and Gap Placebo
Randomize vessel positions/gaps to test false positives.

## W83A-M15 — Spatial Exposure Weights
Use production/capacity weights, fixed ex ante, not tuned on outcomes.

## W83A-M16 — Matched Weather Placebos
Matched-season, matched-weekday windows without model revisions.

## W83A-M17 — Overlap With Scheduled Releases
Separate windows overlapping EIA storage, FOMC, data releases.

## W83A-M18 — Ensemble Calibration
Check ensemble rank histograms and spread-skill before using spread as uncertainty.

## W83A-M19 — Rights and Attribution
NOAA NODD: attribution for unaltered data, no implied endorsement; ECMWF CC-BY-4.0.

## W83A-M20 — Sensor/Collection Harmonization
Harmonize across collection (Landsat C2), product versions (MRMS v11 vs v12 caution).

## W83A-M21 — Intermediate-Outcome Promotion Gate
Source -> physical intermediate (load, solar error, outage) -> expectation revision -> return -> execution; no direct return mining.

## W83A-M22 — Multiple-Testing
Count all lead/cycle/region variants in the family.

## W83A-M23 — Failure-Mode Logging
Log 503/404/empty-page source failures as availability evidence (e.g. SNOTEL, MarineCadastre).
