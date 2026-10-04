# Wave 56G — Global Bullion Geography & Fungibility

Namespace: **W56G**

Thesis: gold is globally priced but not instantly fungible across locations, bar formats, refinery status, vault systems, customs regimes, funding markets and exchange delivery systems. Apparent abundance in one venue can coexist with scarcity elsewhere. The useful state is therefore not “global gold inventory,” but the cost, legal eligibility, time and physical ability to transform metal in one location/form into deliverable metal in another.

This wave complements W49 physical-delivery pressure by modeling the **geographic and metallurgical conversion network** connecting London, New York, Switzerland, Shanghai and other major bullion hubs.

All candidates are research hypotheses only. Claude owns any later implementation.

## W56G-E01 — London Vault Stock State

Primary source:
LBMA London Vault Holdings.

Track monthly:
gold tonnes,
silver tonnes,
month-over-month change.

LBMA data include London commercial vaults and Bank of England gold.

Priority: S

## W56G-E02 — London Vault Depletion Velocity

Feature:
monthly vault stock change
/
starting vault stock.

Priority: S-

## W56G-E03 — London Vault Turnover

Combine:
LBMA clearing volume
/
London vault holdings.

Purpose:
distinguish static stock from active settlement intensity.

Priority: S

## W56G-E04 — London Clearing Acceleration

Primary source:
LBMA Clearing Data.

Track monthly:
gold ounces transferred,
value transferred,
number of transfers,
ounces per transfer.

Priority: A+

## W56G-E05 — Vault-vs-Clearing Reality Gap

State:
vault stocks stable/falling
while clearing turnover accelerates,
or vice versa.

Priority: S

## W56G-E06 — Good Delivery Refinery State

Primary source:
LBMA Good Delivery List.

State:
CURRENT
SUSPENDED
FORMER
REINSTATED
NEWLY_LISTED.

Priority: S

## W56G-E07 — Refinery Accreditation Addition

A newly accredited refinery expands the set of new bars eligible for London Good Delivery.

Estimate added annual refining capacity where public.

Priority: A+

## W56G-E08 — Refinery Suspension Capacity Shock

Suspension prevents new production during the suspension period from being treated as Good Delivery under LBMA rules.

Model refinery production capacity removed from the future Good Delivery supply pool.

Priority: S

## W56G-E09 — Legacy-Bar Eligibility

Bars produced before suspension/transfer can remain Good Delivery, subject to rule-specific exceptions.

Track production date / serial evidence where material.

Priority: S architecture

## W56G-E10 — Sanctions-Driven Bar Eligibility

LBMA rules can treat bars differently when refinery suspension/transfer is tied to responsible-sourcing or trade/economic sanctions.

Fuse W47S sanctions state.

Priority: S-

## W56G-E11 — Good Delivery Production Capacity

Aggregate current-list refiners by:
country,
declared/estimated annual production capacity,
primary vs recycled feedstock where public.

Priority: A

## W56G-E12 — Refinery Geographic Concentration

Measure share of Good Delivery refining capacity by country/region.

Priority: A

## W56G-E13 — Refinery Outage × Accreditation Shock

Fuse physical refinery outage with Good Delivery status.

A refinery can be accredited but physically impaired, or physically operating but not producing eligible Good Delivery bars.

Priority: S

## W56G-E14 — London Bar Format State

LBMA Good Delivery gold bars generally require large-bar specifications near 400 troy ounces.

Maintain exact current specification by rule version.

Priority: S methodology/edge hybrid

## W56G-E15 — COMEX/London Bar Conversion Friction

Compare:
Loco London large-bar inventory
vs
COMEX acceptable bar formats.

Estimate refining/fabrication steps required to convert inventory between venues.

Priority: S

## W56G-E16 — Conversion Capacity Bottleneck

Feature:
bullion needing recast/re-assay
/
available compatible refinery/fabrication capacity.

Priority: S

## W56G-E17 — Conversion Time-to-Deliver

Estimate:
transport
+ refinery queue
+ assay
+ warranting/vault admission
+ customs
time from London-form metal to COMEX-deliverable stock or reverse.

Priority: S

## W56G-E18 — Conversion Cost Spread

Estimate all-in:
freight
insurance
refining/fabrication
assay
vault
financing
customs/tariff
relative to location price spread.

Priority: S

## W56G-E19 — Conversion Arbitrage Feasibility

State:
PRICE_SPREAD_EXISTS
but
NOT_EXECUTABLE
because conversion cost/time/capacity exceeds spread.

Priority: S

## W56G-E20 — New York / London Deliverability Gap

Fuse W49 COMEX registered stock with LBMA vault state.

Feature:
COMEX deliverable scarcity
vs
London available large-bar abundance
adjusted for conversion friction.

Priority: S

## W56G-E21 — Swiss Refining Gateway Flow

Primary source:
Swiss Federal Office for Customs and Border Security.

Track monthly raw/refined gold imports/exports by country.

Priority: S

## W56G-E22 — Swiss Net Refining Flow

Estimate:
imports of raw/large-format/refined feed
vs
exports to consuming/financial centers.

Do not infer exact fabrication transformations without tariff-code support.

Priority: A+

## W56G-E23 — Swiss Country Flow Rotation

Detect changes in export destination share:
UK,
US,
China/Hong Kong,
India,
Middle East,
other.

Priority: S-

## W56G-E24 — Swiss-to-US Bullion Surge

Feature:
Swiss gold exports to US
vs
historical seasonal baseline.

Hypothesis:
can precede/confirm COMEX inventory replenishment under New York scarcity.

Priority: S

## W56G-E25 — Swiss-to-China Bullion Surge

Feature:
Swiss exports toward China/Hong Kong
vs
historical baseline.

Priority: S

## W56G-E26 — Swiss-to-India Bullion Surge

Feature:
Swiss exports to India
conditioned on local premium, festivals/import duty and seasonality.

Priority: A+

## W56G-E27 — SGE Daily Physical Delivery

Primary source:
Shanghai Gold Exchange daily market data.

Track contract-level:
delivery direction,
delivery volume,
trading volume,
open interest.

Priority: S

## W56G-E28 — SGE Delivery/Volume Ratio

Feature:
physical delivery volume
/
trading volume
for applicable contracts.

Priority: S

## W56G-E29 — SGE Delivery Direction Persistence

Track consecutive days of delivery direction imbalance.

Priority: A+

## W56G-E30 — Shanghai Gold Leasing Curve

Primary source:
SGE gold interbank leasing reference rates.

Track:
O/N,
1M,
3M,
6M,
9M,
1Y
curve shape and level.

Priority: S

## W56G-E31 — Chinese Physical Funding Stress

Candidate:
short-dated gold lease rate spike
× SGE delivery demand
× local premium.

Priority: S

## W56G-E32 — Gold Lease Curve Inversion

Detect unusual:
O/N or short-tenor lease rate
relative to longer tenors.

Interpret as potential near-term metal/funding stress only after historical validation.

Priority: A+

## W56G-E33 — SGE Physical Asset-Management Holdings

Primary source:
SGE monthly physical-gold investment statistics for gold asset-management products.

Track:
physical gold held by qualifying products
and monthly change.

Priority: A

## W56G-E34 — Chinese Institutional Physical Demand

Fuse:
SGE asset-management physical holdings
+ gold ETF statistics
+ delivery flow.

Priority: A+

## W56G-E35 — Shanghai/New York Cash-Settlement Link

SGE NYAuTN06/NYAuTN12 use COMEX Asia Marker/calendar-spread references for cash settlement.

Track published SGE reference prices and contract structure.

Priority: S-

## W56G-E36 — Shanghai/New York Basis State

With licensed/live market data:
compare local Shanghai gold pricing to the NYAuTN reference economics, FX and COMEX curve.

Priority: S

## W56G-E37 — SGE Margin Regime Shock

Primary source:
SGE exchange notices.

Track changes to:
margin ratio,
price limits,
holiday risk-control settings.

Priority: S

## W56G-E38 — Margin-Induced Position Compression

Research whether sharp SGE margin increases reduce:
open interest,
leveraged T+D participation,
local premium,
delivery demand.

Priority: S-

## W56G-E39 — Chinese Holiday Closure Gap

SGE holiday closures can leave global gold moving while local market is shut.

Feature:
international price move accumulated during closure
× local inventory/funding state.

Priority: A+

## W56G-E40 — Reopen Gap Absorption

Measure SGE opening/repricing after multi-day closures.

Priority: A

## W56G-E41 — Global Gold ETF Physical Demand

Primary source:
issuer holdings / World Gold Council aggregation.

Track changes in physically backed ETF gold holdings separately from price-driven AUM changes.

Priority: S-

## W56G-E42 — ETF Creation/Redemption Metal Demand

For funds with reliable daily holdings:
estimate ounces added/removed
× authorized-participant settlement mechanics.

Priority: S

## W56G-E43 — ETF Holdings vs Exchange Stock Migration

Compare:
ETF metal inflow/outflow
with
COMEX/London inventory changes.

Research whether ETF redemptions release metal into wholesale delivery networks.

Priority: A+

## W56G-E44 — ETF Regional Flow Divergence

State:
North America inflow
vs
Asia outflow,
or inverse.

Priority: A

## W56G-E45 — Physical-vs-Investment Demand Gap

Compare:
SGE physical delivery / Swiss exports
vs
ETF holdings changes.

Priority: S

## W56G-E46 — London-vs-China Funding Gap

Compare:
SGE lease curve
vs
London physical/vault stress proxies.

A China-specific funding squeeze need not imply London scarcity.

Priority: S

## W56G-E47 — London-vs-New York Inventory Divergence

State:
LBMA vault accumulation
while COMEX registered stocks fall,
or inverse.

Priority: S

## W56G-E48 — New York Replenishment Pipeline

Model:
Swiss/UK export signal
-> US customs arrival
-> approved-vault receipt
-> eligible stock
-> registered stock.

Priority: S

## W56G-E49 — China Replenishment Pipeline

Model:
Swiss/other exports
-> Chinese import arrival
-> SGE/other physical availability
-> delivery/lease response.

Priority: A+

## W56G-E50 — Geographic Bullion Velocity

Estimate movement rate between:
London,
Switzerland,
New York,
Shanghai,
India,
Middle East.

Priority: A

## W56G-E51 — Geographic Scarcity Tensor

Dimensions:
location,
bar form,
legal eligibility,
vault status,
financing cost,
conversion time,
physical delivery pressure.

Priority: S architecture

## W56G-E52 — Metal Fungibility Score

For metal at location A:
probability it can become acceptable deliverable inventory at location B within horizon H.

Priority: S

## W56G-E53 — Effective Global Deliverable Gold

Sum location-specific stocks weighted by:
legal eligibility,
format compatibility,
conversion capacity,
shipping time,
financing,
customs constraints.

Priority: S

## W56G-E54 — Bullion Migration Surprise

Feature:
actual cross-border movement
-
movement expected from contemporaneous price/location spreads.

Priority: S

## W56G-E55 — Refinery Status × Migration

Test whether Good Delivery suspensions/list additions redirect Swiss/Asian refining and bullion flows.

Priority: A+

## W56G-E56 — Bullion Stress Propagation Graph

LOCATION SCARCITY
-> LEASE/PREMIUM
-> REFINERY/CONVERSION DEMAND
-> CROSS-BORDER FLOW
-> EXCHANGE INVENTORY
-> BASIS/FUTURES
-> GLOBAL PRICE.

Priority: S

## W56G-E57 — Physical Gold Reality Gap

Compare:
gold price narrative
vs
physical delivery,
lease rate,
warehouse/vault,
ETF,
customs migration.

Priority: S

## W56G-E58 — Gold Fungibility Truth Ladder

GOLD EXISTS
-> ACCEPTABLE BAR
-> LEGALLY ELIGIBLE
-> RIGHT LOCATION
-> FINANCEABLE
-> CONVERTIBLE
-> VAULTED/WARRANTED
-> DELIVERABLE
-> MARKET PRICE.

Priority: S architecture

## Highest-priority W56G tests

1. W56G-E03 London Vault Turnover
2. W56G-E08 Refinery Suspension Capacity Shock
3. W56G-E15 COMEX/London Bar Conversion Friction
4. W56G-E20 New York / London Deliverability Gap
5. W56G-E24 Swiss-to-US Bullion Surge
6. W56G-E27 SGE Daily Physical Delivery
7. W56G-E30 Shanghai Gold Leasing Curve
8. W56G-E45 Physical-vs-Investment Demand Gap
9. W56G-E52 Metal Fungibility Score
10. W56G-E53 Effective Global Deliverable Gold
