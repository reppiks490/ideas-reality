# Wave 3 Source Notes

## CME cryptocurrency data
CME provides official daily/weekly/monthly volume and open-interest reporting, cryptocurrency daily bulletins, settlements and product-specific liquidity reports. Preliminary daily OI may differ from final bulletin data, so archive both status and revision.

Primary:
https://www.cmegroup.com/market-data/volume-open-interest.html

## iShares IBIT
The issuer product page publishes shares outstanding and holdings information; filings provide additional audited/periodic context.

Research requirement:
Archive the page/holding vintage daily if using it to infer primary-market activity. Do not reconstruct past daily holdings from today's page.

Primary:
https://www.ishares.com/us/products/333011/

## NRC reactor status
NRC publishes daily power-reactor status data with power percentage, down date/reason and change flags. NRC states status data are collected between roughly 4 AM and 8 AM Eastern each day.

Primary:
https://www.nrc.gov/reading-rm/doc-collections/event-status/reactor-status/index

## FERC eLibrary
FERC eLibrary entries expose document filed/posted times and gas-infrastructure docket metadata.

Use:
regulatory/project-event research.

Do not infer actual pipeline flow solely from a FERC document.

Primary:
https://elibrary.ferc.gov/

## USPTO / PatentsView
PatentsView is migrating to the USPTO Open Data Portal in 2026. Bulk downloads are available; legacy search/API functions may be interrupted during migration. Some ODP APIs require account/MFA/API key.

Use:
pre-grant/grant/assignee research with explicit publication-date semantics.

Primary:
https://data.uspto.gov/
https://www.uspto.gov/ip-policy/economic-research/patentsview

## USDA Weekly Export Sales
The FAS weekly Export Sales report covers major agricultural commodities and provides outstanding sales, weekly sales/exports and cumulative information.

Use:
commitment and shipment pace.

Primary:
https://fas.usda.gov/data/weekly-export-sales

## On-chain data
Prefer direct public-chain events over vendor-derived labels.

Store:
chain id
block height
block hash
transaction hash
log index
contract
event
block timestamp
observed timestamp
finality timestamp

Do not label exchange wallets retroactively in a historical backtest unless point-in-time label vintages are available.

## Pipeline operational data
Many interstate pipelines maintain public informational/electronic bulletin boards under regulatory requirements, but access methods and terms vary.

Before implementation:
inventory operator-by-operator access, authentication, robots/terms, archive depth, timestamps and schema.

Classify as TERMS_REVIEW_REQUIRED until verified for each target pipeline.
