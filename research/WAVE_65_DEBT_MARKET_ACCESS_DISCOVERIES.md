# Wave 65D — Debt Market Access & Refinancing State

Namespace: **W65D**

Thesis: the important transition between secondary-credit stress and bankruptcy is whether an issuer can actually refinance. SEC debt disclosures, offering/pricing supplements, direct-obligation 8-Ks, debt-retirement events and post-pricing TRACE behavior expose a state machine from maturity pressure to successful or failed market access.

W25C owns secondary credit price discovery. W32I owns equity issuer flow. W51B owns court-controlled restructuring. W65D owns **pre-bankruptcy corporate debt market access and refinancing execution**.

All candidates are research hypotheses only. Claude owns later implementation.

## W65D-E01 — Point-in-Time Debt Maturity Wall
From the latest public 10-K/10-Q debt maturity schedule:
principal due by quarter/year,
secured/unsecured,
fixed/floating,
currency,
instrument.

Priority: S

## W65D-E02 — Near-Term Refinancing Need
Feature:
debt due next 3/6/12/24 months
minus
cash and committed liquidity realistically available.

Priority: S

## W65D-E03 — Revolver Availability State
Track:
committed amount,
drawn amount,
letters of credit,
borrowing-base constraints,
maturity,
covenant limitations.

Priority: S-

## W65D-E04 — Item 2.03 New Debt Event
Primary source:
SEC Form 8-K Item 2.03.

Capture material direct financial obligation:
obligation date,
amount,
maturity,
rate,
security,
guarantees,
payment terms,
acceleration terms.

Priority: S

## W65D-E05 — Material Financing Agreement
Fuse 8-K Item 1.01 / exhibits with Item 2.03.

Extract exact credit/indenture terms rather than headline notional only.

Priority: S

## W65D-E06 — Refinancing Proceeds Allocation
Classify proceeds:
REFINANCE_EXISTING
GENERAL_CORPORATE
CAPEX
M&A
BUYBACK
DIVIDEND
LIQUIDITY
OTHER.

Priority: A+

## W65D-E07 — Debt Extension
Feature:
weighted-average maturity after refinancing
-
weighted-average maturity of retired debt.

Priority: S

## W65D-E08 — Interest-Cost Reset
Feature:
new all-in fixed/floating coupon/spread
-
effective cost of retired debt.

Priority: S

## W65D-E09 — Annual Cash-Interest Delta
Translate refinancing terms into expected annual interest change.

Priority: S-

## W65D-E10 — Secured-Lien Migration
Track refinancing that moves debt:
unsecured -> secured
junior -> senior
or adds guarantees/collateral.

Priority: S-

## W65D-E11 — Covenant Tightening State
Parse:
leverage,
coverage,
minimum liquidity,
borrowing base,
restricted payments,
asset sales,
additional debt.

Priority: A+

## W65D-E12 — Covenant Headroom
Estimate distance from current reported metrics to covenant thresholds.

Use explicit definitions from credit agreement.

Priority: S

## W65D-E13 — Covenant Amendment / Waiver
Track amendment:
temporary waiver,
permanent reset,
pricing step-up,
additional collateral,
new maturity.

Priority: S

## W65D-E14 — Item 2.04 Acceleration Trigger
Primary source:
SEC Form 8-K Item 2.04.

State:
TRIGGER_OCCURRED
CURE_PERIOD
WAIVER_REQUESTED
WAIVER_GRANTED
ACCELERATED
RESOLVED.

Priority: S

## W65D-E15 — Cross-Default Contagion
One default/acceleration can trigger other debt.

Map contractual cross-default/cross-acceleration relationships.

Priority: S

## W65D-E16 — Preliminary Debt Offering State
Primary sources:
SEC preliminary 424B2/424B5 / Rule 433 materials where applicable.

State:
MARKETING
PRICING_PENDING
PRICED
SETTLED
WITHDRAWN/DELAYED.

Priority: S-

## W65D-E17 — Final Debt Pricing State
Extract:
principal,
coupon,
issue price,
maturity,
settlement,
underwriting discount,
call/redemption terms.

Priority: S

## W65D-E18 — New-Issue Spread
Estimate offering spread over contemporaneous Treasury/swap benchmark where terms permit.

Priority: S

## W65D-E19 — New-Issue Concession
Compare offering spread/price to issuer's point-in-time secondary curve from TRACE.

Priority: S

## W65D-E20 — Concession Surprise
Feature:
actual new-issue concession
-
expected concession conditional on issuer rating/liquidity/market regime/deal size.

Priority: A+

## W65D-E21 — Post-Issue Secondary Validation
Use TRACE after settlement to measure:
spread tightening/widening,
turnover,
customer buy/sell pressure,
price support.

Priority: S

## W65D-E22 — Deal Absorption Half-Life
Time for new issue to converge toward the issuer's comparable secondary curve.

Priority: A

## W65D-E23 — Debt Offering Delay / Failure
State:
DEAL_ANNOUNCED
MARKETED
DOWNSIZED
PRICE_WIDENED
POSTPONED
WITHDRAWN.

Only use public evidence; do not infer failed deal from silence alone.

Priority: S

## W65D-E24 — Refinancing Completion Ratio
RCR =
near-term debt retired or contractually refinanced
/
near-term debt requiring refinancing.

Priority: S

## W65D-E25 — Tender / Redemption State
Track issuer debt retirement:
tender offer,
open-market repurchase where disclosed,
optional redemption,
make-whole call,
maturity payment.

Priority: A+

## W65D-E26 — Tender Participation / Residual Maturity
Feature:
principal tendered/accepted
vs
remaining debt still outstanding.

Priority: A

## W65D-E27 — Maturity-Wall Compression
If refinancing raises liquidity but leaves a large cluster of maturities soon afterward, risk may merely shift.

Priority: A+

## W65D-E28 — Market Access Breadth
Across issuers/sectors:
share of attempted deals that price,
average concession,
downsizing/delay breadth.

Priority: S

## W65D-E29 — Credit Window Open/Closed State
Regime:
OPEN_EASY
OPEN_EXPENSIVE
SELECTIVE
DISTRESSED_ONLY
CLOSED_FOR_WEAK_CREDITS.

Priority: S

## W65D-E30 — Refinancing vs Secondary-Credit Gap
Fuse W25C:
secondary bonds may rally before actual financing succeeds, or new financing may reopen despite distressed secondary pricing.

Priority: S

## W65D-E31 — Refinancing vs Equity-Issuance Choice
Fuse W32I:
issuer choosing debt vs equity/convertible can reveal financing constraint and dilution trade-off.

Priority: A+

## W65D-E32 — Refinancing Runway
Estimate:
cash + undrawn committed liquidity + net new debt proceeds
/
forward cash needs and maturities.

Priority: S

## W65D-E33 — Debt Market Access Quotient
DMAQ =
probability-weighted executable refinancing capacity
/
debt requiring refinancing.

Priority: S

## W65D-E34 — Distress Escalation Hazard
Estimate probability:
market access weakens
-> amendment/waiver
-> acceleration/default
-> W51B bankruptcy/restructuring.

Priority: S

## W65D-E35 — Refinancing Recovery State
After stressed issuer successfully refinances:
measure whether TRACE liquidity/spreads, equity, supplier terms and ratings stabilize.

Priority: A+

## W65D-E36 — Debt Access Truth Ladder
MATURITY WALL
-> MARKETED FINANCING
-> PRICING
-> SETTLEMENT
-> DEBT RETIREMENT
-> LIQUIDITY RUNWAY
-> SECONDARY CREDIT VALIDATION
-> COVENANT/DEFAULT STATE
-> RECOVERY OR RESTRUCTURING.

Priority: S architecture

## Highest-priority W65D tests

1. W65D-E02 Near-Term Refinancing Need
2. W65D-E04 Item 2.03 New Debt Event
3. W65D-E12 Covenant Headroom
4. W65D-E14 Item 2.04 Acceleration Trigger
5. W65D-E19 New-Issue Concession
6. W65D-E21 Post-Issue Secondary Validation
7. W65D-E23 Debt Offering Delay / Failure
8. W65D-E24 Refinancing Completion Ratio
9. W65D-E33 Debt Market Access Quotient
10. W65D-E34 Distress Escalation Hazard
