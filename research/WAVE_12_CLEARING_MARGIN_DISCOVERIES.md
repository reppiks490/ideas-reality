# Wave 12C — Clearing, Margin and Delivery Mechanics

Namespace: W12C

This tranche targets exchange-level leverage cost, clearing risk parameters, delivery mechanics, bank participation, and trading-limit states for NQ and COMEX metals.

All candidates remain hypotheses until falsified and promoted.

## W12C-E01 — Exchange Margin Requirement Shock

Primary sources:
CME Clearing Performance Bond Requirements advisories and CME margin/risk-parameter data.

Status:
PUBLIC notices; current risk-file/tool access varies by product/service.

CME publishes performance-bond changes with a notice date and an effective date. 2026 advisories explicitly include metals and other product groups.

Core feature:
margin_shock =
new_exchange_maintenance_margin / prior_exchange_maintenance_margin - 1

Track separately:
- maintenance
- Non-HRP initial
- HRP initial
- outright vs spread rates
- contract month/risk tier

Priority: S

## W12C-E02 — Margin Burden per Dollar of Notional

Raw margin dollars are not comparable across time as prices change.

Feature:
exchange margin requirement / contract notional.

For NQ:
margin / (NQ price × contract multiplier)

For GC:
margin / (gold price × 100 oz)

Research:
Does a sudden rise in margin burden predict open-interest reduction or liquidity change beyond realized/implied volatility?

Priority: S

## W12C-E03 — Margin Shock × Crowded Open Interest

Fuse:
exchange margin shock
× cleared open interest
× recent OI growth
× realized volatility.

Hypothesis:
raising required capital matters more when leverage/crowding is already high.

Intermediate target:
subsequent OI and volume change.

Priority: S

## W12C-E04 — Margin Relief / Re-Risk State

Margin decreases can release capital.

Feature:
negative margin shock
× depressed OI
× improving volatility/liquidity.

Question:
Does margin relief accelerate position rebuilding after stress?

Priority: A

## W12C-E05 — Volatility Scan-Range Shock

CME performance-bond advisories and risk parameter files can expose volatility-scan changes.

Mechanism:
volScan changes alter option portfolio margin sensitivity even when outright futures margin is unchanged.

Features:
- volScan percentage change
- days/tenor bucket
- product family
- relation to implied-volatility surface

Priority: A+

## W12C-E06 — Short Option Minimum Shock

Some CME advisories explicitly change Short Option Minimum parameters.

Research:
SOM shock
× short-vol crowding proxy
× tail skew
× OI by option region where licensed.

Use:
risk-capital state, not a direct directional signal.

Priority: A

## W12C-E07 — SPAN Price-Scan Risk State

Legacy/current CME risk parameter files encode price-scan ranges and risk arrays; SPAN2 access can require current CME SFTP/software entitlements.

Feature:
scan_range / price
and
change in scan range.

Question:
Can exchange risk calibration provide a cleaner measure of clearinghouse-perceived tail risk than raw realized volatility?

Priority: A+

## W12C-E08 — Inter-Commodity Margin Credit Change

SPAN parameters include inter-commodity offsets/credits.

Research:
changes in offsets between related products alter capital efficiency for hedged portfolios.

Examples:
equity-index family offsets,
metals family offsets,
calendar-spread offsets.

Potential effect:
portfolio rebalancing when a formerly cheap hedge becomes more capital intensive.

Priority: A

## W12C-E09 — Margin Shock × Funding Stress

Fuse:
W12C exchange margin shock
+ W10B repo/dealer funding stress
+ money-market funding state.

Hypothesis:
the same exchange margin increase causes much larger deleveraging when external financing is tight.

Priority: S

## W12C-E10 — Margin Shock × Basis Trade Fragility

For futures/cash convergence trades:
higher initial margin
+ repo stress
+ basis widening
+ elevated leverage prior
can force position reduction.

Targets:
Treasury basis first; analogous logic can condition equity-index futures arbitrage research.

Priority: A+

## W12C-E11 — COMEX Daily Delivery Pressure

Source:
CME Metals Issues and Stops Report.

Status:
DAILY.

Official report fields include:
- exchange/contract
- settlement price
- intent date
- delivery date
- clearing firm/org
- issued quantity
- stopped quantity

For GC:
daily and cumulative issued/stopped contracts.

Priority: S for gold

## W12C-E12 — Delivery Concentration by Clearing Firm

Feature:
Herfindahl/concentration of:
- issuers
- stoppers
- net issue/stop balance
by clearing firm.

Question:
Does concentrated delivery activity add information beyond total delivery volume and inventory?

Caution:
clearing firm != ultimate economic beneficiary.

Priority: A+

## W12C-E13 — Delivery-to-Registered-Stock Pressure

Fuse:
daily/cumulative delivery notices
÷ registered depository stock expressed in contract equivalents.

State:
LOW / NORMAL / ELEVATED / EXTREME delivery pressure.

Do not imply inevitable shortage: warrants can change status and eligible metal can become registered if requirements are met.

Priority: S

## W12C-E14 — Registered / Eligible Inventory Migration

Source:
CME daily depository stock reports.

Official daily fields can include:
previous total,
received,
withdrawn,
net change,
adjustment,
total today,
registered,
eligible,
and for gold a pledged-performance-bond line item.

Features:
- eligible -> registered conversion proxy
- registered withdrawals
- eligible withdrawals
- depository-level concentration
- pledged inventory changes

Priority: S

## W12C-E15 — Physical Tightness Composite for Gold

Fuse:
registered inventory
+ eligible inventory migration
+ delivery pressure
+ futures curve/basis
+ lease/financing proxies where lawful
+ BPR bank positioning.

Goal:
distinguish:
NORMAL
DELIVERY_HEAVY
INVENTORY_TIGHT
BANK_CROWDED
PHYSICAL_STRESS.

Priority: S

## W12C-E16 — CFTC Bank Participation Gold Regime

Source:
CFTC Bank Participation Report.

Status:
MONTHLY.

Official behavior:
- data typically as of first Tuesday of month
- website publication first Friday shortly after 3:30 p.m. ET
- separate futures and gross-options reports
- U.S. bank vs non-U.S. bank aggregate gross long/short
- only markets with enough reportable bank participation are shown

Features:
- bank gross-short share of OI
- bank gross-long share
- net bank positioning
- U.S. vs non-U.S. divergence
- month-over-month acceleration

Priority: A+

## W12C-E17 — Bank Positioning × Delivery Tightness

Hypothesis:
bank-positioning information is more relevant when physical delivery pressure and registered inventory tightness are simultaneously elevated.

Fuse:
BPR
× W12C-E13
× W12C-E14
× gold curve state.

Priority: S-

## W12C-E18 — Bank Options Skew State

BPR options report shows aggregate long/short calls and puts, gross and not delta-adjusted.

Construct:
bank call/put positioning shares separately.

Do not convert gross options counts into delta exposure without strike/maturity detail that the BPR does not provide.

Priority: B+

## W12C-E19 — NQ Distance-to-Hard-Limit State

Source:
CME current daily price-limit/circuit-breaker tables and rule methodology.

For U.S. equity-index futures, overnight hard limits and daytime market-wide limits constrain executable price space.

Feature:
distance_to_active_limit / realized-vol unit.

Use:
execution-risk and tail-state gate.

Priority: S-

## W12C-E20 — Dynamic Circuit Breaker Proximity

CME Dynamic Circuit Breakers use a rolling lookback and configured movement width.

For NQ and related equity-index futures:
estimate exact active DCB boundaries from official rules/reference values where possible.

Output:
NORMAL / NEAR_DCB / DCB_EVENT / POST_DCB_RECOVERY.

Priority: A+

## W12C-E21 — Constrained-Liquidity State

Fuse:
distance to exchange limit
+ depth/spread
+ realized volatility
+ margin burden
+ overnight/session state.

Question:
Does apparent order-book liquidity become non-executable as exchange constraints approach?

Priority: A+

## W12C-E22 — Margin-to-Limit Collision

Rare but important state:
large margin increase
+ high volatility
+ low distance to price limit
+ elevated OI.

Purpose:
identify periods where leverage reduction and restricted price discovery can interact.

Priority: S-

## W12C-E23 — Clearing Constraint State Vector

Fuse:
MARGIN
VOLSCAN
SOM
OI
DELIVERY
REGISTERED_STOCK
BANK_POSITIONING
PRICE_LIMIT_DISTANCE.

Use as a context/regime vector for NQ and gold, not one monolithic directional signal.

Priority: S

## W12C-E24 — Exchange-Risk Lead/Lag Test

Research question:
Does CME clearing risk calibration change before, contemporaneously with, or after observable market risk?

Compare:
margin / scan parameter notice time
vs
realized volatility
implied volatility
OI
liquidity
returns.

This is critical because margin is endogenous to risk.

Priority: S

## Highest-priority W12C tests

1. W12C-E01 Exchange Margin Requirement Shock
2. W12C-E02 Margin Burden per Notional
3. W12C-E03 Margin Shock × Crowded OI
4. W12C-E09 Margin Shock × Funding Stress
5. W12C-E11 COMEX Daily Delivery Pressure
6. W12C-E13 Delivery-to-Registered-Stock Pressure
7. W12C-E14 Registered/Eligible Migration
8. W12C-E15 Gold Physical Tightness Composite
9. W12C-E19 NQ Distance-to-Hard-Limit
10. W12C-E23 Clearing Constraint State Vector
