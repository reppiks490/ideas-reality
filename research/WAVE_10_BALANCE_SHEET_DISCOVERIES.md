# Wave 10B — Dealer Balance Sheet and Funding Plumbing

Namespace: W10B

This wave models who is warehousing securities risk, how that inventory is financed, whether settlement is failing, how hedge-fund/money-fund repo channels are expanding, and when Treasury issuance must be absorbed by constrained intermediaries.

All candidates remain hypotheses until falsified and promoted.

## W10B-E01 — Primary Dealer Duration Inventory Pressure

Source:
New York Fed Primary Dealer Statistics, FR 2004.

Status:
WEEKLY, published Thursday around 4:15 p.m. ET for the prior week.

Build maturity-bucket net positions for:
Treasuries, TIPS, agencies, MBS and relevant fixed-income categories.

Feature:
inventory z-score × duration × change.

Hypothesis:
large dealer duration inventory can alter auction absorption, Treasury liquidity and willingness to warehouse additional risk.

Priority: S

## W10B-E02 — Dealer Inventory-to-Transaction Velocity

Fuse:
dealer net positions
/ cumulative outright transaction volume.

Interpretation:
large inventory with falling turnover differs from large inventory in a liquid/high-turnover market.

Candidate:
inventory_days =
abs(net_position) / average_daily_outright_volume.

Priority: A+

## W10B-E03 — Dealer Financing Asymmetry

Source:
FR 2004 financing data.

Compare securities-in:
reverse repo + borrowed

to securities-out:
repo + lent

by collateral class and tenor.

Output:
NET_CASH_PROVIDER / NET_CASH_BORROWER / COLLATERAL_SEEKER / BALANCED.

Priority: S-

## W10B-E04 — Primary Dealer Settlement-Fail Stress

Source:
NY Fed weekly fails-to-deliver / fails-to-receive.

Features:
- Treasury fail level
- fail acceleration
- fails / transaction volume
- FTR vs FTD asymmetry
- asset-class breadth
- persistence

Use:
settlement/collateral-friction state, not a manipulation label.

Priority: S

## W10B-E05 — Specific-Issue Treasury Scarcity

Fuse:
NY Fed specific-issue FR2004 data
+ SOMA securities lending
+ repo specialness
+ Treasury issue characteristics.

Goal:
identify CUSIP/maturity-level collateral scarcity rather than aggregate Treasury stress.

Priority: S

## W10B-E06 — When-Issued Dealer Positioning

Source:
FR 2004WI aggregate daily positions in Treasury securities offered but not yet issued, where public aggregate data are available.

Question:
Does pre-auction/when-issued dealer positioning improve models of auction concession, tail and post-auction inventory pressure?

Priority: A+

## W10B-E07 — Repo Venue Migration

Source:
OFR U.S. Repo Markets Data Release.

Status:
DAILY preliminary update around 3 p.m.; centrally cleared data generally one-day lag, tri-party roughly two-day lag; final quarterly validated series.

Segments:
FICC DVP
FICC GCF
tri-party.

Feature:
share of repo activity migrating between venues.

Mechanism:
venue choice reflects differences in clearing, counterparty visibility, specific-collateral demand and financing use.

Priority: S

## W10B-E08 — Specific-Collateral vs Pure-Funding Repo State

OFR distinguishes:
- DVP, where specific securities matter
- GCF, general-collateral financing
- tri-party, general collateral financing.

Candidate:
specific_collateral_intensity =
DVP volume growth - GC venue volume growth

Interpretation:
separate demand for particular securities from broad cash funding demand.

Priority: S

## W10B-E09 — Repo Rate / Volume Stress Surface

Build by venue × collateral × tenor:
rate residual
volume residual
rate-volume interaction.

States:
LIQUID
CASH_SCARCE
COLLATERAL_SCARCE
BALANCE_SHEET_CONSTRAINED
DISLOCATED.

Priority: S

## W10B-E10 — Sponsored Repo Hedge-Fund Borrowing Pulse

Source:
FICC Sponsored Repo Service public volumes via OFR/DTCC.

Official interpretation:
sponsored repo is often non-dealer borrowing against securities; the majority of sponsored repo borrowing activity involves hedge funds.

Research:
abnormal sponsored repo borrowing
× Treasury basis dislocation
× dealer balance-sheet capacity.

Priority: S-

## W10B-E11 — Sponsored Reverse-Repo Money-Fund Supply

Sponsored reverse repo is predominantly cash lending by money-market funds according to OFR descriptions.

Fuse:
FICC sponsored reverse-repo volume
+ N-MFP holdings/flows
+ ON RRP
+ private repo rates.

Goal:
measure migration of money-fund cash into private Treasury financing.

Priority: A+

## W10B-E12 — Treasury Auction Investor-Class Surprise

Source:
Treasury Investor Class Auction Allotments / auction results.

Classes can include:
primary dealers, investment funds, depository institutions, pensions/retirement, insurance, foreign/international and others.

Feature:
actual class allotment share
-
expected share by tenor, auction type and macro regime.

Priority: S-

## W10B-E13 — Dealer Takedown Burden

Candidate:
primary dealer allotment
× auction size
/ estimated dealer balance-sheet capacity.

Enhance with:
pre-auction dealer inventory,
repo financing stress,
when-issued position,
auction tail,
post-auction inventory.

Question:
When are dealers forced to warehouse unusually large issuance?

Priority: S

## W10B-E14 — Foreign / Investment-Fund Auction Demand State

Track investor-class demand separately rather than use indirect-bidder share as a proxy for foreign demand.

State:
FOREIGN_STRONG
FUND_STRONG
DEALER_HEAVY
BANK_STRONG
BROAD_DEMAND.

Priority: A

## W10B-E15 — Weekly Bank Credit Pulse

Source:
Federal Reserve H.8 Assets and Liabilities of Commercial Banks.

Status:
WEEKLY aggregate release, with revisions/benchmarking.

Candidate features:
- C&I loan growth
- commercial real-estate loan growth
- consumer loan growth
- securities holdings
- cash assets
- deposits
- large vs small bank divergence

Use:
slow credit-supply and liquidity state.

Priority: A

## W10B-E16 — Bank Deposit-to-Credit Funding Gap

Construct:
loan growth - deposit growth
and
securities growth - deposit growth.

Hypothesis:
rapid asset growth unsupported by deposit growth changes marginal wholesale-funding pressure and lending appetite.

Priority: A

## W10B-E17 — Dealer Financing Terms Regime

Source:
Federal Reserve Senior Credit Officer Opinion Survey (SCOOS).

Status:
QUARTERLY.

Fields cover price/nonprice terms, haircuts, financing demand, client leverage and collateral/mark disputes across hedge funds and other counterparties.

Use:
slow structural prior for live repo/dealer signals.

Priority: A-

## W10B-E18 — Hedge-Fund Leverage Structural Prior

Sources:
OFR Hedge Fund Monitor / aggregated SEC Form PF.

Status:
DELAYED/AGGREGATED.

Features:
gross-to-net leverage
repo borrowing
long/short repo exposure
collateral
asset-class exposure
concentration by largest funds.

Use:
regime prior, never current fund-level positioning.

Priority: A

## W10B-E19 — Basis-Trade Fragility State

Fuse:
Form PF/OFR hedge-fund Treasury exposure
+ sponsored repo borrowing
+ dealer financing capacity
+ repo rates
+ Treasury cash-futures basis
+ margin/volatility.

Hypothesis:
same basis dislocation has different crash/mean-reversion behavior depending on leverage and financing availability.

Priority: S

## W10B-E20 — Treasury Central-Clearing Transition Regime

Structural event:
SEC Treasury clearing requirements phase in across cash and repo markets in 2026–2027.

Research:
treat clearing migration as a market-structure break affecting:
netting,
dealer balance-sheet use,
repo venue share,
margin,
sponsored access,
liquidity.

Never train one stationary model blindly across implementation.

Priority: S

## W10B-E21 — Dealer Balance-Sheet Capacity Index

Fuse:
dealer inventory
+ financing
+ repo rates/volumes
+ fails
+ auction takedown
+ SCOOS terms
+ bank funding conditions.

Output:
ABUNDANT / NORMAL / TIGHT / CONSTRAINED.

Purpose:
condition Treasury liquidity, auction, basis and cross-asset models.

Priority: S

## W10B-E22 — Leveraged-Fund / Dealer Resonance

Hypothesis:
stress becomes nonlinear when:
hedge-fund borrowing rises
while
dealer balance-sheet capacity falls.

Fuse high-frequency repo/sponsored data with slower Form PF/SCOOS priors.

Output:
low / moderate / elevated / critical resonance state.

Priority: S

## Highest-priority W10B tests

1. W10B-E01 Dealer Duration Inventory
2. W10B-E04 Settlement-Fail Stress
3. W10B-E07 Repo Venue Migration
4. W10B-E08 Specific-Collateral vs Funding State
5. W10B-E09 Repo Rate/Volume Stress
6. W10B-E10 Sponsored Repo Hedge-Fund Borrowing
7. W10B-E12 Investor-Class Auction Surprise
8. W10B-E13 Dealer Takedown Burden
9. W10B-E19 Basis-Trade Fragility
10. W10B-E21 Dealer Balance-Sheet Capacity
