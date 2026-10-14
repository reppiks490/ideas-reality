# Wave 83A — Source Notes

Namespace: **W83A**

Status vocabulary: VERIFIED = primary artifact content read this session (2026-10-11); PARTIAL = page read but requested field absent; UNVERIFIED / PROVENANCE_PENDING = not confirmed, must be checked before any dependency.

## W83A-D01 — NCEP Production Status
Primary: https://www.nco.ncep.noaa.gov/pmb/nwprod/prodstat/
Owner: NOAA NCEP Central Operations
Cadence/latency class: 30-day running averages of run start/end; snapshot 2026-10-11
Revision behavior: Live; not an archive
Rights status: Public domain
Verification note: VERIFIED snapshot: GFS 00Z complete 05:13 UTC, HRRR 00Z 01:34; not NOMADS posting time; NBM not listed

## W83A-D02 — HRRR Product Page
Primary: https://www.nco.ncep.noaa.gov/pmb/products/hrrr/
Owner: NOAA NCEP
Cadence/latency class: Hourly cycles; FH18 standard, FH48 at 00/06/12/18Z
Revision behavior: Model upgrades versioned
Rights status: Public domain
Verification note: VERIFIED

## W83A-D03 — ECMWF Open Data
Primary: https://www.ecmwf.int/en/forecasts/datasets/open-data
Owner: ECMWF
Cadence/latency class: 4 cycles/day; 0.25 degree; last 12 runs retained
Revision behavior: IFS at end of dissemination, AIFS as produced
Rights status: CC-BY-4.0 plus ECMWF Terms
Verification note: VERIFIED; member count and exact lag UNVERIFIED

## W83A-D04 — NBM v5.0
Primary: https://vlab.noaa.gov/web/mdl/nbm
Owner: NOAA MDL/NWS
Cadence/latency class: Unknown from page
Revision behavior: Version 5.0 effective 2026-05-05
Rights status: Public
Verification note: PARTIAL: version/date verified; cycles/percentiles UNVERIFIED

## W83A-D05 — MRMS on AWS
Primary: https://registry.opendata.aws/noaa-mrms-pds/
Owner: NOAA NSSL/NCEP via NODD
Cadence/latency class: PUBLIC_REALTIME, 2-minute cycle
Revision behavior: v12 on 2020-10-14 changed products
Rights status: Open with attribution; no implied endorsement
Verification note: VERIFIED; retention not stated

## W83A-D06 — CPC Degree-Day Products
Primary: https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/cdus/degree_days/
Owner: NOAA CPC
Cadence/latency class: Daily, weekly, monthly; schedule not stated
Revision behavior: Archive preliminary; reruns after 2008/2009 corrupted grids
Rights status: Public
Verification note: PARTIAL: normals 1981-2010 and 2010 Census weights verified; schedule UNVERIFIED

## W83A-D07 — CPC ENSO Diagnostic Discussion
Primary: https://www.cpc.ncep.noaa.gov/products/analysis_monitoring/enso_advisory/
Owner: NOAA CPC
Cadence/latency class: UNVERIFIED monthly
Revision behavior: Updates monthly (UNVERIFIED)
Rights status: Public
Verification note: UNVERIFIED: fetched page was legacy (last modified 2016); schedule and ONI definition not confirmed

## W83A-D08 — NSIDC Sea Ice Index G02135
Primary: https://nsidc.org/data/g02135/versions/3
Owner: NSIDC
Cadence/latency class: Daily resolution; coverage 1978-2025 on v3
Revision behavior: v3 retired, v4 current; monthly method updated
Rights status: Public (NSIDC terms)
Verification note: PARTIAL: daily resolution and version notes verified; latency UNVERIFIED

## W83A-D09 — US Drought Monitor
Primary: https://www.drought.gov/data-maps-tools/us-drought-monitor
Owner: NDMC/USDA/NOAA
Cadence/latency class: PUBLIC_SCHEDULED: Thursday release, valid Tuesday 7 a.m. ET
Revision behavior: Weekly new map; expert-authored
Rights status: Public
Verification note: VERIFIED

## W83A-D10 — NOAA HMS
Primary: https://www.ospo.noaa.gov/products/land/hms.html
Owner: NOAA OSPO
Cadence/latency class: Smoke twice daily (11-12 ET, 19-20 ET); fires by ~8 ET
Revision behavior: Format change 2022-07-19
Rights status: Public
Verification note: VERIFIED

## W83A-D11 — Sentinel-2 Products
Primary: https://sentiwiki.copernicus.eu/web/s2-products
Owner: ESA/Copernicus
Cadence/latency class: Latency and revisit not stated on page
Revision behavior: Product baselines versioned (UNVERIFIED)
Rights status: Copernicus open
Verification note: PARTIAL: resolution/bands verified; revisit/NRT UNVERIFIED

## W83A-D12 — USGS Landsat Collections
Primary: https://www.usgs.gov/landsat-missions/landsat-collections
Owner: USGS
Cadence/latency class: Tier latencies UNVERIFIED
Revision behavior: Collection 2 reprocessing
Rights status: Public
Verification note: PARTIAL

## W83A-D13 — GOES-R / STAR GLM Lightning
Primary: https://www.star.nesdis.noaa.gov/goes/index.php
Owner: NOAA NESDIS STAR
Cadence/latency class: UNVERIFIED
Revision behavior: n/a
Rights status: Public
Verification note: PARTIAL: only GLM Flash Extent Density menu entries seen; PROVENANCE_PENDING

## W83A-D14 — USDA NRCS SNOTEL
Primary: https://www.nrcs.usda.gov/resources/data-and-reports/snotel
Owner: USDA NRCS
Cadence/latency class: UNVERIFIED
Revision behavior: Provisional data likely (UNVERIFIED)
Rights status: Public
Verification note: UNVERIFIED: HTTP 503; PROVENANCE_PENDING

## W83A-D15 — NOAA/BOEM MarineCadastre Vessel Traffic
Primary: https://hub.marinecadastre.gov/pages/vesseltraffic
Owner: NOAA/BOEM
Cadence/latency class: PUBLIC_DELAYED (assumed)
Revision behavior: UNVERIFIED
Rights status: Public
Verification note: UNVERIFIED: page text empty; PROVENANCE_PENDING
