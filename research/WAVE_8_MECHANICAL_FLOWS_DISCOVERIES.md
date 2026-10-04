# Wave 8M — Mechanical Flow and Pre-Trade Intent Discoveries

Namespace: W8M

This tranche targets public data that represents an intention to transact, a mechanical cash transfer, a physical cash-market price, a grid scarcity mechanism, or a reported OTC derivatives transaction.

All candidates are hypotheses until independently falsified and promoted.

## W8M-E01 — Form 144 Proposed-Sale Supply Pressure

Primary source:
SEC EDGAR electronic Form 144.

Status:
LIVE public filing.

Form 144 is a Notice of Proposed Sale of Securities. Electronic filing for covered issuers became mandatory in 2023, and the SEC disseminates accepted filings publicly the same business day.

Structured information can include:
- seller/filer and issuer CIK
- seller relationship to issuer
- security class
- shares/units proposed for sale
- aggregate market value
- shares outstanding
- approximate sale date
- expected broker or market maker
- exchange
- acquisition history
- sales in the prior three months
- Rule 10b5-1 plan adoption date where applicable

Core pressure measures:
- proposed shares / float
- proposed shares / trailing ADV
- proposed market value / market cap
- estimated liquidation days
- seller stake reduction
- cluster breadth across insiders

Priority: S

## W8M-E02 — Intent-to-Execution Gap

Fuse:
Form 144 proposed sale
-> subsequent Form 4 / other evidence of actual execution.

Outcomes:
FULL_EXECUTION / PARTIAL_EXECUTION / RETENTION / DEFERRED / UNKNOWN.

Research evidence:
recent academic work using the two-stage Form 144-to-Form 4 process reports that insiders sometimes retain some or all proposed shares and that the retention decision contains incremental information relative to treating every filing as a completed sale.

Candidate:
execution_gap =
proposed_quantity - matched_actual_quantity

Question:
Does execution/retention state predict returns or fundamentals after controlling for routine insider behavior, liquidity and 10b5-1 plans?

Priority: S

## W8M-E03 — Affiliate Supply Wave

Mechanism:
One proposed sale may be immaterial; clustered proposed sales across multiple officers/directors/large holders can create a more meaningful potential float injection.

Features:
- unique sellers
- aggregate proposed shares / ADV
- aggregate proposed shares / float
- same-week concentration
- role-weighted seller breadth
- prior-three-month actual sales
- issuer repurchase offset

Priority: A+

## W8M-E04 — Planned vs Discretionary Proposed Sale

Form 144 can report Rule 10b5-1 plan adoption date.

Research state:
PREPLANNED / NON_10B5_1 / AMBIGUOUS.

Question:
Does unexpected discretionary proposed-sale pressure contain more information than old-plan mechanical sales?

Controls:
plan age, historical cadence, compensation vesting, tax sales and prior patterns.

Priority: A+

## W8M-E05 — Proposed-Sale Liquidity Absorption

Combine:
proposed sale size
× current displayed/depth liquidity
× realized volume
× spread
× volatility
× issuer buybacks/issuance.

Output:
expected days/market impact required to absorb potential supply.

Do not assume every proposed share executes.

Priority: A

## W8M-E06 — Daily Treasury Cash Impulse

Primary source:
U.S. Treasury FiscalData Daily Treasury Statement (DTS).

Status:
DAILY official API.

DTS reports Treasury operating cash, deposits, withdrawals, public-debt cash issues/redemptions, tax-related flows and refunds.

Mechanism:
Treasury cash flows move balances between the Treasury General Account and the private banking system/Fed reserves.

Candidate:
daily_cash_impulse =
non-debt Treasury withdrawals
-
non-debt Treasury deposits

Then decompose debt settlement separately.

Priority: S

## W8M-E07 — Fiscal Payment Surprise

For each detailed DTS withdrawal category:
actual daily payment
-
expected payment from calendar, weekday, month, benefit schedule and historical seasonality.

Potential categories:
benefit payments, defense/federal programs, tax refunds and other large recurring flows.

Use:
macro liquidity and sector-specific nowcasting only where the category economically maps to the target.

Priority: A+

## W8M-E08 — TGA × Debt Settlement Collision

Fuse:
DTS
+ Treasury auction/settlement calendar
+ W4F Treasury buybacks
+ Fed repo/RRP/SOMA operations.

Mechanism:
Debt issuance/redemption and Treasury spending/tax flows can have opposite reserve effects on the same day.

Research:
estimate net reserve/cash pressure rather than treating TGA change as a standalone direction signal.

Priority: S

## W8M-E09 — Federal Outlay Sector Pulse

Use DTS detailed withdrawal categories to build sector-relevant payment pulses when the mapping is economically defensible.

Examples:
construction/infrastructure, defense, healthcare, transfers.

Hard rule:
A Treasury payment category is not automatically public-company revenue. Prove the intermediate economic exposure.

Priority: B+

## W8M-E10 — Tax Refund / Benefit Liquidity Pulse

DTS includes tax refunds and recurring government transfer payments.

Research:
Does abnormal household cash injection first show up in:
payments/spending proxies
-> consumer sectors
-> macro data?

Use daily public availability, not the underlying benefit entitlement date.

Priority: A-

## W8M-E11 — USDA Cash-Futures Basis Mesh

Primary source:
USDA AMS MyMarketNews API.

Status:
PUBLIC API; source/report-specific cadence.

MyMarketNews exposes raw data published in official Market News reports across physical agricultural markets.

Build regional spot/cash observations by:
commodity
× grade/quality
× location
× delivery terms
× report.

Candidate:
cash price - matched futures-implied price

Research basis dispersion and convergence rather than generic spot momentum.

Priority: S-

## W8M-E12 — Physical Price Dispersion / Shortage State

Across comparable USDA cash markets:
- cross-region price dispersion
- abnormal premium clusters
- missing/zero-volume markets
- volume migration
- convergence failure

Hypothesis:
physical scarcity appears first as geographically uneven cash premiums before aggregate futures fully adapt.

Priority: A+

## W8M-E13 — Cash-Market Pass-Through Graph

Track:
producer/auction cash
-> wholesale
-> processor
-> downstream retail/food inputs
where official reporting supports the chain.

Goal:
estimate propagation lag and margin pressure, not merely correlation.

Priority: A

## W8M-E14 — PJM Five-Minute Load Residual

Source:
PJM Data Miner 2.

Status:
NEAR-LIVE; system-to-system API access requires a PJM account.

PJM instantaneous zonal/area load can update every five minutes.

Feature:
actual five-minute load - weather/time-of-day/day-type expected load.

Use:
regional electricity scarcity and short-horizon gas/power demand state.

Priority: S-

## W8M-E15 — PJM Congestion Topology

Source:
PJM five-minute LMPs, constraints and outages.

Separate LMP into:
energy
+ congestion
+ loss components where source fields allow.

Graph:
constrained transmission element
-> affected nodes/zones
-> load/generation exposure.

Question:
Do new binding-constraint patterns predict short-lived regional price dislocations or generation redispatch?

Priority: A+

## W8M-E16 — Outage-to-Scarcity Conversion

Fuse:
generation outages
+ load residual
+ available imports
+ reserve/ancillary state
+ fuel mix
+ LMP congestion.

An outage matters only to the extent that spare capacity/substitution cannot absorb it.

Priority: S-

## W8M-E17 — ERCOT Reserve Scarcity Field

Sources:
ERCOT real-time SCED and market reports.

Official public data include:
LMPs, settlement-point prices, reserves, ancillary-service clearing prices, ORDC/reliability deployment price adders and other system parameters.

Candidate:
scarcity_pressure =
reserve depletion
× reserve price adder
× load surprise
× outage/renewable shortfall.

Priority: S

## W8M-E18 — ERCOT Renewable Shortfall × Thermal Call

Fuse:
wind/solar forecast
vs actual/updated state
+ load
+ reserves
+ thermal generation requirement.

Hypothesis:
gas/thermal sensitivity rises when renewable shortfall coincides with high load and low reserves.

Priority: S-

## W8M-E19 — ISO/RTO Scarcity Concordance

Construct comparable states across PJM/ERCOT and later other ISO/RTOs:
NORMAL / CONGESTED / RESERVE_STRESS / SCARCITY / RECOVERY.

Question:
Does simultaneous regional scarcity identify national fuel-demand or macro weather shocks distinct from local grid events?

Priority: A

## W8M-E20 — Public SDR Rates-Swap Flow Pulse

Sources:
CFTC Part 43 public swap reporting through registered Swap Data Repositories.

Status:
PUBLIC transaction/pricing dissemination; repository-specific access and terms.

Research dimensions:
- product / UPI
- currency
- tenor
- execution timestamp
- cleared status
- SEF/off-SEF
- price/rate
- reported/capped notional
- transaction/correction state

Candidate:
tenor-bucket trade intensity and price-pressure residual vs Treasury/futures curve.

Priority: S-

## W8M-E21 — Public Credit-Swap Pressure

Use public CFTC/SEC swap/security-based-swap transaction reporting where legally available.

Research:
index CDS / single-name CDS transaction state
vs
cash bond TRACE
vs
equity
vs
options.

Goal:
identify which credit venue currently leads price discovery.

Priority: S-

## W8M-E22 — Commodity Swap Hedge Pressure

Use public commodity swap transaction reports only after product mapping and dissemination-delay controls.

Hypothesis:
abnormal OTC hedge activity can contain information about physical producer/consumer hedging pressure not visible in futures alone.

Critical:
do not infer customer direction unless the public fields and methodology genuinely support it.

Priority: A

## W8M-E23 — OTC-to-Futures Leadership State

Estimate rolling directional influence:
public SDR swaps
<-> futures
<-> cash/reference rates.

Output:
OTC_LEADS / FUTURES_LEADS / SYNCHRONIZED / FRAGMENTED.

Must account for public-reporting delay and capped notionals.

Priority: A+

## W8M-E24 — Mechanical Flow Collision Engine

Fuse scheduled/observed:
Treasury cash flows
+ Treasury issuance/redemption
+ Fed operations
+ rates swap activity
+ futures liquidity.

Purpose:
explain when multiple mechanically different balance-sheet flows reinforce or cancel each other.

Priority: S

## Highest-priority W8M tests

1. W8M-E01 Form 144 Proposed-Sale Supply Pressure
2. W8M-E02 Intent-to-Execution Gap
3. W8M-E06 Daily Treasury Cash Impulse
4. W8M-E08 TGA × Debt Settlement Collision
5. W8M-E11 USDA Cash-Futures Basis Mesh
6. W8M-E15 PJM Congestion Topology
7. W8M-E17 ERCOT Reserve Scarcity Field
8. W8M-E20 Public SDR Rates-Swap Flow Pulse
9. W8M-E21 Public Credit-Swap Pressure
10. W8M-E24 Mechanical Flow Collision Engine
