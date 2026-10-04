# Wave 55T — Treasury Financing & Settlement Liquidity

Namespace: **W55T**

Thesis: Treasury financing pressure is not captured by gross auction size. The relevant state is the amount of cash the private sector must absorb at each settlement, conditioned on maturities, SOMA add-ons, bill/CMB issuance, buybacks, dealer balance-sheet capacity, demand composition, repo specialness and the Treasury General Account path.

The research target is the **actual financing/liquidity impulse** transmitted through Treasury auctions and settlements into rates, funding markets and risk assets such as NQ.

All candidates are research hypotheses only. Claude owns any later implementation.

## W55T-E01 — Auction Announcement State

Primary source:
TreasuryDirect auction announcements / Treasury Quarterly Refunding.

Track:
security,
CUSIP,
new issue/reopening,
offering amount,
auction date/time,
issue/settlement date,
maturity date,
NLP threshold,
competitive/noncompetitive deadlines.

Priority: S

## W55T-E02 — Auction Size Surprise

Feature:
announced offering amount
-
pre-announcement public expectation.

Expectation sources may include:
Quarterly Refunding guidance,
Treasury's tentative schedule,
Primary Dealer Auction Size Survey,
consensus estimates.

Priority: S

## W55T-E03 — Quarterly Refunding Financing Revision

Track changes in Treasury's quarterly borrowing estimate and assumed quarter-end cash balance.

Priority: S

## W55T-E04 — Coupon Issuance Path Revision

Compare announced 2Y/3Y/5Y/7Y/10Y/20Y/30Y/FRN/TIPS sizes to prior guidance.

Priority: S

## W55T-E05 — Bill Issuance Path Revision

Extract guidance for:
benchmark bill increases/reductions,
seasonal changes,
tax-date reductions,
fiscal-outflow increases.

Priority: S-

## W55T-E06 — Cash Management Bill Shock

State:
NO_CMB
CMB_ANNOUNCED
CMB_AUCTIONED
CMB_SETTLED
CMB_MATURED.

CMBs can create short-dated financing impulses outside the regular bill cycle.

Priority: S

## W55T-E07 — Private Net Cash Raised

For a refunding/issue:
private-sector new cash =
public issuance to private investors
-
privately held maturing Treasury debt refinanced.

Use Treasury's own new-cash/paydown calculations where available.

Priority: S

## W55T-E08 — Gross-vs-Net Issuance Gap

Feature:
gross issuance
-
private net cash raised.

Purpose:
avoid mistaking rollover/refunding activity for new private-sector financing demand.

Priority: S

## W55T-E09 — Settlement-Day Cash Drain

Aggregate by settlement date:
cash due from private investors
-
Treasury redemptions to private holders
-
cash-management buyback payouts where appropriate
± other verified Treasury cash-flow offsets.

Priority: S

## W55T-E10 — Settlement Cluster Density

Feature:
multiple coupon/bill/TIPS/FRN settlements
within same day/window.

Priority: A+

## W55T-E11 — Settlement Shock Quotient

SSQ =
net private settlement demand
/
estimated immediately available dealer/investor balance-sheet capacity.

Priority: S

## W55T-E12 — SOMA Auction Add-On

Primary source:
Treasury auction results / NY Fed rollover policy.

SOMA rollover bids are noncompetitive add-ons to announced auction size.

Track:
SOMA accepted,
SOMA holdings maturing,
allocation across securities.

Priority: S

## W55T-E13 — Private Absorption Ex-SOMA

Feature:
total accepted
-
SOMA accepted
-
other non-private add-ons where applicable.

Priority: S

## W55T-E14 — SOMA Rollover Regime

Track FOMC/NY Fed policy determining whether maturing Treasuries are rolled over, redeemed or otherwise reinvested.

Priority: S

## W55T-E15 — Auction Bid-to-Cover

Primary source:
TreasuryDirect Auction Query.

Track total tendered / total accepted.

Use maturity/security-specific historical distribution.

Priority: A+

## W55T-E16 — Primary Dealer Award Share

Feature:
primary dealer accepted
/
competitive/public accepted.

Priority: S

## W55T-E17 — Direct Bidder Award Share

Feature:
direct bidder accepted
/
competitive/public accepted.

Priority: A+

## W55T-E18 — Indirect Bidder Award Share

Feature:
indirect bidder accepted
/
competitive/public accepted.

Important:
indirect does not equal foreign; Treasury states both foreign and domestic customers can be indirect.

Priority: S

## W55T-E19 — Dealer Backstop Burden

High dealer share conditioned on weak non-dealer demand and existing dealer inventory may indicate balance-sheet absorption pressure.

Priority: S

## W55T-E20 — Auction Tail / Stop-Through

With point-in-time when-issued yield from a lawful market feed:
high auction yield
-
pre-auction WI yield.

Positive = tail, negative = stop-through.

Priority: S

## W55T-E21 — Tail Adjusted for Intraday Rates Move

Separate auction-specific concession from broad market move immediately before 1 p.m. ET auction close.

Priority: S-

## W55T-E22 — Auction Concession Build

Measure pre-auction cheapening relative to:
curve,
swap,
neighboring issues,
historical concession.

Priority: A+

## W55T-E23 — Post-Auction Repricing

Track first:
1m,
5m,
15m,
60m
yield/futures/NQ reaction after auction result publication.

Research mechanism only after auction quality state is defined.

Priority: A+

## W55T-E24 — Dealer Inventory Preload

Primary source:
NY Fed Primary Dealer Statistics.

Estimate dealer Treasury position change in relevant maturity bucket before heavy auction/settlement week.

Priority: S

## W55T-E25 — Dealer Inventory Saturation

State:
dealer net position
relative to historical distribution,
financing usage,
recent auction awards.

Priority: S

## W55T-E26 — Dealer Financing Burden

Use Primary Dealer Statistics financing data to assess repo/reverse-repo dependence around issuance.

Priority: A+

## W55T-E27 — Dealer Fails Stress

Primary dealer fail-to-deliver/receive statistics can indicate settlement or collateral stress.

Priority: S-

## W55T-E28 — Fed Securities-Lending Demand

Primary source:
NY Fed daily SOMA securities lending.

CUSIP-level submitted/accepted amounts can identify specialness demand and collateral scarcity.

Priority: S

## W55T-E29 — Auctioned-CUSIP Specialness

Track securities-lending demand for newly auctioned/reopened CUSIP before/after settlement.

Priority: S

## W55T-E30 — Reopening Specialness Risk

Reopenings can have different repo dynamics from new issues.

Model separately.

Priority: A+

## W55T-E31 — 20-Year Settlement Regime Break

Treasury changed 20-year reopening settlement timing beginning June 2026 so reopenings settle Friday of auction week, explicitly to mitigate repo specialness.

Encode pre/post regime separately.

Priority: S methodology/edge hybrid

## W55T-E32 — Treasury Buyback State

Primary source:
Treasury tentative schedules and operation results.

State:
ANNOUNCED
OPERATION_OPEN
RESULT
SETTLED.

Priority: S

## W55T-E33 — Liquidity-Support Buyback Intensity

Track:
maximum purchase amount,
accepted amount,
maturity bucket,
offer volume,
price dispersion where public.

Priority: S-

## W55T-E34 — Cash-Management Buyback Impulse

Cash-management buybacks target short maturities and can alter near-term redemption profile/TGA cash use.

Model distinctly from liquidity-support buybacks.

Priority: S

## W55T-E35 — Buyback Offer-to-Accept Ratio

Feature:
submitted offers
/
accepted amount.

Potential signal of off-the-run liquidity demand or cheapness, subject to Treasury selection policy.

Priority: A

## W55T-E36 — Buyback Settlement Offset

In settlement-liquidity models:
include actual Treasury cash paid for accepted buybacks on settlement date.

Avoid treating buyback announcement size as guaranteed cash injection.

Priority: S

## W55T-E37 — Buyback Maturity-Profile Shift

Measure how accepted buybacks alter future redemption concentrations.

Priority: A+

## W55T-E38 — Long-End Buyback Regime Change

Treasury increased long-end liquidity-support buyback maximums beginning September 9, 2026.

Preserve this as a structural break.

Priority: S

## W55T-E39 — TGA Target / Financing Gap

Compare:
Treasury projected cash balance
vs
realized Daily Treasury Statement/TGA trajectory.

Priority: S

## W55T-E40 — TGA Rebuild / Drawdown Velocity

Feature:
daily/weekly change in TGA
conditioned on tax dates, issuance and spending.

Priority: S

## W55T-E41 — Tax-Date Funding Offset

Corporate/non-withheld tax receipts can reduce near-term bill issuance need.

Fuse public tax calendar/realized receipts with auction schedule.

Priority: A+

## W55T-E42 — Fiscal Outflow Funding Pressure

Known large fiscal outflow periods can require bill/CMB size increases and TGA drawdowns.

Priority: A+

## W55T-E43 — Treasury Financing Forecast Error

Feature:
realized net marketable borrowing
-
prior quarterly financing estimate.

Priority: S-

## W55T-E44 — Primary Dealer Survey Disagreement

Treasury publishes historical Primary Dealer Auction Size Surveys.

Feature:
dispersion around expected future auction sizes.

Priority: A

## W55T-E45 — TBAC-vs-Treasury Policy Gap

Compare TBAC recommended financing path with Treasury's chosen path.

Priority: A+

## W55T-E46 — Maturity-Bucket Supply Shock

Aggregate projected net issuance by duration bucket:
bills,
2-3Y,
5-7Y,
10Y,
20-30Y,
TIPS,
FRN.

Priority: S

## W55T-E47 — Duration Supply Impulse

Convert issuance by maturity into duration/DV01 supply rather than face amount only.

Priority: S

## W55T-E48 — Private Duration Absorption

Duration issued to private sector
minus
duration retired through maturities/buybacks
minus
SOMA absorption where applicable.

Priority: S

## W55T-E49 — Auction Calendar Convexity

Multiple duration-heavy auctions clustered before/after macro events can create nonlinear dealer hedging/concession behavior.

Priority: A+

## W55T-E50 — Auction × Options Gamma State

Fuse W27 volatility/constraint layer:
Treasury supply shock
× rates option gamma
× NQ option gamma.

Priority: A+

## W55T-E51 — Auction × NQ Duration Sensitivity

Estimate NQ response conditional on:
real-rate shock,
nominal-rate shock,
auction maturity,
macro regime.

Priority: S-

## W55T-E52 — Auction × Dollar Liquidity State

Fuse settlement demand with:
TGA,
repo,
reserves,
money-market conditions.

Priority: S

## W55T-E53 — Large Position Reporting Call State

Treasury can issue LPR calls for specific securities.

Use as a concentration/regulatory state, not a direct real-time holdings feed.

Priority: B+

## W55T-E54 — Net Long Position Constraint State

Auction rules cap bidder awards considering net long positions and impose reporting thresholds.

Potentially relevant for concentrated ownership/auction capacity in specific CUSIPs.

Priority: A

## W55T-E55 — Treasury Financing Reality Gap

Compare:
headline gross issuance narrative
vs
actual private net cash + duration absorption.

Priority: S

## W55T-E56 — Settlement-to-Reserve Reality Gap

Compare modeled private cash drain from settlements with observed reserve/repo/TGA responses.

Priority: S

## W55T-E57 — Auction Demand Reality Gap

Compare apparently strong bid-to-cover with:
dealer share,
indirect/direct share,
tail/stop,
post-auction performance.

Priority: S

## W55T-E58 — Treasury Financing Truth Ladder

QUARTERLY GUIDANCE
-> AUCTION ANNOUNCEMENT
-> BIDDING / AUCTION RESULT
-> SETTLEMENT
-> TGA / DEALER BALANCE SHEET
-> REPO / YIELD CURVE
-> NQ / RISK ASSET RESPONSE.

Priority: S architecture

## Highest-priority W55T tests

1. W55T-E07 Private Net Cash Raised
2. W55T-E09 Settlement-Day Cash Drain
3. W55T-E12 SOMA Auction Add-On
4. W55T-E19 Dealer Backstop Burden
5. W55T-E20 Auction Tail / Stop-Through
6. W55T-E28 Fed Securities-Lending Demand
7. W55T-E34 Cash-Management Buyback Impulse
8. W55T-E47 Duration Supply Impulse
9. W55T-E48 Private Duration Absorption
10. W55T-E57 Auction Demand Reality Gap
