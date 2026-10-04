# Wave 56G — Research Methods

Namespace: **W56G**

## W56G-M01 — Location/Form Ledger
Every gold quantity must carry:
location,
bar form,
fineness,
refiner,
production date where relevant,
vault/warehouse status.

## W56G-M02 — Good Delivery Versioning
Archive LBMA Current/Former/Suspended status changes with effective date.

## W56G-M03 — Legacy-Bar Rule
Pre-suspension bars can remain Good Delivery under LBMA rules, subject to exceptions.

Do not invalidate all historical production when a refiner is suspended.

## W56G-M04 — New Production Gate
Post-suspension production is not automatically acceptable London Good Delivery.

## W56G-M05 — Sanctions Exception
Where transfer/suspension relates to responsible-sourcing or sanctions, use controlling LBMA rule and sanctions state; do not generalize legacy acceptability.

## W56G-M06 — Vault Data Frequency
LBMA vault holdings are monthly stock snapshots, not daily inventory.

## W56G-M07 — Clearing != Gross Trading
LBMA clearing data represent net physical transfers settled among LPMCL clearing banks, not total OTC trading volume.

## W56G-M08 — Trade Data Licensing
LBMA detailed trade data may have licensing/usage restrictions.

Separate public summary from licensed production feed.

## W56G-M09 — Swiss Customs Vintage
Archive monthly Swiss gold import/export data by first public release.

## W56G-M10 — Tariff-Code Semantics
Swiss 7108/subdivision changes alter comparability across 2021 boundary.

## W56G-M11 — Import Origin vs Last Country
Use published Swiss customs definitions for origin/trading partner; do not assume shipment routing equals mine origin.

## W56G-M12 — Refining Transformation Uncertainty
Imports/exports do not prove which specific bars were recast.

Use flow-level inference with uncertainty.

## W56G-M13 — SGE Daily Market Vintage
Store first-public time for SGE daily price/delivery files.

## W56G-M14 — SGE Contract Semantics
Spot, deferred, cash-settled NYAu and other SGE contracts have different delivery/settlement rules.

## W56G-M15 — Delivery Direction Semantics
Validate SGE delivery-direction field per contract before aggregating.

## W56G-M16 — SGE Lease Publication Lag
Lease reference curves may be published after the trading week; use true public availability.

## W56G-M17 — FX Normalization
Shanghai/New York basis must use point-in-time USD/CNY and correct ounce-to-gram conversion.

## W56G-M18 — Licensed CME Data Boundary
SGE NYAu reference pages include proprietary CME-derived data with redistribution restrictions.

Do not scrape/redistribute prohibited values in production.

## W56G-M19 — Holiday Calendar
Explicitly model SGE, LBMA/London, COMEX and Swiss customs/business-day calendars.

## W56G-M20 — ETF Holdings vs AUM
Use physical ounces/tonnes, not dollar AUM, to infer metal creation/redemption.

## W56G-M21 — ETF Bar Ownership Scope
ETF holdings may be allocated in specific vault networks and are not automatically free exchange inventory.

## W56G-M22 — Customs-to-Vault Lag
Cross-border export date and exchange-vault receipt can differ by days/weeks.

Estimate distribution rather than same-day mapping.

## W56G-M23 — Conversion Capacity Evidence
Refinery nameplate capacity is not necessarily spare conversion capacity.

## W56G-M24 — Transport Feasibility
Shipping route, insurance, sanctions, customs and security all constrain location arbitrage.

## W56G-M25 — Arbitrage Endogeneity
Price spreads cause metal migration; migration then closes spreads.

Use lead-lag design, not static correlation.

## W56G-M26 — Cross-Market Timestamp Alignment
Align Beijing, London, Zurich and New York trading/publication timestamps precisely.

## W56G-M27 — Physical Promotion Gate
Before price-alpha tests require OOS improvement in:
delivery demand,
lease-rate stress,
cross-border flow,
vault/warehouse state,
or conversion/warranting.

## W56G-M28 — W49 Integration
Do not duplicate COMEX inventory mechanics; consume W49 registered/eligible/delivery state as an upstream input.

## W56G-M29 — W47 Integration
Consume sanctions/refiner legal restrictions from W47S where applicable.

## W56G-M30 — Gold-Specific Promotion Gate
A gold edge must outperform simpler controls:
DXY,
real yields,
nominal yields,
ETF flows,
CFTC positioning,
COMEX basis,
volatility.
