# Wave 11C — Mandatory Commitments & Convexity

Namespace: **W11C**

Thesis: some of the strongest lawful public signals are created when an entity is *required* to disclose a completed economic commitment or when market infrastructure mechanically changes the amount of capital/hedging required. This wave focuses on mandatory export-sale flashes, exchange margin shocks, agency MBS/TBA flow, mortgage convexity, municipal transaction transparency, and explicit grid-emergency state transitions.

All candidates are hypotheses for Claude to test later. Nothing here is an implementation or a claim of alpha.

## W11C-E01 — USDA Mandatory Large Export-Sale Flash

Primary source:
USDA Foreign Agricultural Service Export Sales Reporting Program.

Status:
LIVE / scheduled public release.

Official timing:
For covered commodities, sufficiently large sales must be reported by exporters to FAS by 3:00 p.m. ET on the following business day. FAS publishes qualifying daily sales on the subsequent business day at 9:00 a.m. ET.

Current thresholds include:
- 100,000 metric tons or more of one covered commodity sold in one day to one destination, except soybean oil
- 200,000 metric tons or more accumulated to one destination during the reporting week, except soybean oil
- lower 20,000 / 40,000 metric ton thresholds for soybean oil

Fields include commodity/type/class, quantity, marketing year and destination.

Mechanism:
This is a mandatory public confirmation of a large forward physical purchase, often before shipment.

Research:
sale size surprise
× destination
× current outstanding sales
× crop-year supply state
× futures curve
× basis/logistics capacity.

Priority: S

## W11C-E02 — Export Flash Surprise, Not Raw Sale Size

Estimate the probability and expected size of a flash sale using information already public before 9:00 a.m. ET:
- seasonal export pattern
- destination demand
- prior outstanding commitments
- crop-year balance
- FX
- competing-origin prices
- recent cancellations
- shipping/logistics state.

Feature:
flash_surprise = observed mandatory sale - expected sale.

Priority: S

## W11C-E03 — Export Cancellation / Destination-Revision State

USDA reporting also incorporates cancellations and destination changes.

Research:
NEW_COMMITMENT
-> DESTINATION_CHANGE
-> PARTIAL_CANCELLATION
-> FULL_CANCELLATION
-> SHIPPED.

Question:
Does the revision path contain more information than the initial flash?

Hard rule:
reconcile daily flashes with later weekly data; never count the same sale twice.

Priority: A+

## W11C-E04 — Export Demand × Logistics Capacity Collision

Fuse:
W11C-E01 mandatory export-sale demand
+ W7T/W9 physical river/lock/port/rail capacity
+ USDA cash basis
+ export inspections.

Hypothesis:
the same demand shock has larger price/basis impact when physical outbound capacity is constrained.

Priority: S

## W11C-E05 — CME Performance-Bond Shock

Primary source:
CME Clearing Performance Bond / Margin advisories.

Status:
LIVE notices with historical PDF archive.

CME publicly announces product-level margin changes, including initial/maintenance performance bonds and some SPAN parameters. Advisories specify notice date and effective time, commonly after close of business on the stated effective date.

Features:
- percentage change in initial margin
- percentage change in maintenance margin
- margin / contract notional
- margin / realized volatility
- scan-range/SOM change
- affected-contract breadth
- notice-to-effective interval.

Priority: S

## W11C-E06 — Margin Shock × Positioning Vulnerability

A margin increase matters more when leveraged participation is high.

Fuse:
margin requirement change
× open interest
× speculative/crowding state
× volatility
× liquidity
× basis/leverage proxy.

Output:
LOW_IMPACT / ABSORBABLE / DELEVERAGING_RISK / SYSTEMIC_CROSS_PRODUCT.

Priority: S

## W11C-E07 — Cross-Exchange Margin Divergence

Sources:
CME + ICE clearing margin notices.

Research:
For economically related products, compare changes in required collateral across exchanges and contracts.

Hypothesis:
relative margin cost can alter where risk is warehoused, spread liquidity, volume share and basis behavior.

Priority: A+

## W11C-E08 — Margin Notice vs Effective-Time Decomposition

Separate two events:
1. public announcement
2. margin becomes binding/effective.

Test:
- informational reaction at notice
- position reduction before effective time
- forced/non-discretionary adjustment around effective time
- post-change liquidity.

This is essential because margin changes are endogenous to volatility.

Priority: S

## W11C-E09 — Agency TBA TRACE Flow Pulse

Primary source:
FINRA TRACE securitized-products dissemination.

Status:
LIVE market transparency; programmatic access/product terms vary.

FINRA states agency pass-through MBS TBA transactions are publicly disseminated. Historical/current rules require prompt reporting with product-specific delays; TBA good-delivery transactions have historically been subject to 15-minute reporting after the applicable transition, with different treatment for other TBA categories.

2026 development:
FINRA announced new securitized-product datasets through its API platform, including Agency Pass-Thru TBA pricing/activity data accessible with Public API credentials.

Candidate features:
- coupon/maturity bucket trade-intensity surprise
- price/yield residual
- customer/interdealer mix where public fields permit
- trade-size distribution with cap-aware handling
- buy/sell side only where dissemination semantics genuinely identify it.

Priority: S

## W11C-E10 — TBA Dollar-Roll Pressure State

TRACE securitized-product reporting supports special-processing flags for TBA dollar-roll transactions.

Mechanism:
Dollar rolls combine financing, settlement and MBS relative-value mechanics.

Research:
- dollar-roll transaction share
- coupon-specific concentration
- roll activity vs implied financing/specialness
- roll activity vs settlement month
- roll activity vs Fed MBS operations.

Output:
NORMAL_FINANCING / SPECIAL_COLLATERAL / SETTLEMENT_PRESSURE / POSITION_ROLL.

Priority: S-

## W11C-E11 — Mortgage Convexity Amplification State

Mechanism:
Fixed-rate mortgage borrowers hold a prepayment option. When rates rise, prepayments slow and MBS duration can extend; hedgers may need additional duration shorts/pay-fixed exposure. When rates fall, duration can shorten and hedges can reverse.

Federal Reserve research has documented that mortgage hedging can amplify long-rate movements and rate volatility.

Build a point-in-time state from:
- TBA coupon distribution
- current mortgage-rate incentive
- MBS coupon concentration
- TBA flow
- prepayment/factor history
- Treasury/swap volatility.

Output:
CONVEXITY_DAMPED / NEUTRAL / EXTENSION_PRESSURE / REFI_SHORTENING_PRESSURE.

Priority: S

## W11C-E12 — TBA-to-Treasury Futures Hedge-Pressure Graph

Fuse:
TBA TRACE flow
+ W11C-E11 convexity state
+ Treasury futures order flow
+ swap/SDR rates flow
+ dealer balance-sheet state from W10B.

Question:
When do MBS flows mechanically create incremental Treasury futures pressure rather than merely co-move with rates?

Strict requirement:
lagged causal timing and common-rate-news controls.

Priority: S

## W11C-E13 — Mortgage Convexity × NQ Duration Channel

Research chain:
mortgage extension/shortening pressure
-> Treasury/swap yield amplification
-> long-duration equity discount-rate shock
-> NQ response.

Do not test direct TBA->NQ return first.

Promotion ladder:
1. prove TBA/convexity predicts rate-market response
2. prove incremental rate response
3. only then test NQ spillover.

Priority: A+

## W11C-E14 — Agency MBS Coupon / Refinance Exposure Surface

Sources:
Fannie Mae, Freddie Mac and Ginnie Mae public securities disclosures plus mortgage-rate data.

Build:
outstanding balance by coupon/vintage
× refinance incentive
× burnout/seasoning proxy
× historical factor/prepayment response.

Purpose:
estimate which part of the MBS universe has the greatest duration sensitivity to a rate move.

Priority: A+

## W11C-E15 — Fed Agency-MBS Operation Collision

Source:
New York Fed agency MBS operation schedule/results.

The Desk publicly announces operation windows and posts results after operations. In 2026 it has continued small-value readiness operations in agency MBS.

Research:
Fed operation
× TBA flow
× coupon specialness
× convexity state
× dealer capacity.

Important:
small-value operations are deliberately small; do not assume market impact. Treat them as clean, timestamped mechanical-flow experiments first.

Priority: A

## W11C-E16 — Real-Time Municipal Credit / Liquidity Pulse

Primary source:
MSRB Real-Time Transaction Reporting System / EMMA.

Status:
LIVE market transparency. Most municipal trades must be reported as soon as practicable and generally within 15 minutes; MSRB states public transaction information is made available almost immediately after receipt/error checks. The real-time machine feed is a paid subscription; EMMA provides public web access.

Features:
- issuer/sector yield residual
- trade-price dispersion
- trade frequency
- customer/interdealer state where public semantics permit
- trade-size/liquidity shift
- abnormal concession vs matched muni curve.

Priority: A+

## W11C-E17 — Municipal Stress -> Regional Financial Exposure Graph

Build:
municipal issuer
-> geography
-> sector/project
-> bond insurer
-> bank/insurer/fund holder exposure where point-in-time public data permit
-> listed issuer.

Research:
Does abnormal muni stress identify localized fiscal/economic deterioration or balance-sheet exposure before equity analysts fully reprice it?

Priority: A

## W11C-E18 — PJM Emergency Transition Hazard

Source:
PJM emergency procedures and public alerts.

State ladder:
NORMAL
-> ALERT
-> MAXIMUM_GENERATION / LOAD_MANAGEMENT_ALERT
-> emergency actions
-> demand response / reserve actions
-> recovery.

Research:
Model probability and timing of the next state from load, outages, imports, reserve margins and congestion.

Value:
state transition is an operational intervention, not simply another price feature.

Priority: A+

## W11C-E19 — ERCOT EEA Transition Hazard

Source:
ERCOT public notices/alerts and market data.

Public EEA states include Level 1, Level 2 and Level 3, with reserve/frequency triggers and explicit emergency actions.

Research:
forecast transition probability from:
Physical Responsive Capability
+ reserve trend
+ renewable forecast error
+ thermal outages
+ load
+ storage duration
+ imports.

Output:
P(EEA1), P(EEA2), P(EEA3), expected duration and recovery probability.

Priority: S-

## W11C-E20 — Emergency Intervention / Industrial Load Displacement

Fuse:
grid emergency state
+ demand-response deployment
+ controlled-load reduction
+ backup-generation directives/availability where public
+ industrial/data-center geographic exposure.

Mechanism:
Grid emergency actions can alter both power prices and actual industrial/commercial grid demand.

Research:
first quantify load displaced and duration, then map exposed sectors/facilities.

Priority: A+

## W11C-E21 — Mandatory-Disclosure Clock Arbitrage Test

Compare event classes where information becomes public at a known legal/operational clock:
- 9:00 a.m. USDA daily sales
- TRACE dissemination after reporting
- MSRB post-trade dissemination
- margin advisories/effective times
- grid emergency notices.

Question:
Which markets reprice immediately and which show measurable, repeatable digestion lag?

Priority: S research method/edge hybrid

## W11C-E22 — Commitment-to-Physical-Reality Gap

General framework:

MANDATORY_COMMITMENT
-> financing/collateral requirement
-> logistics/settlement
-> physical realization.

Examples:
USDA sale -> shipment
TBA trade -> settlement
municipal trade stress -> fiscal/credit outcome
margin hike -> position reduction
grid alert -> demand response/load shed.

Feature:
expected realization - observed realization.

Priority: S

## Highest-priority W11C tests

1. W11C-E01 USDA Mandatory Large Export-Sale Flash
2. W11C-E04 Export Demand × Logistics Capacity Collision
3. W11C-E05 CME Performance-Bond Shock
4. W11C-E06 Margin Shock × Positioning Vulnerability
5. W11C-E09 Agency TBA TRACE Flow Pulse
6. W11C-E11 Mortgage Convexity Amplification State
7. W11C-E12 TBA-to-Treasury Futures Hedge-Pressure Graph
8. W11C-E16 Real-Time Municipal Credit / Liquidity Pulse
9. W11C-E19 ERCOT EEA Transition Hazard
10. W11C-E22 Commitment-to-Physical-Reality Gap
