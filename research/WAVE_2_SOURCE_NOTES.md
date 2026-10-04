# Wave 2 — Source Notes and Availability Audit

Namespace: **W2**

## W2-D01 — FINRA Daily Short Sale Volume
Primary:
https://www.finra.org/finra-data/browse-catalog/short-sale-volume-data/daily-short-sale-volume-files

PUBLIC_SCHEDULED. Use FINRA's current publication calendar/statement for same-day file availability. Scope is FINRA-reported venues, not total-market shorting.

## W2-D02 — FINRA Short Interest
Primary:
https://www.finra.org/filing-reporting/regulatory-filing-systems/short-interest

PUBLIC_SCHEDULED twice-monthly under FINRA's settlement/reporting/publication calendar.

## W2-D03 — SEC Fails-to-Deliver
Primary:
https://www.sec.gov/data-research/sec-markets-data/fails-deliver-data

PUBLIC_DELAYED. FTD is aggregate outstanding fails on settlement date, not a daily short-sale flow.

## W2-D04 — Reg SHO Threshold Securities
Primary:
https://www.nasdaqtrader.com/Trader.aspx?id=RegSHOThreshold
https://www.nyse.com/regulation/threshold-securities

PUBLIC_SCHEDULED/event-state. Preserve exchange scope and file timestamp.

## W2-D05 — Federal Register Public Inspection
Primary:
https://www.federalregister.gov/reader-aids/developer-resources/rest-api
https://www.federalregister.gov/reader-aids/using-federalregister-gov/understanding-public-inspection

PUBLIC_SCHEDULED/EVENT_DRIVEN. Event time is first lawful public-inspection availability, not later Federal Register publication.

## W2-D06 — Census Business Formation Statistics
Primary:
https://www.census.gov/econ/bfs/data.html
https://www.census.gov/econ/bfs/data/weekly.html

Use release-time vintages; weekly estimates may be included within monthly publication structure under current methodology.

## W2-D07 — Opportunity Insights Economic Tracker
Primary:
https://github.com/OpportunityInsights/EconomicTracker

PUBLIC_BATCH/RESEARCH_DATA. Preserve dataset vintage/methodology; do not assume source components are unrevised.

## W2-D08 — FINRA OTC/ATS Transparency Data
Primary:
https://www.finra.org/finra-data/browse-catalog/otc-transparency-data

PUBLIC_DELAYED/PERIODIC; apply product-specific delay and aggregation rules.

## W2-D09 — Source timing rule

For every W2 source, published_time must come from the source's current file/API/public-inspection timestamp. Reporting deadlines do not substitute for public availability.
