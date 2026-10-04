# Wave 6N Source Notes

## W6N-D01 — Taiwan MOPS / TWSE / TPEx
Official company-disclosure and exchange open-data systems.

Use:
monthly operating revenue and point-in-time company disclosures.

Primary:
https://mops.twse.com.tw/
https://openapi.twse.com.tw/

Point-in-time caveat:
whole-market latest-period open-data snapshots may not preserve each company's exact historical disclosure time. Archive company-level publication times.

Rights:
TERMS_REVIEW before production redistribution.

## W6N-D02 — CME COMEX Delivery Notices & Stocks
Official clearing operations page includes COMEX/NYMEX metal delivery notices and stock reports.

Primary:
https://www.cmegroup.com/solutions/clearing/operations-and-deliveries/nymex-delivery-notices.html

Use:
GC/SI/HG delivery and physical inventory research.

Rights:
TERMS_REVIEW / LICENSED depending production use.

## W6N-D03 — CME Metals Issues and Stops
Daily delivery notices identify contract, settlement, intent/delivery dates and clearing firms issuing/stopping.

Primary:
https://www.cmegroup.com/delivery_reports/MetalsIssuesAndStopsReport.pdf

Caution:
clearing firm is not beneficial owner.

## W6N-D04 — SPDR Gold Shares (GLD)
Official trust page and historical resources publish trust/shares information.

GLD explicitly notes that trust ounces shown on the website can differ from the daily bar list because the website is trade-date based while the bar list is settlement-date based.

Primary:
https://www.spdrgoldshares.com/usa/gld/
https://www.spdrgoldshares.com/usa/historical-data/

Archive:
both daily observations and first-seen timestamps.

## W6N-D05 — iShares Gold Trust (IAU)
Official iShares page publishes current ounces in trust and shares outstanding.

Primary:
https://www.ishares.com/us/products/239561/ishares-gold-trust-fund

Archive daily vintages if used for historical flow reconstruction.

## W6N-D06 — FINRA Corporate TRACE
FINRA Trade Activity / Trade History provides transaction information for corporate/agency bonds and other TRACE-eligible products.

Primary:
https://www.finra.org/finra-data/fixed-income/about-trade-activity

FINRA states real-time market trade information includes execution date/time, quantity, price and yield. Exact product/access/usage terms must be reviewed.

## W6N-D07 — USAspending
Official U.S. federal-spending API.

Primary:
https://api.usaspending.gov/
https://github.com/fedspendingtransparency/usaspending-api

Timing:
action_date is an economic/administrative date, not guaranteed first-public availability. Preserve first_seen and source modification metadata.

## W6N-D08 — SAM.gov Opportunities
Official GSA public opportunities API.

Production search:
https://api.sam.gov/opportunities/v2/search

Docs:
https://open.gsa.gov/api/get-opportunities-public-api/

API key required. Opportunity types include pre-solicitation, solicitation, sources-sought, special notice, combined notices and award notices.

Archive versions/amendments; current search can emphasize current active state.

## W6N-D09 — BSEE Hurricane Activity
BSEE publishes Gulf storm evacuation and oil/gas production-curtailment statistics during relevant active events.

Primary:
https://www.bsee.gov/resources-tools/hurricane/hurricane-history

Official documentation says operator reports are collected daily during storm response and public updates are posted in the early afternoon.

Use:
realized physical shut-in and restoration ground truth.

## W6N-D10 — OFAC Sanctions List Service
Structured downloadable SDN/non-SDN files, custom/API capabilities and archived published deltas.

Primary:
https://ofac.treasury.gov/sanctions-list-service

Store:
raw version, hash, first-seen timestamp and structured delta.

## W6N-D11 — BIS Entity List / Consolidated Screening List
Official export-control/restricted-party sources.

Primary:
https://www.bis.gov/

Use:
technology/export-control exposure.

Important:
restriction applicability can extend beyond exact-name list matching. Legal rule interpretation must be rule-grounded rather than inferred by a model.

## W6N-D12 — DoD Contract / Program Releases
Use as corroborating sources for material defense programs and awards.

Primary:
https://www.defense.gov/News/Contracts/

Prefer SAM/USAspending as structured backbone where possible.

## W6N-D13 — Korea Customs preliminary trade statistics
Use with W6N-D01 for semiconductor-cycle research.

Primary:
https://tradedata.go.kr/

Preserve:
first-10-day, first-20-day and final vintages separately; normalize for working days.

## W6N-D14 — SEC EDGAR APIs
Use for U.S. company structured-fundamental confirmation and event controls.

Primary:
https://www.sec.gov/search-filings/edgar-application-programming-interfaces

SEC documentation states submissions metadata update throughout the day in real time; typical processing delays can be under a second for submissions metadata and under a minute for XBRL, but may be longer during peaks.

## W6N-D15 — Federal Register Public Inspection
Use for BIS/export-control and regulatory lifecycle timing before formal publication.

Primary:
https://www.federalregister.gov/reader-aids/developer-resources/rest-api
https://www.federalregister.gov/reader-aids/using-federalregister-gov/understanding-public-inspection

Public-inspection time, formal publication date and effective date are distinct events.

## W6N-D16 — NOAA/NHC forecast vintages
Use for storm prediction before BSEE realization.

Primary:
https://www.nhc.noaa.gov/

Archive every forecast advisory/vintage needed for causal backtests. Never substitute the final storm track.

## Source acceptance contract

Before Claude implements any connector:
1. verify official source and terms,
2. identify event_time,
3. identify first public availability,
4. identify revisions/vintages,
5. identify historical coverage,
6. record timezone,
7. estimate latency distribution,
8. define stable keys,
9. define missing/outage behavior,
10. preserve immutable raw payload and hash.
