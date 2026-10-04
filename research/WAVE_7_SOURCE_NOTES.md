# Wave 7 Source Notes

## NRC Reactor Status
Official:
https://www.nrc.gov/reading-rm/doc-collections/event-status/reactor-status/index

NRC publishes unit-level daily power percentage. Data are collected in the morning. The rolling raw dataset should be archived prospectively because rolling windows can drop old records.

## Panama Canal Authority
Official:
https://pancanal.com/en/maritime-services/advisory-to-shipping/
https://pancanal.com/en/maritime-services/vessel-eta-and-transit-booking/
https://evtms-rpts.pancanal.com/eng/h2o/index.html

ACP publishes advisories with future effective dates, booking capacity, draft restrictions and rule changes. Water indicators provide observed/projected Gatun Lake data and downloadable CSVs. Operations summaries can include slot utilization and planned lock outages.

## Bureau of Reclamation RISE
Official:
https://data.usbr.gov/rise/api
https://data.usbr.gov/

RISE provides JSON API access to supported time-series datasets and reservoir/water data.

## EIA Refinery
Official:
https://www.eia.gov/petroleum/supply/weekly

Weekly WPSR provides PADD/U.S. refinery inputs, capacity and utilization. These are regional aggregates, not plant-level outage feeds.

## FERC LNG
Official:
https://elibrary.ferc.gov/eLibrary/

Project status/construction reports can be public and timestamped, but frequency varies by docket. Treat as project/capacity state rather than guaranteed live operations.

## Availability cautions

- NRC detailed outage reasons can lag the morning power reading.
- ACP projection/advisory versions must be archived as-of.
- RISE datasets differ in cadence and coverage.
- EIA weekly refinery utilization cannot locate a specific plant outage.
- FERC project-status reports can be biweekly/monthly and should not be misrepresented as real-time terminal telemetry.
