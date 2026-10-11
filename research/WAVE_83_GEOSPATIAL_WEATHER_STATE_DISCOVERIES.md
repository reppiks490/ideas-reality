# Wave 83A — Satellite, Geospatial, Mobility & Weather-Derived State

Namespace: **W83A**

Thesis: weather, satellite and mobility data are tradeable only through their clocks. Forecast vintages arrive hours after the cycle label, analyst products arrive on fixed schedules with stale valid times, and satellite indices lag with cloud missingness. This wave defines vintage-safe, latency-explicit state for gas, power, ags, refining and AI-load narratives and treats forecast revision, not level, as the information.

Boundary: W3 owns gas balance and weather-surprise tensor (E80); W5 owns NHC cone vintages and PORTS; W7/W7T own chokepoint telemetry, EIA-930 residual methodology and AIS basics; W15X owns thermal anomalies; W18G space weather; W24A generation availability and renewable forecast error; W24M marine operability; W30W water and drought exposure; W34D digital infrastructure; W47/W53/W57/W61 sanctions, vessel detention, LNG commissioning, airspace flow. W83A owns NWP vintage/arrival clocks, ensemble spread, release-clock events and satellite/AIS/mobility method discipline.

All candidates are research hypotheses only. Claude owns later implementation.

## W83A-E01 — GFS Cycle Arrival Clock

Primary source: NCEP Central Operations production status (https://www.nco.ncep.noaa.gov/pmb/nwprod/prodstat/): 30-day running averages, GFS 00Z complete ~05:13, 06Z ~11:10, 12Z ~17:14, 18Z ~23:13 UTC

Mechanism: Model runs are public only when the files are posted, after the production end time. Conversion: 00Z ends ~01:13 ET, 06Z ~07:10 ET, 12Z ~13:14 ET, 18Z ~19:13 ET in daylight time. Using valid cycle time instead of arrival time leaks 3-5 hours.

Features: cycle_end_time (running avg), NOMADS first-seen time, delay vs average, ON-TIME flag

Target: Per-cycle embargo applied to any weather feature

Falsify-if: Observed first-seen time differs from posted production end by under 5 minutes in all cycles (no embargo needed)

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: S-

## W83A-E02 — Run-to-Run Population-Weighted Degree-Day Revision

Primary source: NCEP Central Operations production status (https://www.nco.ncep.noaa.gov/pmb/nwprod/prodstat/) + CPC population weights (2010 Census basis, verified)

Mechanism: Natural gas weather trading reacts to change in expected demand, not level. Revision of 15-day pop-weighted HDD/CDD between successive GFS runs measures the new information. Overlaps W3 E80 (weather surprise tensor) by purpose; increment: per-cycle clock and vintage discipline.

Features: dHDD15 = HDD15(run_k) - HDD15(run_k-1), cumulative over 4 runs, sign by season

Target: NG front-month return in 30 min after cycle arrival (12Z and 00Z mostly)

Falsify-if: Revision has no relation to NG return after controlling storage-report calendar

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: S

## W83A-E03 — ECMWF Open-Data vs GFS Disagreement

Primary source: ECMWF open data (https://www.ecmwf.int/en/forecasts/datasets/open-data) (CC-BY-4.0, 00/06/12/18Z, 0.25 deg, last 12 runs retained; verified)

Mechanism: When the two global models disagree on pop-weighted temperature, forecast uncertainty is high and markets reprice on the arbiter model. Disagreement size is an uncertainty gate; sign is the direction of repricing.

Features: d = HDD_ECMWF - HDD_GFS, |d| z-score, run availability gap

Target: Absolute NG move and subsequent NG vol

Falsify-if: |d| not related to abs NG move

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: A

## W83A-E04 — ECMWF Ensemble Spread as Uncertainty Gate

Primary source: ECMWF open data (https://www.ecmwf.int/en/forecasts/datasets/open-data) (ensemble streams enfo/waef and AIFS pf/cf listed; member count UNVERIFIED)

Mechanism: Ensemble spread of pop-weighted temperature encodes forecast uncertainty; high spread in a winter week predicts larger revisions and vol.

Features: std across members of 10-day HDD, spread percentile by season

Target: Next-day NG realized vol

Falsify-if: Spread has zero explanatory power vs implied vol

Horizon: DAILY

Availability: PUBLIC_NEAR_REALTIME

Priority: A

## W83A-E05 — AIFS-IFS-GFS Model Triad Dispersion

Primary source: ECMWF open data (https://www.ecmwf.int/en/forecasts/datasets/open-data) (AIFS data released as produced, IFS at end of dissemination; verified)

Mechanism: Three model families with different release timing: AIFS arrives earlier than IFS, so AIFS-first dispersion previews later IFS revisions.

Features: AIFS_run - GFS_run at arrival, later IFS - AIFS residual, lead time

Target: Whether early AIFS state predicts later IFS shift

Falsify-if: AIFS does not predict IFS

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: A-

## W83A-E06 — NBM v5.0 Probabilistic Percentile Spread

Primary source: NBM v5.0 (https://vlab.noaa.gov/web/mdl/nbm) (v5.0 effective 2026-05-05, verified; percentiles and cycles UNVERIFIED)

Mechanism: NBM blends models and bias-corrects to station-calibrated probabilistic output; percentile spread is a bias-corrected uncertainty measure. Version break on 2026-05-05 requires vintage segmentation.

Features: P90-P10 spread of Tmax, version flag, bias vs observed

Target: Power-price and load forecast error

Falsify-if: Spread no better than raw model spread

Horizon: DAILY

Availability: PUBLIC_NEAR_REALTIME

Priority: B+

## W83A-E07 — NBM Version-Break Placebo

Primary source: NBM v5.0 (https://vlab.noaa.gov/web/mdl/nbm)

Mechanism: Model upgrades alter bias and variance; a signal fitted pre-5.0 may change post-5.0.

Features: pre/post 2026-05-05 error distribution

Target: Stability of weather features across the break

Falsify-if: No distribution shift (placebo passes)

Horizon: SLOW_PRIOR

Availability: PUBLIC_NEAR_REALTIME

Priority: B

## W83A-E08 — HRRR Extended-Cycle Skill Gap (FH18 vs FH48)

Primary source: HRRR product page (https://www.nco.ncep.noaa.gov/pmb/products/hrrr/) (hourly cycles; extended FH48 only at 00/06/12/18Z; verified)

Mechanism: Only four cycles per day give 48-hour horizons; others stop at 18h. Skill and arrival differ by cycle; design must not assume uniform horizon.

Features: forecast hour coverage, error by lead and cycle

Target: Load-forecast-relevant temperature/cloud error by cycle

Falsify-if: Skill identical across cycles

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: B+

## W83A-E09 — HRRR Sub-Hourly 15-Minute Surface for Convective Timing

Primary source: HRRR product page (https://www.nco.ncep.noaa.gov/pmb/products/hrrr/) (wrfsubhf adds 15/30/45 min fields; verified)

Mechanism: Sub-hourly fields resolve frontal and convective passage timing that hourly data smooth, relevant to load ramps in ERCOT/PJM.

Features: 15-min temp drop, wind shift, cloud change over load zones

Target: Intraday load surprise and spot price spike

Falsify-if: Sub-hourly adds nothing over hourly

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: B

## W83A-E10 — HRRR Arrival Latency by Cycle

Primary source: NCEP Central Operations production status (https://www.nco.ncep.noaa.gov/pmb/nwprod/prodstat/) (HRRR 00Z complete ~01:34, 06Z ~07:36 UTC on the snapshot)

Mechanism: HRRR ends about 1.5 hours after cycle label; features at hour H use cycle H-2 or older.

Features: end-time vs cycle label, NOMADS first-seen

Target: Embargo

Falsify-if: Latency under 10 min after run label

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: A-

## W83A-E11 — 12Z Model Arrival Window vs NG Intraday Volatility

Primary source: NCEP Central Operations production status (https://www.nco.ncep.noaa.gov/pmb/nwprod/prodstat/)

Mechanism: 12Z GFS ends ~13:14 ET (EDT) and 12Z ECMWF follows later; event-time clustering of NG vol around arrival windows tests whether markets trade model releases.

Features: NG 1-min abs return around arrival, ET-converted with DST handling

Target: Vol uplift in arrival window vs same window non-model days

Falsify-if: No uplift

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: A

## W83A-E12 — Weekend Forecast Risk into Monday Gap

Primary source: NCEP Central Operations production status (https://www.nco.ncep.noaa.gov/pmb/nwprod/prodstat/) (Friday 12Z/18Z -> Monday open)

Mechanism: Weekend model runs revise while NG/power markets are shut; gap = Friday close vs Monday open correlates with weekend dHDD.

Features: sum dHDD of Sat-Sun runs, Monday opening gap

Target: Monday gap sign/size

Falsify-if: No relation to weekend revision

Horizon: DAILY

Availability: PUBLIC_NEAR_REALTIME

Priority: A-

## W83A-E13 — Storage-Report Weather Overlap Control

Primary source: Weather vintages + EIA storage report (Thursday timing UNVERIFIED this session; W3 owns storage)

Mechanism: Weather revisions overlapping the storage report confuse attribution; need clean windows for weather-only tests.

Features: calendar overlap flag, minutes between model arrival and storage release

Target: Clean-window weather response

Falsify-if: Response same inside/outside overlap

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B

## W83A-E14 — CPC Preliminary Degree-Day Revision Ledger

Primary source: CPC degree-day products (https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/cdus/degree_days/) (archive labelled preliminary; reruns after corrupted grids in 2008 and 2009, verified)

Mechanism: Degree-day tables are revised or rerun; backtests must use the vintage available then.

Features: version hash per daily file, diff vs final NCDC

Target: Size of revisions and effect on demand-model residuals

Falsify-if: Revisions negligible (placebo passes)

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B+

## W83A-E15 — Stale-Normals Bias (1981-2010 Basis)

Primary source: CPC degree-day products (https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/cdus/degree_days/) (current products use 1981-2010 normals, verified)

Mechanism: Anomalies against outdated normals carry climate-trend bias; deviation vs newer normals is a systematic offset in anomaly features.

Features: HDD anomaly with 1981-2010 vs recent 30y normal, offset trend

Target: Bias in demand-surprise features

Falsify-if: Offset not trending

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B

## W83A-E16 — Population-Weight Drift (2010 Census Basis)

Primary source: CPC degree-day products (https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/cdus/degree_days/) (2010 Census weights, verified)

Mechanism: Sun Belt growth and data-center load shift real exposure away from 2010 weights; stale weights misstate demand sensitivity.

Features: reweighted HDD/CDD vs CPC weights, difference

Target: Demand-model residual

Falsify-if: Reweighting does not reduce residual

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B

## W83A-E17 — MRMS 2-Minute QPE Over Gulf Refining Polygons

Primary source: NOAA MRMS on AWS Open Data (https://registry.opendata.aws/noaa-mrms-pds/) (2-minute cycle, >100 products; verified)

Mechanism: Heavy rain/flood over refinery clusters (Houston, Port Arthur, Lake Charles) disrupts operations hours before outage reports. Overlaps W24M marine operability; increment: fast rain rate rather than port restrictions.

Features: rolling 1h QPE over polygons, threshold exceedances

Target: RB/HO crack and CL spread over next sessions

Falsify-if: Exceedance not related to crack move vs matched dry days

Horizon: INTRADAY

Availability: PUBLIC_REALTIME

Priority: B+

## W83A-E18 — MRMS Hail and Severe Swath Over Data-Center Corridors

Primary source: NOAA MRMS on AWS Open Data (https://registry.opendata.aws/noaa-mrms-pds/)

Mechanism: Severe convection over dense data-center counties (e.g. Northern Virginia) can trigger load loss events; W34D owns provider incident side.

Features: hail size swath overlap with polygon, duration

Target: Grid frequency/price anomalies and cloud incident probability

Falsify-if: No relation vs placebo storms

Horizon: INTRADAY

Availability: PUBLIC_REALTIME

Priority: B

## W83A-E19 — MRMS New-Object Notification Latency

Primary source: NOAA MRMS on AWS Open Data (https://registry.opendata.aws/noaa-mrms-pds/) (SNS topic NewMRMSObject; Lambda/SQS subscribers only; verified)

Mechanism: Push notification reduces polling lag; measure message-to-object-available latency.

Features: SNS timestamp vs object LastModified vs first_seen

Target: Latency table

Falsify-if: Polling equals push

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: B

## W83A-E20 — GOES GLM Flash Extent Density Storm Intensity

Primary source: GOES-R GLM Flash Extent Density product (menu verified at https://www.star.nesdis.noaa.gov/goes/index.php; latency UNVERIFIED => PROVENANCE_PENDING)

Mechanism: Lightning rate surges (lightning jumps) precede severe weather; over refineries/substations flags near-term operational risk.

Features: flash count per 5 min per polygon, jump = z>k

Target: Outage reports and energy price spikes

Falsify-if: Jumps do not precede disruptions

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: B

## W83A-E21 — Lightning-Absence Placebo for Outage Attribution

Primary source: GLM + outage reports

Mechanism: Outages without lightning/precip suggest non-weather cause; subset isolates mechanical failures from weather.

Features: weather-attributable fraction

Target: Cleaner classification of outage signals

Falsify-if: Fractions equal

Horizon: DAILY

Availability: UNKNOWN_MEASURED

Priority: B

## W83A-E22 — ENSO Weekly Niño-3.4 Slow Prior

Primary source: CPC ENSO diagnostic discussion (https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/enso_advisory/: schedule, alert status UNVERIFIED; page fetched was legacy)

Mechanism: ENSO phase conditions winter temperature/precip patterns, agricultural supply and gold/oil narrative; used as slow regime prior only. Extends W7/W18 mentions of ENSO.

Features: Niño-3.4 anomaly, ONI definition (UNVERIFIED), phase persistence

Target: Conditional forecast of seasonal HDD anomaly and ag risk premia

Falsify-if: Phase has no skill vs climatology

Horizon: SLOW_PRIOR

Availability: PUBLIC_SCHEDULED

Priority: B+

## W83A-E23 — ENSO Alert-Status Change Event Study

Primary source: CPC ENSO advisory

Mechanism: Watch/Advisory transitions are discrete announcements; markets may reprice ag and energy seasonal premia.

Features: alert-state transition dates, ag/NG event-window returns

Target: Abnormal return in 2 days

Falsify-if: No effect vs placebo monthly dates

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: B

## W83A-E24 — ENSO × Winter HDD Model Bias

Primary source: GFS/ECMWF winter forecasts + ENSO state

Mechanism: Models may be biased in particular ENSO phases; bias map improves conditional forecast.

Features: bias by phase, lead

Target: Bias-corrected dHDD

Falsify-if: Bias not phase-dependent

Horizon: SLOW_PRIOR

Availability: PUBLIC_NEAR_REALTIME

Priority: B

## W83A-E25 — Autumn Arctic Sea-Ice Anomaly Winter Prior

Primary source: NSIDC Sea Ice Index G02135 (https://nsidc.org/data/g02135/versions/3: v3 retired, v4 exists; daily 1978-2025 listed; verified)

Mechanism: Low autumn Arctic ice is hypothesised to influence winter circulation; evidence contested. Treat as weak slow prior with large null-test burden. Version-handling: use v4 and record version.

Features: September minimum extent anomaly, Oct-Nov growth rate

Target: DJF HDD anomaly sign

Falsify-if: No incremental skill over ENSO and persistence

Horizon: SLOW_PRIOR

Availability: PUBLIC_DELAYED

Priority: B

## W83A-E26 — Sea-Ice Daily Revision and Version Discipline

Primary source: NSIDC G02135

Mechanism: Daily values are weather-noisy and versions change monthly-average methods; vintage the data.

Features: version, daily-vs-monthly gap

Target: Revision magnitude table

Falsify-if: Revisions trivial

Horizon: SLOW_PRIOR

Availability: PUBLIC_DELAYED

Priority: B

## W83A-E27 — SNOTEL Snow Water Equivalent Hydropower Prior

Primary source: USDA NRCS SNOTEL (https://www.nrcs.usda.gov/resources/data-and-reports/snotel; HTTP 503 UNVERIFIED => PROVENANCE_PENDING)

Mechanism: Mountain SWE sets spring runoff and hydro output in Northwest/West, shifting regional power prices and gas burn.

Features: basin SWE percent of median, 1 April state

Target: Spring west power and NG demand residual

Falsify-if: No skill vs reservoir storage

Horizon: SLOW_PRIOR

Availability: PUBLIC_NEAR_REALTIME

Priority: B+

## W83A-E28 — Snow-Cover × Cold Interaction in Load Forecast

Primary source: Snow cover + temperature model

Mechanism: Snow cover amplifies cold via albedo; models underpredict cold under fresh snow in some regimes (UNVERIFIED).

Features: snow-covered fraction × T forecast error

Target: Cold-day error

Falsify-if: No interaction

Horizon: DAILY

Availability: UNKNOWN_MEASURED

Priority: B

## W83A-E29 — USDM Thursday Release Event with Valid-Date Staleness

Primary source: US Drought Monitor (https://www.drought.gov/data-maps-tools/us-drought-monitor) (released Thursday morning, valid Tuesday 7 a.m. ET; verified)

Mechanism: Data is 2 days stale at release; markets already saw rain/forecast; the information is category change by production region. Extends W30W-E12 (drought exposure) with release-clock event study and staleness.

Features: D-category share change, production-weighted for corn/wheat/soy, forecast-implied change from model rainfall since Tuesday

Target: ZC/ZW/ZS return around Thursday release

Falsify-if: Release move absent after controlling for model rainfall

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W83A-E30 — USDM Author-Rotation Subjectivity Noise

Primary source: US Drought Monitor (https://www.drought.gov/data-maps-tools/us-drought-monitor) (weekly authors rotate; verified)

Mechanism: Subjective expert maps introduce author-driven noise; author fixed effect should be tested.

Features: author id, category change size by author

Target: Author fixed-effect share of variance

Falsify-if: No author effect

Horizon: WEEKLY

Availability: PUBLIC_SCHEDULED

Priority: B

## W83A-E31 — Drought Acceleration Class Jump

Primary source: US Drought Monitor (https://www.drought.gov/data-maps-tools/us-drought-monitor)

Mechanism: Two-class jumps in a week signal flash drought; faster than level.

Features: Δ weekly category share ≥2 classes

Target: Ag futures risk premium next month

Falsify-if: No effect

Horizon: WEEKLY

Availability: PUBLIC_SCHEDULED

Priority: B

## W83A-E32 — HMS Smoke Polygon Release Clock

Primary source: NOAA OSPO HMS (https://www.ospo.noaa.gov/products/land/hms.html) (first classification 11:00-12:00 ET, second 19:00-20:00 ET; verified)

Mechanism: Smoke analysis is twice daily from daytime GOES; availability is the analyst release, not the satellite pass. Analyst quality review adds ~1-3 hours (verified).

Features: polygon file mtime, Start/End fields, density

Target: Embargo and daily state

Falsify-if: Release times scatter beyond 1h of stated window

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: A-

## W83A-E33 — Smoke × Solar Resource Forecast Error

Primary source: NOAA OSPO HMS (https://www.ospo.noaa.gov/products/land/hms.html) + CAISO/ERCOT solar actuals (UNVERIFIED sources)

Mechanism: Aerosol reduces irradiance not modelled by many forecasts; smoke density over solar fleets predicts negative solar error and hence higher net-load and gas burn.

Features: density-weighted overlap with solar capacity, forecast error

Target: CAISO/SW gas burn, power price in afternoon

Falsify-if: Smoke overlap not related to solar forecast error

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: A-

## W83A-E34 — HMS Fire Detection FRP Surge

Primary source: NOAA OSPO HMS (https://www.ospo.noaa.gov/products/land/hms.html) (fire points by ~8 AM ET; FRP in MW; -999 missing; verified)

Mechanism: Aggregate FRP in western forest regions measures fire intensity; overlaps W15X thermal anomalies but focuses on wildfire-utility link rather than industrial.

Features: sum FRP, new-point count, missing -999 handling

Target: Utility outage and power-price risk

Falsify-if: FRP not related

Horizon: DAILY

Availability: PUBLIC_NEAR_REALTIME

Priority: B

## W83A-E35 — HMS Format-Break Guard

Primary source: NOAA OSPO HMS (https://www.ospo.noaa.gov/products/land/hms.html) (July 19 2022 format change to light/medium/heavy; verified)

Mechanism: Pre-2022 numeric density codes differ; mixing breaks features.

Features: format version flag

Target: Valid sample start date

Falsify-if: No difference after harmonization

Horizon: SLOW_PRIOR

Availability: RETROSPECTIVE_ONLY

Priority: B

## W83A-E36 — Smoke-Season × Air-Quality Demand Suppression

Primary source: HMS + EIA-930 load residual

Mechanism: Heavy smoke may suppress outdoor activity and raise indoor cooling demand; sign ambiguous.

Features: smoke exposure vs load residual

Target: Regional load residual

Falsify-if: No relation

Horizon: DAILY

Availability: PUBLIC_NEAR_REALTIME

Priority: B

## W83A-E37 — Solar GHI Forecast Revision Between HRRR Cycles

Primary source: HRRR product page (https://www.nco.ncep.noaa.gov/pmb/products/hrrr/)

Mechanism: Cloud timing revisions across consecutive HRRR cycles produce solar output surprises; overlaps W24A-E24 (renewable outage × forecast error) in target, differs by NWP vintage input.

Features: ΔGHI between cycle k and k-1 over fleet

Target: Intraday power price and gas burn

Falsify-if: No link

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: A-

## W83A-E38 — Wind Ramp Detection from NWP Vintage Disagreement

Primary source: HRRR product page (https://www.nco.ncep.noaa.gov/pmb/products/hrrr/) + GFS

Mechanism: Spread between NWP vintages for 80 m wind flags ramp uncertainty.

Features: dispersion of hub-height wind between models, ramp threshold

Target: ERCOT/SPP price spikes in ramp windows

Falsify-if: Disagreement does not flag ramps

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: A-

## W83A-E39 — Evening Net-Load Ramp Compression

Primary source: NWP wind + solar decay

Mechanism: At sunset solar drops as wind may lull; coincident drop compresses supply; check dispatch.

Features: solar ramp down × wind ramp down alignment

Target: Price spike frequency

Falsify-if: No coincident-effect

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: B+

## W83A-E40 — Cold-Front Passage Timing Error

Primary source: HRRR product page (https://www.nco.ncep.noaa.gov/pmb/products/hrrr/)

Mechanism: 1-3 hour timing error for fronts causes load misforecast.

Features: front timing difference between cycles, load error

Target: Real-time price

Falsify-if: No effect

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: B

## W83A-E41 — Heat-Dome Tail Probability: ECMWF Ensemble vs NBM Percentile

Primary source: ECMWF open data (https://www.ecmwf.int/en/forecasts/datasets/open-data) ; NBM v5.0 (https://vlab.noaa.gov/web/mdl/nbm)

Mechanism: Tail probability from member exceedance vs percentile: disagreement sizes heat-wave risk premium for power.

Features: P(Tmax>threshold) from members vs NBM P90

Target: Power forward/next-day spread

Falsify-if: Disagreement not informative

Horizon: DAILY

Availability: PUBLIC_NEAR_REALTIME

Priority: B+

## W83A-E42 — Polar-Vortex Ensemble Spread Gate

Primary source: ECMWF open data (https://www.ecmwf.int/en/forecasts/datasets/open-data)

Mechanism: January bimodal ensemble spread yields tail risk in NG; use as gating of short-vol exposures.

Features: bimodality index of 10-day HDD members

Target: NG vol jump

Falsify-if: No jump

Horizon: DAILY

Availability: PUBLIC_NEAR_REALTIME

Priority: B+

## W83A-E43 — Hurricane Track Ensemble Vintage Divergence

Primary source: ECMWF open data (https://www.ecmwf.int/en/forecasts/datasets/open-data) + GFS ensemble (NHC cone covered in W5)

Mechanism: Ensemble divergence about landfall location sets Gulf production/refining risk premium before NHC cone updates.

Features: track spread at 72h, landfall-area exposure

Target: NG/CL/crack vol

Falsify-if: Spread not predictive vs NHC cone

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: B+

## W83A-E44 — Sentinel-2 Cloud-Mask Missingness Feature

Primary source: Sentinel-2 products (https://sentiwiki.copernicus.eu/web/s2-products) (L2A SCL map, 10/20/60 m folders; verified)

Mechanism: In growing seasons many scenes are cloudy; cloud-covered fraction determines how often crop indices can update. Missingness is a feature and a bias.

Features: SCL cloud fraction, clear-scene count/week

Target: Update-frequency map

Falsify-if: Clear-scene count uniform

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B

## W83A-E45 — Sentinel-2 NDVI Crop-Condition Prior

Primary source: Sentinel-2 products (https://sentiwiki.copernicus.eu/web/s2-products) (bands 4 and 8 at 10 m; verified; revisit and latency UNVERIFIED)

Mechanism: NDVI anomalies at county scale lead USDA condition ratings. Satellite lead must beat USDA weekly crop progress.

Features: NDVI anomaly vs 5-yr, county weighting by acreage

Target: USDA condition rating change and ZC/ZS drift

Falsify-if: No lead vs USDA

Horizon: WEEKLY

Availability: PUBLIC_BATCH

Priority: B+

## W83A-E46 — Landsat Collection 2 Reprocessing Vintage

Primary source: USGS Landsat Collection 2 (https://www.usgs.gov/landsat-missions/landsat-collections; reprocessing statement verified; Real-Time tier details UNVERIFIED)

Mechanism: Collection reprocessing alters pixel values; backtests must use consistent collection and tier.

Features: collection/tier flags, geolocation shift

Target: Stability

Falsify-if: Values unchanged across tiers

Horizon: SLOW_PRIOR

Availability: RETROSPECTIVE_ONLY

Priority: B

## W83A-E47 — MODIS/VIIRS Vegetation Index Composite Lag (UNVERIFIED)

Primary source: NASA MODIS/VIIRS NDVI/EVI composites (primary URL not fetched; PROVENANCE_PENDING)

Mechanism: Composite products average over multi-day windows and lag; useful for slow crop prior only.

Features: composite window, latency

Target: Crop-condition prior

Falsify-if: Lag exceeds crop-report lead

Horizon: SLOW_PRIOR

Availability: PUBLIC_DELAYED

Priority: B

## W83A-E48 — SAR Floating-Roof Tank Shadow Storage Estimate (PROVENANCE_PENDING)

Primary source: Sentinel-1/optical shadow methods (academic/commercial; no primary artifact verified)

Mechanism: Floating roof height inferred from shadow area proxies crude inventory ahead of reports.

Features: tank shadow ratio, tank count, revisit

Target: Cushing/Gulf storage vs EIA weekly

Falsify-if: Error exceeds EIA weekly surprise std

Horizon: WEEKLY

Availability: UNKNOWN_MEASURED

Priority: B

## W83A-E49 — VIIRS Nighttime-Lights Activity Index (UNVERIFIED)

Primary source: NASA/NOAA VIIRS Day/Night Band (not fetched; PROVENANCE_PENDING)

Mechanism: Night-light changes proxy local activity in disrupted regions (war, outages).

Features: radiance change vs baseline, cloud/moon mask

Target: Disruption confirmation

Falsify-if: No signal after mask

Horizon: SLOW_PRIOR

Availability: PUBLIC_DELAYED

Priority: B

## W83A-E50 — Sentinel-5P NO2 Industrial Activity (UNVERIFIED)

Primary source: Copernicus Sentinel-5P TROPOMI NO2 (not fetched; PROVENANCE_PENDING)

Mechanism: NO2 column changes follow industrial/power activity.

Features: NO2 anomaly over industrial clusters

Target: Activity prior

Falsify-if: Anomaly unrelated to production data

Horizon: SLOW_PRIOR

Availability: PUBLIC_DELAYED

Priority: B

## W83A-E51 — AIS Terrestrial-vs-Satellite Coverage Bias Map

Primary source: NOAA/BOEM MarineCadastre vessel traffic (https://hub.marinecadastre.gov/pages/vesseltraffic; page text empty => PROVENANCE_PENDING)

Mechanism: Vessel density from terrestrial AIS undercounts offshore areas; density changes may reflect receiver coverage. Corrects W7T/W24M AIS usage.

Features: message rate per receiver-grid, vessel count per grid, coverage index

Target: Coverage-adjusted density

Falsify-if: Coverage index uncorrelated with density changes

Horizon: SLOW_PRIOR

Availability: PUBLIC_DELAYED

Priority: B+

## W83A-E52 — Chokepoint Tanker Density with Spoofing Placebo

Primary source: AIS (provider-specific; PROVENANCE_PENDING); extends W7T/W53 chokepoint monitoring

Mechanism: Counts of tankers inside bounding polygons for Hormuz/Suez/Malacca measure flows; spoofing and gaps produce false changes, so use confidence-weighted counts.

Features: count with speed/heading filters, gap fraction, position-jump flag

Target: CL/Brent range expansion

Falsify-if: Counts do not lead price after gap control

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: B+

## W83A-E53 — LNG Terminal Anchorage Queue vs Weather

Primary source: AIS + HRRR/MRMS (W57 owns commissioning; W24M owns port conditions)

Mechanism: Queue length at Sabine/Cameron-class terminals responds to weather and outages; NG demand pull changes.

Features: vessels waiting >6h, weather flags

Target: Henry Hub next-day move

Falsify-if: Queue not related

Horizon: DAILY

Availability: UNKNOWN_MEASURED

Priority: B

## W83A-E54 — AIS Gap-Rate as Dark-Fleet Noise Floor

Primary source: AIS (W47 owns sanctions)

Mechanism: Rate of vessels disappearing near sanctioned regions is a measure of evasion intensity, but differs from coverage gaps; baseline subtraction is required.

Features: gap rate minus coverage baseline

Target: Oil discount/spread

Falsify-if: Gap rate = coverage rate

Horizon: WEEKLY

Availability: UNKNOWN_MEASURED

Priority: B

## W83A-E55 — TSA Throughput Mobility Proxy (UNVERIFIED)

Primary source: TSA checkpoint numbers (https://www.tsa.gov/travel/passenger-volumes; not fetched; PROVENANCE_PENDING)

Mechanism: Daily throughput proxies travel demand and jet fuel; W61 covers airspace flow.

Features: 7d vs same-week prior year

Target: Jet fuel/crack, travel stocks

Falsify-if: No relation

Horizon: DAILY

Availability: PUBLIC_DELAYED

Priority: B

## W83A-E56 — DOT Traffic Volume Trends (UNVERIFIED)

Primary source: FHWA Traffic Volume Trends (not fetched; PROVENANCE_PENDING)

Mechanism: Monthly vehicle-miles proxy gasoline demand; lag long, so slow prior.

Features: VMT YoY

Target: RB demand surprise

Falsify-if: Lag exceeds EIA weekly

Horizon: SLOW_PRIOR

Availability: PUBLIC_DELAYED

Priority: B

## W83A-E57 — Port-Webcam Container-Stack Proxy (PROVENANCE_PENDING)

Primary source: Public port webcams (terms and legality unknown)

Mechanism: Computer-vision yard occupancy proxy; terms of use risk and weather noise.

Features: stack height proxy, daylight availability

Target: Container-flow nowcast

Falsify-if: Terms prohibit or proxy uncorrelated with port statistics

Horizon: WEEKLY

Availability: PUBLIC_WEB_ONLY

Priority: B

## W83A-E58 — Data-Center-Dense Balancing Authority Load Residual

Primary source: EIA-930 hourly demand (W7T owns residual methodology) with NWP expected load

Mechanism: Residual growth in data-center-heavy BAs measures AI load buildout visible to NQ-relevant narratives; increment over W7T: BA-specific trend and weather vintage discipline.

Features: load - weather-expected load, 30d slope, vintage of weather forecast

Target: AI-capex narrative vs semiconductor basket

Falsify-if: Residual slope flat or explained by weather

Horizon: SLOW_PRIOR

Availability: PUBLIC_NEAR_REALTIME

Priority: A-

## W83A-E59 — Wet-Bulb Cooling-Load Forecast for Data Centers

Primary source: HRRR product page (https://www.nco.ncep.noaa.gov/pmb/products/hrrr/) + ECMWF

Mechanism: Wet-bulb extremes raise cooling electric demand; W30W-E22 covers the water side.

Features: wet-bulb forecast vs threshold, load sensitivity

Target: Local price spikes

Falsify-if: No effect

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: B

## W83A-E60 — Large-Load Interconnection Queue Growth (PROVENANCE_PENDING)

Primary source: ISO/RTO large-load queue reports (ERCOT, PJM; not fetched)

Mechanism: Queued data-center load shifts capacity prices and equipment demand; slow, lumpy.

Features: queue MW, quarter change

Target: Capacity price and utility equities

Falsify-if: No relation

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B+

## W83A-E61 — Price-Spike Hour × Temperature Ensemble Tail

Primary source: ISO LMP + ensemble

Mechanism: Spike probability is nonlinear in temperature tail; ensemble exceedance prob captures tail.

Features: P(T>k) × reserve margin

Target: Spike hour probability

Falsify-if: No gain over deterministic

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: B+

## W83A-E62 — Eclipse and Special Astronomical Solar Dip Template

Primary source: Solar geometry (computed)

Mechanism: Predictable irradiance drops are known with certainty; event study of solar eclipses validates solar-gas linkage; no eclipse in short window (UNVERIFIED dates).

Features: obscuration fraction

Target: Gas burn response

Falsify-if: Response absent

Horizon: SLOW_PRIOR

Availability: PUBLIC_SCHEDULED

Priority: B

## W83A-E63 — Forecast-Error Memory (Persistence of Model Bias)

Primary source: NCEP Central Operations production status (https://www.nco.ncep.noaa.gov/pmb/nwprod/prodstat/)

Mechanism: Biases persist for days within a regime; the last N errors condition today's trust in the model.

Features: error at lead 1-3 days, AR(1) of error

Target: Revision size

Falsify-if: Errors i.i.d.

Horizon: DAILY

Availability: PUBLIC_NEAR_REALTIME

Priority: B+

## W83A-E64 — Vintage Archive Completeness Audit

Primary source: NOMADS/AWS/ECMWF 12-run retention (verified)

Mechanism: ECMWF open data keeps only the last 12 runs (~2-3 days), so unarchived history is lost; vintage-complete backtests need own archive from day 1.

Features: archived runs/total runs, gap map

Target: Usable backtest window

Falsify-if: Archive complete from third-party

Horizon: SLOW_PRIOR

Availability: RETROSPECTIVE_ONLY

Priority: A

## W83A-E65 — Weather and Geospatial Truth Ladder

Primary source: All W83A sources

Mechanism: Hierarchy of observed, analyst, forecast, satellite and derived layers with vintage enforcement.

Features: rung label, issue/valid/first_seen clocks

Target: Governance object

Falsify-if: A forecast value used before its first_seen_time

Horizon: SLOW_PRIOR

Availability: PUBLIC_NEAR_REALTIME

Priority: S-

## Final architecture edge — Truth Ladder

Truth Ladder for weather/geospatial state:
1. Observed physical measurement (MRMS, station, GLM, SNOTEL) with measurement latency.
2. Official analyst products (USDM, HMS) with release clocks.
3. Forecast vintages (GFS, ECMWF, HRRR, NBM) with arrival clocks and complete archive.
4. Satellite-derived indices (Sentinel, Landsat, MODIS) with composite lags and cloud missingness.
5. Derived market-facing features (dHDD, spread, exposure-weighted indices).
Forecast vintage may only be used from first_seen_time; observed data can only validate forecasts after the valid time; no revised product replaces its original vintage.

## Highest-priority W83A tests

1. W83A-E01 GFS Cycle Arrival Clock
2. W83A-E02 Run-to-Run Population-Weighted Degree-Day Revision
3. W83A-E11 12Z Model Arrival Window vs NG Intraday Volatility
4. W83A-E03 ECMWF Open-Data vs GFS Disagreement
5. W83A-E04 ECMWF Ensemble Spread as Uncertainty Gate
6. W83A-E32 HMS Smoke Polygon Release Clock
7. W83A-E33 Smoke × Solar Resource Forecast Error
8. W83A-E64 Vintage Archive Completeness Audit
9. W83A-E12 Weekend Forecast Risk into Monday Gap
10. W83A-E58 Data-Center-Dense Balancing Authority Load Residual
