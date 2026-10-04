# Wave 32I — Issuer Mechanical Flow

Namespace: **W32I**

Thesis: corporations themselves are large, state-dependent sources of equity demand and supply through repurchases, accelerated share repurchases, tender offers, ATM programs, follow-ons, convertibles and compensation issuance. The research target is *executed or contractually constrained issuer flow* and its absorption by market liquidity—not announcement headlines.

Current-rule warning: the SEC's 2023 Share Repurchase Disclosure Modernization rule was vacated effective December 19, 2023. In 2026, domestic issuers are back to the pre-2023 Item 703 monthly repurchase table in Forms 10-Q/10-K. The vacated issuer-specific Item 408(d) 10b5-1 disclosure is not a mandatory 2026 signal.

All candidates are research hypotheses only. Claude owns later implementation.

## W32I-E01 — Buyback Authorization Capacity
Public authorization dollars/shares remaining.
State:
NONE / ACTIVE / EXPIRING / EXHAUSTED / SUSPENDED / REPLACED.
Priority: A

## W32I-E02 — Authorization Utilization
Actual cumulative repurchases / authorized capacity using point-in-time periodic filings.
Priority: S-

## W32I-E03 — Item 703 Monthly Repurchase Reality
Primary source: 10-Q/10-K Item 703.
Fields:
shares purchased,
average price,
shares under publicly announced programs,
remaining authorization.
Priority: S calibration

## W32I-E04 — Repurchase Velocity Residual
Actual monthly repurchase dollars relative to:
remaining authorization,
free cash flow,
historical cadence,
valuation,
ADTV.
Priority: S-

## W32I-E05 — Authorization Exhaustion Clock
Estimate months/days to exhaustion under current execution cadence, with uncertainty.
Priority: A+

## W32I-E06 — Rule 10b-18 Safe-Harbor Capacity Envelope
Voluntary safe-harbor volume envelope:
up to 25% of prior four-week ADTV on a normal day, subject to rule conditions and block exception.
This is an upper-bound scenario, not proof of buying.
Priority: S methodology/edge hybrid

## W32I-E07 — Safe-Harbor Flow / Liquidity Ratio
Scenario:
permitted 10b-18 volume envelope / expected continuous-market depth and daily volume.
Priority: A+

## W32I-E08 — Intraday Safe-Harbor Timing State
Rule 10b-18 excludes the opening purchase and restricts repurchases near the scheduled close; highly liquid securities use a 10-minute close window and others 30 minutes under current rule criteria.
Priority: A

## W32I-E09 — Block-Purchase Exception State
Model the once-per-week alternative block exception separately from ordinary 25% ADTV activity.
Priority: B+

## W32I-E10 — ASR Initial Delivery Shock
Primary source: issuer 8-K / material agreement.
Capture:
notional,
payment date,
initial share delivery,
initial-delivery percentage,
expected term.
Priority: S

## W32I-E11 — ASR Dealer Acquisition Envelope
Estimate dealer shares still needing to be sourced/hedged through the averaging period.
Do not equate ASR notional with same-day open-market buying.
Priority: S

## W32I-E12 — ASR VWAP-Term Pressure
Model expected remaining acquisition intensity across disclosed or inferred averaging/settlement window.
Priority: S-

## W32I-E13 — ASR Settlement Residual
At final settlement:
additional shares to issuer
vs issuer cash/share obligation to dealer.
Priority: A+

## W32I-E14 — Fixed-Price / Dutch Auction Tender Demand
Tender offers create explicit price/quantity windows distinct from open-market repurchases.
Priority: S-

## W32I-E15 — ATM Issuance Capacity
Primary source: 424B5 / sales agreement.
Authorized unsold ATM dollar/share capacity.
This is capacity only.
Priority: A

## W32I-E16 — ATM Realized Issuance
Actual shares sold and proceeds disclosed in later periodic/current filings.
Priority: S calibration

## W32I-E17 — ATM Issuance Velocity
Actual shares sold / elapsed eligible period, normalized by ADTV/free float.
Priority: S-

## W32I-E18 — Follow-On / Underwritten Equity Supply
Publicly announced primary share count × offer price and settlement date.
Priority: S

## W32I-E19 — Forward Equity Sale State
Track ATM forward-sale agreements and physical settlement obligations separately from immediate primary issuance.
Priority: A+

## W32I-E20 — Convertible Issuance Equity-Hedge State
Convertible offerings can induce dealer hedge activity; issuer capped-call transactions can offset some exposure.
Estimate directional flow only from disclosed terms and hedge structure.
Priority: A+

## W32I-E21 — Stock-Based Compensation Dilution
Measure recurring gross issuance from employee equity programs separately from capital-raising issuance.
Priority: A

## W32I-E22 — Repurchase Offset to Compensation
Feature:
issuer repurchases - shares issued for compensation.
Question:
is buyback economically reducing share count or mostly neutralizing dilution?
Priority: A+

## W32I-E23 — Net Issuer Share Flow
NISF =
executed repurchase shares
-
primary issuance
-
employee issuance
± settlement adjustments.
Positive = net issuer demand/reduction in float.
Priority: S

## W32I-E24 — Net Issuer Dollar Flow
Translate W32I-E23 into notional using point-in-time execution/offer prices where known.
Priority: S

## W32I-E25 — Issuer Flow / Free-Float Quotient
IFQ =
net issuer shares
/
tradable free float.
Priority: S

## W32I-E26 — Issuer Flow / Adaptive Liquidity Quotient
IFALQ =
expected net issuer notional
/
continuous + auction + block-liquidity capacity.
Priority: S

## W32I-E27 — Issuer Flow × Options Gamma
Same repurchase/issuance flow may have larger impact when dealer gamma/liquidity state amplifies spot movement.
Priority: S-

## W32I-E28 — Issuer Flow × Benchmark Rebalance
Fuse with W26R:
ASR/buyback/issuance overlapping index additions, deletions or weight changes.
Priority: S-

## W32I-E29 — Announcement-to-Execution Reality Gap
Difference between announced authorization/offering capacity and subsequently executed flow.
Priority: S

## W32I-E30 — Buyback Suspension / Termination Shock
Track disclosed expiration, replacement, suspension or intent not to make further purchases.
Priority: A+

## W32I-E31 — Cash / Leverage Repurchase Capacity
Condition future execution probability on:
cash generation,
net leverage,
debt covenants,
maturities,
dividends,
M&A.
Priority: A

## W32I-E32 — Index-Level Issuer Flow Breadth
Aggregate confirmed/estimated issuer demand and supply across SPX/NDX constituents by index weight and sector.
Priority: S-

## W32I-E33 — Mega-Cap Issuer Flow Concentration
For NQ/QQQ:
issuer-flow notional concentrated in largest weights can matter disproportionately to index-level demand.
Priority: S

## W32I-E34 — Issuer-Flow Truth Ladder
AUTHORIZATION / REGISTRATION
-> CONTRACTED FLOW
-> EXECUTED FLOW
-> SHARE-COUNT CHANGE
-> LIQUIDITY ABSORPTION
-> PRICE/BASIS EFFECT.

Priority: S architecture

## Highest-priority W32I tests
1. W32I-E03 Item 703 Monthly Repurchase Reality
2. W32I-E10 ASR Initial Delivery Shock
3. W32I-E11 ASR Dealer Acquisition Envelope
4. W32I-E16 ATM Realized Issuance
5. W32I-E18 Follow-On Equity Supply
6. W32I-E23 Net Issuer Share Flow
7. W32I-E25 Issuer Flow / Free-Float Quotient
8. W32I-E26 Issuer Flow / Adaptive Liquidity Quotient
9. W32I-E29 Announcement-to-Execution Reality Gap
10. W32I-E33 Mega-Cap Issuer Flow Concentration
