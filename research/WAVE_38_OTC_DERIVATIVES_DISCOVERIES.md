# Wave 38O — OTC Derivatives Risk Transfer

Namespace: **W38O**

Thesis: public swap-data-repository dissemination exposes a large class of institutional risk transfers that do not appear in lit-exchange order books. The public data are anonymous and sometimes delayed/capped, so the valid research target is product-level repricing, concentration, timing, structure, and cross-market propagation—not fabricated counterparty identity or customer direction.

All candidates are research hypotheses only. Claude owns implementation.

## W38O-E01 — Rates Swap Repricing Pulse

Primary source:
CFTC Part 43 public swap dissemination from registered SDRs.

Build transaction-level repricing by:
currency,
UPI/product,
tenor,
effective date,
fixed/floating terms,
price/rate,
notional bucket,
execution time.

Target:
unexpected swap-rate movement relative to matched Treasury/OIS/futures state.

Priority: S

## W38O-E02 — Tenor-Specific Rates Pressure

Aggregate abnormal activity and repricing into tenor buckets:
front end,
belly,
long end,
forward-starting where identifiable.

Question:
which curve segment is absorbing the strongest OTC risk transfer?

Priority: S

## W38O-E03 — Swap Curve Kink Shock

Feature:
observed OTC rate at tenor
-
smooth contemporaneous curve expectation.

Require transaction-quality/liquidity controls.

Priority: A+

## W38O-E04 — Rates OTC vs Treasury Futures Divergence

Compare swap repricing/activity with:
SOFR futures,
Treasury futures,
cash Treasury curve.

State:
OTC_LEADS
FUTURES_LEAD
SYNCHRONOUS
DISLOCATED.

Priority: S

## W38O-E05 — Cleared vs Uncleared Activity Mix

Where public fields permit:
track cleared/intended-to-clear state by product and regime.

Question:
does stress migrate toward standardized cleared instruments or bespoke uncleared structures?

Priority: A

## W38O-E06 — SEF / Platform Concentration

Where public dissemination exposes platform identifiers or execution-venue fields:
measure share of activity by venue/platform and off-facility state.

Do not equate venue with customer/dealer identity.

Priority: A

## W38O-E07 — Large-Notional Censored Flow Intensity

Part 43 public notionals are rounded/capped under applicable rules.

Build:
count of capped observations,
lower-bound notional,
censored-size intensity,
share of activity in large-trade class.

Never substitute cap value as exact notional.

Priority: S

## W38O-E08 — Block-Delay Arrival Burst

Large/block trades can be publicly disseminated after regulatory delay.

Feature:
delayed-print burst
relative to
execution timestamps.

Research whether clustered delayed prints reveal prior risk-transfer episodes after the fact and improve state estimation.

Priority: A+

## W38O-E09 — Execution-to-Dissemination Latency State

For every trade:
public dissemination timestamp
-
execution timestamp.

Use to avoid false lead/lag claims across markets.

Priority: S methodology/edge hybrid

## W38O-E10 — Package Transaction Pressure

Public Part 43 technical fields support package identifiers/indicators and package pricing elements where applicable.

Research:
package activity,
multi-leg concentration,
package-vs-outright repricing.

Priority: S-

## W38O-E11 — Basis Swap Stress

Identify basis-type rates products via UPI/reference data.

Feature:
basis spread move
× abnormal transaction count/notional lower bound.

Priority: A+

## W38O-E12 — Forward-Starting Hedge Demand

Separate spot-starting vs forward-starting rates swaps where product terms allow.

Potential use:
future issuance/refinancing/asset-liability hedging regime.

Priority: A

## W38O-E13 — Swap Option / Optionality Activity

Where public swap/SBS feeds disseminate applicable option products:
track premium/strike/expiry structure and transaction bursts.

Do not infer directional volatility demand without defensible payoff-side semantics.

Priority: A

## W38O-E14 — Index CDS Protection Repricing

CFTC public credit derivatives include index products.

Build:
index CDS spread/price repricing
× activity
× maturity/on-the-run state.

Compare with HY/IG cash credit and equity index.

Priority: S

## W38O-E15 — Index CDS OTC vs ETF/Cash Credit Gap

Compare public index-CDS transaction state with:
HYG/LQD,
TRACE bond stress,
CDX/iTraxx proxies where lawful,
equity volatility.

Priority: S

## W38O-E16 — Single-Name CDS Stress

Primary source:
SEC Regulation SBSR public security-based-swap dissemination.

Single-name credit derivatives are security-based swaps.

Build issuer-level:
CDS transaction intensity,
price/spread shock,
maturity concentration,
censored notional lower bounds.

Priority: S

## W38O-E17 — Sovereign CDS Stress

Use SEC SBS public data where sovereign single-name CDS are disseminated.

Target:
country-specific credit risk before/alongside sovereign cash-bond/FX stress.

Priority: A+

## W38O-E18 — Equity Total-Return Swap Activity

Security-based swaps can include equity total-return products.

Research issuer-level abnormal SBS activity around:
earnings,
index changes,
ownership events,
financing,
short stress.

Hard rule:
public SBS data do not reveal beneficial owner/counterparty identity.

Priority: S-

## W38O-E19 — Equity Swap × Cash Short Constraint

Fuse W33S short constraints with equity SBS activity.

Question:
does OTC synthetic exposure become unusually active when borrow/settlement constraints tighten?

Priority: S

## W38O-E20 — CDS × Equity Reality Gap

Fuse W25C and W32R.

State:
single-name CDS deterioration
while
equity remains stable,
or inverse.

Priority: S

## W38O-E21 — OTC Credit × TRACE Confirmation

Compare issuer/index derivative repricing to corporate-bond transaction residuals.

Goal:
distinguish broad hedge flow from issuer-specific cash-credit deterioration.

Priority: S

## W38O-E22 — Commodity Swap Location Stress

CFTC commodity public reporting can include product/location information subject to geographic-masking rules.

Research:
abnormal hedging/repricing by energy/commodity hub,
with exact product/location semantics.

Priority: A+

## W38O-E23 — Gas Basis Swap Confirmation

Fuse public commodity swap activity with W22G gas nomination/basis state.

Question:
do physical transport constraints coincide with OTC basis-risk transfer?

Priority: S-

## W38O-E24 — Power Swap Congestion Confirmation

Fuse W23T/W25R power-grid scarcity with public power-related swap activity where product mapping is available.

Priority: A

## W38O-E25 — Commodity Physical-Delivery Flag State

Part 43 technical specification includes physical-commodity/product attributes under current reporting schema.

Separate:
financial hedge,
physical-delivery-related structure,
and location-masked products where possible.

Priority: A

## W38O-E26 — Cross-SDR Fragmentation Map

Registered SDRs can each receive portions of the market.

Build by product:
DTCC,
CME,
KOR,
other current registered repository as applicable.

Never interpret one repository's volume as total market without coverage analysis.

Priority: S

## W38O-E27 — Cross-SDR Duplicate / Transfer Guard

Lifecycle moves, migrations, corrections and repository changes can create apparent duplicate activity.

Create UTI/dissemination/lifecycle dedupe logic before aggregation.

Priority: S methodology/edge hybrid

## W38O-E28 — UPI Normalized Product Graph

Use ANNA DSB UPI reference data for rates/credit/FX/equity and designated classes.

Map:
UPI
-> asset class
-> instrument type
-> underlier
-> term structure
-> optionality
-> settlement attributes.

Priority: S infrastructure

## W38O-E29 — Correction / Cancellation Shock Filter

Public dissemination includes action/lifecycle/correction semantics.

Distinguish:
NEW
MODIFY
CORRECT
CANCEL/ERROR
TERMINATION
where public schema supports.

Priority: S

## W38O-E30 — OTC Activity Surprise

For each normalized product bucket:
actual trade count/censored notional
-
expected activity given clock, event calendar and volatility.

Priority: S

## W38O-E31 — OTC Price Impact per Censored Notional

Estimate price movement per lower-bound/censored trade-size measure.

Use interval-censoring methods rather than exact notional.

Priority: A+

## W38O-E32 — Cross-Asset Hedge Cascade

Graph:
rates shock
-> rates swaps
-> credit index
-> single-name credit
-> equity SBS
-> cash/futures/options.

Target:
time-varying sequence of institutional risk transfer.

Priority: S

## W38O-E33 — Public OTC Stress Breadth

Aggregate standardized stress across:
rates,
credit,
equity SBS,
commodity swaps,
FX products within legal/public coverage.

Weight by product liquidity and source reliability.

Priority: S-

## W38O-E34 — OTC Risk-Transfer Truth Ladder

PUBLIC SDR PRINT
-> NORMALIZED PRODUCT
-> CENSORED-SIZE/PRICE SHOCK
-> CROSS-MARKET CONFIRMATION
-> INTERMEDIATE RISK OUTCOME
-> MARKET RESPONSE.

No counterparty or directional narrative may be promoted without observable evidence.

Priority: S architecture

## Highest-priority W38O tests

1. W38O-E01 Rates Swap Repricing Pulse
2. W38O-E04 Rates OTC vs Treasury Futures Divergence
3. W38O-E07 Large-Notional Censored Flow Intensity
4. W38O-E10 Package Transaction Pressure
5. W38O-E14 Index CDS Protection Repricing
6. W38O-E16 Single-Name CDS Stress
7. W38O-E19 Equity Swap × Cash Short Constraint
8. W38O-E21 OTC Credit × TRACE Confirmation
9. W38O-E26 Cross-SDR Fragmentation Map
10. W38O-E32 Cross-Asset Hedge Cascade
