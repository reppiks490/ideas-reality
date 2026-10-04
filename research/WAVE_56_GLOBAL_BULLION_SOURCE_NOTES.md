# Wave 56G — Source Notes

Namespace: **W56G**

## W56G-D01 — LBMA London Vault Data
Primary:
https://www.lbma.org.uk/prices-and-data/london-vault-data

Monthly London gold/silver vault holdings include commercial vaults and Bank of England gold.

## W56G-D02 — LBMA Clearing Data
Primary:
https://www.lbma.org.uk/prices-and-data/clearing-data

Monthly clearing statistics represent net gold/silver transfers physically held in London and settled among LPMCL clearing banks.

## W56G-D03 — LBMA Good Delivery Lists
Primary:
https://www.lbma.org.uk/good-delivery/gold-current-list
https://www.lbma.org.uk/good-delivery/gold-former-list

Current/Former lists identify refiners whose bars are eligible under London Good Delivery rules.

## W56G-D04 — LBMA Good Delivery Rules
Primary:
https://www.lbma.org.uk/publications/good-delivery-rules/

Current rules define bar specifications, suspension, former-list treatment and reinstatement.

## W56G-D05 — Good Delivery Suspension Semantics
LBMA guidance states new production during suspension is not Good Delivery; bars produced before suspension/transfer may remain acceptable subject to applicable rule exceptions.

## W56G-D06 — Swiss Gold Trade
Primary:
https://www.bazg.admin.ch/en/swiss-foreign-trade-statistics-gold-silver-and-coins

SwissImpex publishes monthly gold trade by country from 2012; post-2021 subdivisions distinguish mining/refined categories more precisely.

## W56G-D07 — Shanghai Gold Exchange Daily Data
Primary:
https://www.sge.com.cn/sjzx/quotation_daily_new

Daily contract data include prices, volume, open interest and delivery direction/volume.

## W56G-D08 — Shanghai Gold Leasing Reference Rates
Primary:
https://www.sge.com.cn/sjzx/hjzjckll

SGE publishes a downloadable gold interbank leasing reference-rate history across maturities.

## W56G-D09 — SGE Gold Asset-Management Physical Holdings
Primary:
https://www.sge.com.cn/sjzx/hjzgtjsj

Monthly statistics track physical-gold investment by relevant gold asset-management products.

## W56G-D10 — SGE Shanghai/New York Gold Reference
Primary:
SGE Cash Settlement / NYAuTN06 and NYAuTN12 reference-price pages and contract rules.

These contracts use CME-derived Asia Marker/calendar-spread references for cash settlement; data licensing restrictions apply.

## W56G-D11 — SGE Exchange Notices
Primary:
https://www.sge.com.cn/

Use official notices for margin, price-limit, holiday and risk-control changes.

## W56G-D12 — World Gold Council ETF Aggregation
Primary:
https://www.gold.org/goldhub/data/gold-etfs-holdings-and-flows

Weekly/monthly aggregation covers more than 100 physically backed gold ETFs and similar products. Use issuer data where finer daily precision is required.

## W56G-D13 — ETF Issuer Data
Examples:
SPDR Gold Shares and other fund sponsors publish product/holding documents and/or physical holdings.

Respect issuer/licensing terms.

## W56G-D14 — COMEX Physical Inventory
Consume canonical W49P outputs for registered, eligible, delivery notices and effective deliverable stock.

## W56G-D15 — Existing ICARUS Cross-Layers
Fuse:
W49 physical delivery,
W47 sanctions,
W32 Reality Gap,
FX/rates,
gold futures/spot,
transport/customs,
and refinery outage layers.

No duplicate connectors.
