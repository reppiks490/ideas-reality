# Wave 5 Source Notes

## CME Registrar / Physical Storage
Primary documentation:
https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457323380

Registrar metals files describe registered/eligible inventory, receipts, withdrawals and totals. Production licensing/access terms must be reviewed before implementation.

## BSEE Hurricane Activity
Primary:
https://www.bsee.gov/resources-tools/hurricane/hurricane-history

BSEE activates storm monitoring when Gulf offshore operations are threatened and publishes evacuation/production-curtailment updates during active events.

## OFAC Sanctions List Service
Primary:
https://ofac.treasury.gov/
https://home.treasury.gov/policy-issues/financial-sanctions/specially-designated-nationals-and-blocked-persons-list-sdn-human-readable-lists

Machine-readable lists include CSV/XML and enhanced/advanced formats. Preserve every version and hash.

## SEC N-MFP
Primary:
https://www.sec.gov/data-research/sec-markets-data/dera-form-n-mfp-data-sets

Filed monthly by the fifth business day for the preceding month. N-MFP3 includes daily historical subseries, but those values are not public until the filing.

## OCC
Primary:
https://www.theocc.com/market-data/market-data-reports/volume-and-open-interest/daily-volume
https://www.theocc.com/market-data/market-data-reports/other-market-data-info/batch-processing/daily-open-interest

Daily volume and open-interest downloads are available.

## CISA KEV
Primary:
https://www.cisa.gov/known-exploited-vulnerabilities-catalog

Official public JSON/CSV and schema are available. Use only public metadata for financial exposure research; no exploit procedure is required.

## SEC MIDAS / Market Structure
Primary:
https://www.sec.gov/data-research/market-structure-data
https://www.sec.gov/securities-topics/market-structure-analytics/market-activity-data-visualizations

Data include individual-security/exchange-level market-activity measures but are retrospective/delayed. Use for discovery and validation, not pretend-live features.

## CBP CSMS
Primary:
https://www.cbp.gov/trade/automated/cargo-systems-messaging-service

Use timestamped operational guidance and HTS/tariff implementation messages. Archive every message.

## USTR
Primary:
https://ustr.gov/

Official tariff/action notices can contain HTS annexes and exact effective dates. Map legal scope to company/supply-chain exposure.

## NOAA CO-OPS / PORTS
Primary API:
https://api.tidesandcurrents.noaa.gov/api/prod/

Supports water level, currents, wind, visibility and other station observations/predictions. Water levels and currents can be six-minute interval data at supported stations.

## USCG Port Conditions
Primary public sources vary by Captain of the Port/Sector and may be press releases, Marine Safety Information Bulletins, or port-status notices.

Treat as semi-structured. Store exact first-public timestamp and source artifact. Do not infer closure status from news alone when an official notice is available.

## Cloud Status
Google Cloud:
https://status.cloud.google.com/

Azure:
https://azure.status.microsoft/

AWS:
https://health.aws.amazon.com/health/status

Public dashboards have different completeness and retention. Account-specific health APIs are a separate access class and must not be conflated with public data.

## Important availability boundaries

- N-MFP3 daily-looking values are disclosed monthly.
- SEC MIDAS is retrospective/delayed.
- full CAT order lifecycle is regulatory, not public.
- BSEE storm data are event-triggered.
- CME production use/access may require licensing.
- USCG port notices are not guaranteed to be a uniform API.
