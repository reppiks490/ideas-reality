# Wave 39F — Fund Fragility & Fire-Sale Transmission

Namespace: **W39F**

Thesis: delayed public fund disclosures can still reveal structural fragility: crowded ownership, redemption sensitivity, derivatives-driven margin risk, repo dependence, securities-lending concentration, and the channels through which one fund's outflow becomes another asset's forced sale. The valid use is as a lag-aware structural prior and stress map, not as a claim about today's exact portfolio.

All candidates are research hypotheses only. Claude owns implementation.

## W39F-E01 — N-PORT Portfolio Crowding Map

Primary source:
SEC Form N-PORT public datasets.

For each security:
aggregate public fund ownership,
number of funds,
ownership concentration,
share of holder AUM,
fund-type mix.

Priority: S

## W39F-E02 — Portfolio Overlap Network

Construct fund-to-fund similarity from common holdings.

Outputs:
overlap graph,
crowding clusters,
asset nodes that connect many funds.

Priority: S

## W39F-E03 — Redemption Pressure by Fund

Form N-PORT reports fund share sales/redemptions for the preceding months.

Build:
net flow proxy =
sales + reinvestment-related sales - redemptions,
normalized by TNA.

Priority: S-

## W39F-E04 — Asset-Level Redemption Transmission

Candidate:
sum across funds of
redemption pressure
× portfolio weight
× expected sale propensity.

Do not assume proportional liquidation.

Priority: S

## W39F-E05 — Fire-Sale Pressure Quotient

FSPQ =
probability-weighted forced sale dollars
/
estimated market absorption capacity.

Use asset-class-specific liquidity:
TRACE for bonds,
ADV/depth for equities,
repo/OTC proxies where appropriate.

Priority: S

## W39F-E06 — Crowded Illiquid Bond Risk

For corporate bonds:
fund ownership concentration
× redemption exposure
× TRACE liquidity weakness.

Target:
future transaction-price pressure / spread widening.

Priority: S

## W39F-E07 — Fund Fragility Breadth

Aggregate number/share of funds simultaneously showing:
large redemptions,
weak returns,
crowded holdings,
high derivatives exposure,
low apparent cash/liquid buffers.

Priority: A+

## W39F-E08 — Flow-Performance Feedback

Research:
poor fund returns
-> redemptions
-> asset sales
-> further price weakness.

Use strictly lagged public vintages.

Priority: S

## W39F-E09 — Redemption Commonality

Measure correlation of fund redemptions within:
strategy,
asset class,
advisor family,
holding-overlap cluster.

High commonality increases synchronized selling risk.

Priority: A+

## W39F-E10 — Holdings Persistence Score

Estimate how persistent each fund's public holdings are across quarters.

Use persistence to determine whether stale public data remain useful as a structural prior.

Priority: S-

## W39F-E11 — Disclosure Staleness Decay

Feature:
expected current-position uncertainty
as a function of
days since public portfolio date,
historical turnover,
fund flows,
market moves,
corporate actions.

Priority: S

## W39F-E12 — Current-Holdings Nowcast

Start from last public N-PORT portfolio.

Propagate with:
known corporate actions,
reported flows where available,
ETF sponsor holdings where contemporaneously public,
market prices,
historical trading behavior.

Output:
distribution, not point estimate.

Priority: A+

## W39F-E13 — Interest-Rate Derivative Exposure

N-PORT publicly disseminated datasets include granular derivatives positions and interest-rate-risk information where public.

Estimate:
fund-level net duration contribution from swaps/futures/options.

Priority: S-

## W39F-E14 — Duration Amplification Ratio

DAR =
portfolio interest-rate sensitivity including derivatives
/
cash-security duration sensitivity.

Research funds using derivatives to amplify rather than hedge rate exposure.

Priority: S

## W39F-E15 — Derivative P&L Stress

N-PORT includes monthly realized/unrealized derivative gains/losses by asset category/instrument.

Feature:
derivative loss
/
TNA
conditioned on current market shock.

Priority: A+

## W39F-E16 — Margin Liquidity Stress Proxy

Estimate variation-margin/collateral need from disclosed derivative positions under standardized shocks.

Compare with:
cash,
Treasuries,
repo access,
other highly liquid public holdings.

Priority: S

## W39F-E17 — Synthetic Leverage State

Construct gross derivative notional / TNA and risk-adjusted exposure where contract terms permit.

Do not use raw notional as economic leverage without payoff normalization.

Priority: A+

## W39F-E18 — Repo Funding Dependence

N-PORT includes repurchase/reverse-repurchase positions and counterparties.

Feature:
repo liability/exposure
× counterparty concentration
× collateral profile.

Priority: S-

## W39F-E19 — Repo Counterparty Commonality

Map many funds relying on the same disclosed repo counterparties.

Question:
does counterparty concentration amplify systemwide liquidity stress?

Priority: A

## W39F-E20 — Securities-Lending Counterparty Concentration

N-PORT includes borrower and securities-lending collateral information.

Build:
borrower concentration,
loaned-security exposure,
non-cash collateral mix.

Priority: A+

## W39F-E21 — Securities-Lending Recall Pressure

Combine:
fund redemptions
× securities on loan
× W33S borrow/short stress.

Hypothesis:
redemptions may force recalls that tighten securities-borrow conditions.

Priority: S-

## W39F-E22 — Cash-Collateral Reinvestment Risk

Map securities-lending cash collateral reinvestment exposures where public.

Research:
maturity/liquidity mismatch
under borrower return + fund redemption stress.

Priority: A

## W39F-E23 — Counterparty Concentration Across Derivatives

Aggregate disclosed derivative counterparties by fund/strategy.

State:
DIVERSIFIED
MODERATELY_CONCENTRATED
HIGHLY_CONCENTRATED.

Priority: A

## W39F-E24 — Fund-to-Dealer Stress Transmission

Fuse W39F counterparty concentration with:
W10B dealer balance-sheet stress,
W38O OTC activity,
repo conditions.

Priority: S-

## W39F-E25 — Asset Liquidation Priority Model

Estimate which positions a fund is likely to sell first under outflow:
cash,
Treasuries,
liquid equities,
corporate bonds,
derivatives,
less-liquid holdings.

Train only on historical portfolio changes following observed redemptions.

Priority: S

## W39F-E26 — Common-Holding Shock Propagation

Graph:
fund A sells asset X
-> X price impact
-> fund B mark-to-market loss
-> B outflows
-> B sells X/Y.

Target:
second-round fire-sale amplification.

Priority: S

## W39F-E27 — Mutual-Fund / ETF Wrapper Divergence

Compare common strategy exposure in:
open-end mutual funds
vs
ETFs.

Question:
do creation/redemption mechanics alter forced-sale timing and severity?

Priority: A+

## W39F-E28 — Fixed-Income Fund Liquidity Mismatch

Estimate:
shareholder redemption horizon
vs
portfolio liquidation horizon.

Use public holdings and asset liquidity; do not infer nonpublic liquidity classifications.

Priority: S

## W39F-E29 — Corporate-Bond Ownership Shock

For each issuer/bond:
fund ownership concentration
× recent public redemptions
× TRACE market depth/liquidity.

Priority: S

## W39F-E30 — Treasury / Rates Fire-Sale Risk

Aggregate rates-sensitive fund duration, derivatives and redemption stress.

Fuse with:
Treasury market depth,
W10B dealer capacity,
W38O rates swaps.

Priority: S-

## W39F-E31 — Cross-Fund Margin Spiral

Shock:
rates/equity/FX/credit
-> derivative loss / margin need
-> liquid-asset sales
-> asset-price move
-> additional margin/redemptions.

Priority: S

## W39F-E32 — Fund Disclosure Reality Gap

Fuse W32R:
last public fund exposure
vs
current market-implied behavior.

Large mismatch can indicate stale holdings, rapid repositioning, or wrong model.

Priority: A

## W39F-E33 — Structural Fragility Prior

Convert lagged N-PORT state into a slow-moving prior over:
fire-sale sensitivity,
crowding,
margin vulnerability,
counterparty concentration.

Fast market/flow signals update this prior rather than replacing it.

Priority: S architecture

## W39F-E34 — Fund Fragility Truth Ladder

PUBLIC FUND DISCLOSURE
-> STRUCTURAL EXPOSURE
-> OBSERVED OUTFLOW/STRESS
-> LIQUIDATION
-> ASSET PRICE IMPACT
-> SECOND-ROUND CONTAGION.

Promotion requires intermediate validation.

Priority: S architecture

## Highest-priority W39F tests

1. W39F-E01 N-PORT Portfolio Crowding Map
2. W39F-E04 Asset-Level Redemption Transmission
3. W39F-E05 Fire-Sale Pressure Quotient
4. W39F-E06 Crowded Illiquid Bond Risk
5. W39F-E11 Disclosure Staleness Decay
6. W39F-E14 Duration Amplification Ratio
7. W39F-E16 Margin Liquidity Stress Proxy
8. W39F-E21 Securities-Lending Recall Pressure
9. W39F-E26 Common-Holding Shock Propagation
10. W39F-E33 Structural Fragility Prior
