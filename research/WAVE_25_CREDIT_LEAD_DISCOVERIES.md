# Wave 25C — Credit Lead & Distress Transmission

Namespace: **W25C**

Thesis: a firm's credit instruments can reveal changes in default risk, liquidity demand and balance-sheet stress through actual OTC transactions before or differently from its equity. The research target is not "bonds always lead stocks"; it is to identify the states in which credit-market information has incremental, causally timed value.

All candidates are research hypotheses only. Claude owns implementation.

## W25C-E01 — TRACE Issuer Credit Shock

Primary source:
FINRA TRACE / Bond Trade Dissemination Service (BTDS).

Build an issuer-level abnormal credit move from:
transaction yield,
price,
matched Treasury/risk-free move,
maturity,
seniority,
coupon,
liquidity,
and same-day market credit factors.

Candidate:
issuer_credit_residual =
observed bond move - expected bond move.

Priority: S

## W25C-E02 — Customer Sell Pressure

BTDS dissemination includes side and contra-party type.

Construct customer-originated sell pressure using dealer-side semantics correctly:
reporting dealer buys from customer -> customer sale.

Features:
customer sell notional/intensity,
trade count,
size distribution,
spread concession,
cross-bond breadth.

Priority: S

## W25C-E03 — Customer Buy Pressure

Construct customer demand separately from sell pressure.

Question:
Does customer buying after a credit shock indicate informed stabilization, slow-moving capital, or merely liquidity provision?

Priority: A+

## W25C-E04 — Interdealer Risk Transfer

BTDS identifies interdealer trades.

Research:
customer flow
-> interdealer redistribution
-> later customer transfer.

Candidate:
interdealer share surge after issuer shock.

Interpretation:
possible dealer inventory/risk-sharing stress rather than direct bullish/bearish signal.

Priority: A+

## W25C-E05 — ATS Credit Liquidity Migration

BTDS supports ATS-related indicators/types.

Feature:
ATS share of issuer/sector credit activity
relative to
normal venue/intermediation state.

Question:
Does trading migrate toward/away from electronic venues during stress?

Priority: A

## W25C-E06 — Same-Issuer Cross-Bond Consensus

For firms with multiple bonds:
measure fraction of issues showing concordant abnormal spread/yield moves.

States:
ISOLATED_ISSUE
MATURITY_SPECIFIC
SENIORITY_SPECIFIC
ISSUER_WIDE
SYSTEMIC_SECTOR.

Priority: S

## W25C-E07 — Credit Curve Kink

Build issuer yield/spread curve by maturity.

Feature:
local residual relative to smooth issuer curve.

Possible causes:
specific maturity refinancing risk,
tender/call,
covenant/security structure,
liquidity.

Priority: A+

## W25C-E08 — Seniority Inversion / Capital-Structure Stress

Compare senior secured, senior unsecured, subordinated and hybrid debt where available.

Research abnormal changes in expected loss ordering.

Hard rule:
contractual structure and guarantees must be mapped correctly.

Priority: S-

## W25C-E09 — Credit-Equity Divergence

Candidate:
bond-implied deterioration
while equity remains comparatively stable,
or vice versa.

Research which divergence direction resolves through:
bond catch-up,
equity catch-up,
or common-factor reversal.

Priority: S

## W25C-E10 — Distress Lead State

Condition credit-equity lead/lag on:
credit quality,
equity volatility,
bond liquidity,
firm leverage,
upcoming refinancing,
earnings/event windows.

Goal:
identify when credit has informational advantage rather than assume universal leadership.

Priority: S

## W25C-E11 — Bond Liquidity Breakdown

Measure:
intertrade duration,
transaction count,
size,
price dispersion,
effective price-impact proxy,
customer/interdealer mix,
staleness.

State:
NORMAL
THIN
ONE_SIDED
DISLOCATED
FROZEN.

Priority: S

## W25C-E12 — Liquidity-vs-Credit Decomposition

A falling bond price can reflect liquidity rather than default risk.

Estimate separate components using:
issuer cross-bond consensus,
sector/index move,
trade size,
customer flow,
dealer/interdealer activity,
maturity/seniority.

Priority: S

## W25C-E13 — Large-Trade Censored Pressure

FINRA dissemination caps displayed size for large trades.

Do not treat 5MM+ or 1MM+ as exact notionals.

Build censored-volume lower bounds and count/intensity measures.

Priority: S methodology/edge hybrid

## W25C-E14 — High-Yield Distress Breadth

Aggregate issuer-level residual stress across HY bonds:
breadth,
depth,
sector concentration,
customer sell intensity,
liquidity deterioration.

Use as a credit-risk regime for equity/index research.

Priority: S-

## W25C-E15 — Investment-Grade Funding Stress Breadth

Construct the same for IG separately.

Question:
Does broad IG liquidity/credit deterioration precede funding/financial-condition tightening relevant to equities?

Priority: A+

## W25C-E16 — Fallen-Angel Precursor State

Rather than use rating downgrade after the fact, estimate transition risk from:
bond residuals,
curve inversion,
cross-bond breadth,
equity distance-to-distress proxies,
maturity wall,
filing fundamentals.

Target:
future rating downgrade / spread regime transition.

Priority: A+

## W25C-E17 — Rating Action as Delayed Validation

SEC-required NRSRO rating-history files are publicly available but can have 12- or 24-month disclosure delays depending on rating type/payment status.

Use them for historical label/validation only, not live triggers.

Priority: Validation only

## W25C-E18 — Refinancing Wall Pressure

Map bond maturities and outstanding amounts.

Candidate:
near-term debt due
/
liquidity/resources
conditioned on:
current credit spread,
market issuance conditions,
cash flow,
revolver availability where public.

Priority: S-

## W25C-E19 — Maturity-Specific Refinance Stress

A firm's short-dated bonds can deteriorate faster than long-dated issues when refinancing risk dominates.

Feature:
front-end issuer spread
-
long-end issuer spread
relative to historical structure.

Priority: A+

## W25C-E20 — New-Issue Concession Reality Gap

For newly issued debt:
compare initial/new-issue pricing to secondary issuer curve and post-issue trading.

Research:
unexpected concession
and
post-pricing repricing.

Use exact issuance/public pricing clocks.

Priority: A

## W25C-E21 — Convertible Credit-Equity Bridge

For issuers with convertibles:
compare convertible transaction behavior,
straight-bond credit,
equity,
and options/short-flow state.

Recent research suggests convertibles can increase integration between a firm's credit and equity markets.

Priority: A+

## W25C-E22 — Convertible Parity Dislocation

Estimate theoretical convertible value from:
straight-bond component
+ equity option component
subject to contract terms.

Research transaction-price residuals.

Do not promote without accurate conversion/call/put terms.

Priority: A

## W25C-E23 — Cross-Market Information Propagation Graph

Nodes:
corporate bonds,
equity,
options,
CDS proxy if legally/licensed available,
issuer filings,
sector credit,
Treasuries.

Output:
time-varying directed propagation probabilities.

Priority: S

## W25C-E24 — Credit Shock × Dealer Capacity

Fuse issuer/sector credit flow with W10B dealer balance-sheet/funding state.

Hypothesis:
identical customer selling has larger price impact when dealer balance-sheet capacity is constrained.

Priority: S

## W25C-E25 — Credit Shock × Equity Liquidity

Fuse bond credit shock with:
equity depth/spread,
options gamma state,
short-pressure state.

Question:
When does a credit signal transmit into equity violently versus remain isolated to debt?

Priority: S

## W25C-E26 — Credit Event Surprise Around Earnings/Filings

Compare bond reaction and equity reaction around:
earnings,
8-K,
10-Q/10-K,
financing,
guidance,
legal/regulatory events.

Feature:
credit response residual after controlling for equity move and common factors.

Priority: A+

## W25C-E27 — Credit Recovery Confirmation

After distress shock:
does bond liquidity/price stabilize before equity?

Build:
CREDIT_RECOVERY_LEADS
EQUITY_RECOVERY_LEADS
SYNCHRONOUS
FALSE_RECOVERY.

Priority: A

## W25C-E28 — Issuer Distress Truth Ladder

Sequence:
transaction-level credit flow
-> issuer cross-bond consensus
-> refinancing/fundamental stress
-> ratings/default label
-> realized financing outcome.

Promotion requires survival through intermediate credit outcomes before equity-return claims.

Priority: S architecture

## Highest-priority W25C tests

1. W25C-E01 TRACE Issuer Credit Shock
2. W25C-E02 Customer Sell Pressure
3. W25C-E06 Same-Issuer Cross-Bond Consensus
4. W25C-E09 Credit-Equity Divergence
5. W25C-E10 Distress Lead State
6. W25C-E11 Bond Liquidity Breakdown
7. W25C-E12 Liquidity-vs-Credit Decomposition
8. W25C-E18 Refinancing Wall Pressure
9. W25C-E24 Credit Shock × Dealer Capacity
10. W25C-E28 Issuer Distress Truth Ladder
