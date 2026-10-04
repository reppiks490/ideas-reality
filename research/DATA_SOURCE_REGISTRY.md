# Data Source Registry

The registry is implementation-neutral. "Live" means the source exists now, not that it is necessarily low-latency enough for intraday trading.

| ID | Source | Status | Approx cadence/latency | Candidate use | Primary reference |
|---|---|---|---|---|---|
| D01 | CME Swap Data Repository | LIVE | real-time subject to regulatory delay | OTC risk-transfer flow | https://www.cmegroup.com/market-data/repository/data.html |
| D02 | FINRA Treasury TRACE transaction data | LIVE | public next-day for on-the-run nominal coupons | Treasury flow/counterparty state | https://www.finra.org/rules-guidance/notices/24-06 |
| D03 | FINRA Treasury daily aggregate statistics | LIVE | prior-day data, published business days | ATS/interdealer/customer Treasury state | https://www.finra.org/finra-data/browse-catalog/about-treasury/daily-file |
| D04 | FINRA SLATE securities lending | WATCH | launch currently extended to 2028-09-28 | future borrow/short stress | https://www.finra.org/filing-reporting/slate |
| D05 | US Treasury Daily Treasury Statement | LIVE | by about 4 PM following business day | fiscal liquidity/TGA/tax/customs | https://fiscaldata.treasury.gov/datasets/daily-treasury-statement/operating-cash-balance |
| D06 | New York Fed Primary Dealer Statistics | LIVE | weekly, prior week | dealer positions/funding/fails | https://www.newyorkfed.org/markets/counterparties/primary-dealers-statistics |
| D07 | DTCC FICC Sponsored Membership Volume | LIVE | check publication timing | cleared repo capacity | https://www.dtcc.com/charts/membership |
| D08 | ICI Money Market Fund Assets | LIVE | weekly | cash reservoir/liquidity | https://www.ici.org/weekly-money-market-mutual-fund-assets |
| D09 | SEC EDGAR submissions/XBRL APIs | LIVE | submissions typically <1 sec; XBRL typically <1 min after dissemination | filings/event graph | https://www.sec.gov/search-filings/edgar-application-programming-interfaces |
| D10 | SEC Form N-PORT datasets | LIVE | quarterly public dissemination | fund crowding/derivatives/risk | https://www.sec.gov/dera/data/form-n-port-data-sets |
| D11 | Port of Los Angeles Signal/Control Tower | LIVE | forward view; updated frequently/weekday depending product | forward imports/cargo | https://tower.portoptimizer.com/ |
| D12 | Port of Los Angeles Cargo Operations Dashboard | LIVE | weekday updates | vessels/import volumes | https://www.portoflosangeles.org/business/statistics/cargo-update |
| D13 | USACE Lock Performance Monitoring System | LIVE | lock queues/status about every 15 min; river view about 30 min | barge/logistics constraints | https://ndc.ops.usace.army.mil/ords/f?p=108 |
| D14 | USGS Water Data APIs | LIVE | near real time | river stage/flow | https://api.waterdata.usgs.gov/ |
| D15 | USDA MyMarketNews MARS API | LIVE | report-dependent | physical cash/basis/volume | https://mymarketnews.ams.usda.gov/mymarketnews-api |
| D16 | EIA grid hourly operating data | LIVE | hourly/subhourly depending feed | load/generation/interchange | https://www.eia.gov/opendata/ |
| D17 | PJM Data Miner API | LIVE | feed-specific | load forecast/outages/grid | https://www.pjm.com/markets-and-operations/etools/data-miner-2 |
| D18 | ERCOT public data APIs/portals | LIVE | feed-specific | Texas power/weather/NG link | https://www.ercot.com/mp/data-products |
| D19 | CAISO OASIS | LIVE | feed-specific | load/renewables/congestion | http://oasis.caiso.com/ |
| D20 | EIA Weekly Petroleum Status Report | LIVE | weekly scheduled | oil/refinery/product demand | https://www.eia.gov/petroleum/supply/weekly/ |
| D21 | NASA Black Marble | LIVE | NRT products within hours; daily and granular products | lights/outages/activity/flaring | https://www.earthdata.nasa.gov/data/projects/black-marble |
| D22 | NASA FIRMS | LIVE | near-real-time fire detections | fire/disaster/industrial shock | https://firms.modaps.eosdis.nasa.gov/ |
| D23 | NOAA/NWS alerts | LIVE | near real time | weather shock | https://www.weather.gov/documentation/services-web-alerts |
| D24 | Cloudflare Radar API | LIVE | 15m/1h possible for some traffic series; outage/anomaly feeds | internet/activity/outages | https://developers.cloudflare.com/radar/ |
| D25 | FEMA OpenFEMA disaster declarations | LIVE | some datasets state ~20 min refresh | official disaster confirmation | https://www.fema.gov/openfema-data-page/disaster-declarations-summaries-v2 |
| D26 | FAA SWIM/SWIFT | LIVE/ACCESS-CONTROLLED | near real time | aviation network stress | https://www.faa.gov/air_traffic/technology/swim |
| D27 | TSA checkpoint throughput | LIVE | daily | travel demand | https://www.tsa.gov/travel/passenger-volumes |
| D28 | Indeed Hiring Lab Job Postings Index | LIVE | daily observations, refreshed weekly | labor-demand nowcast | https://hiring-lab.github.io/job_postings_tracker/ |
| D29 | AAR weekly rail traffic | LIVE | weekly | industrial/intermodal pulse | https://www.aar.org/railroad-data/ |
| D30 | Korea Customs preliminary trade statistics | LIVE | first 10/20 days and monthly releases | semiconductor/global trade cycle | https://tradedata.go.kr/ |
| D31 | Kalshi market data API | LIVE | market data live; historical endpoints | macro expectation distributions | https://docs.kalshi.com/ |
| D32 | NHTSA recalls API | LIVE | daily dataset frequency | auto/supplier shocks | https://www.nhtsa.gov/nhtsa-datasets-and-apis |
| D33 | openFDA | LIVE | dataset-dependent | pharma/device events | https://open.fda.gov/apis/ |
| D34 | NOAA/SWPC | LIVE | real time | experimental infrastructure stress | https://www.swpc.noaa.gov/ |
| D35 | USGS earthquake feeds | LIVE | near real time | geospatial physical shock | https://earthquake.usgs.gov/earthquakes/feed/ |
| D36 | Copernicus/Sentinel-5P atmospheric data | LIVE | satellite cadence | NO2 industrial activity | https://dataspace.copernicus.eu/ |
| D37 | OFR Short-Term Funding Monitor | LIVE | dataset-dependent | repo/funding state | https://www.financialresearch.gov/short-term-funding-monitor/ |
| D38 | Federal Reserve H.8 | LIVE | weekly | bank credit/deposits/liquidity | https://www.federalreserve.gov/releases/h8/ |
| D39 | AAR/rail commodity groups | LIVE | weekly | sector-specific physical activity | https://www.aar.org/news/ |
| D40 | Port satellite imagery (Sentinel/NASA) | LIVE | satellite revisit dependent | port/container congestion | https://dataspace.copernicus.eu/ |

## Availability notes

### FINRA Treasury
Do not call D02 real-time. FINRA states the free non-professional transaction-level product is next-day. The historical product has uncapped sizes on a delay and professional products may carry fees/usage restrictions.

### FINRA SLATE
Do not build against it as if available. Current FINRA page says launch is September 28, 2028.

### SEC APIs
Store both event time and ingestion time. Reconstruct historical "what was knowable then" using filing acceptance/public dissemination timing.

### Revised macro/alternative series
Indeed and many official series revise history. Preserve vintages/snapshots. Never train on revised history if the live system would only have seen the first release.

### Satellite
Always preserve acquisition time, processing time and availability time separately.

### Port forecasts
Archive every forecast vintage. A backtest built from only the final revised forecast destroys the central research question: whether forecast revisions had value in real time.

## Data-source acceptance checklist

Before Claude implements a connector:
1. Verify official source and terms.
2. Identify event timestamp.
3. Identify publication/availability timestamp.
4. Identify revisions and vintage policy.
5. Determine stable key/schema.
6. Record timezone.
7. Record expected latency distribution, not only average.
8. Determine historical availability.
9. Determine missingness/outage behavior.
10. Build checksum/raw immutable archive.
