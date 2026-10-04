# Wave 26R — Benchmark Rebalance & Forced Flow

Namespace: **W26R**

Thesis: benchmark providers publish deterministic or semi-deterministic changes that force passive/indexed capital to alter holdings at known implementation clocks. The edge is not "index addition goes up"; it is the size, timing, uncertainty, and absorption capacity of mechanically required flow across stocks, ETFs, futures and options.

All candidates are research hypotheses only. Claude owns implementation.

## W26R-E01 — S&P Addition/Deletion Forced-Flow Estimate

Primary source:
S&P Dow Jones Indices public index announcements and methodology.

S&P methodology states S&P 500/400/600 additions/deletions are generally announced with at least three business days advance notice and public announcements are posted before or at the same time as clients/affected companies.

Estimate:
target_index_weight
× assets_tracking_index
-
current indexed ownership from source index.

Priority: S

## W26R-E02 — Announcement-to-Effective Pressure Path

Track:
announcement close
AD+1
...
effective-date close
next open.

Research:
pre-positioning,
passive catch-up,
closing-auction pressure,
post-effective reversal.

Priority: S

## W26R-E03 — Closing-Auction Forced-Flow Ratio

Candidate:

FFAR =
estimated forced buy/sell dollars
/
expected closing-auction executable liquidity.

Expected liquidity is security-specific and conditioned on event type/market regime.

Priority: S

## W26R-E04 — Migrating vs Non-Migrating Index Change

An S&P 400 -> S&P 500 migration has both forced buying and forced selling by different tracker pools.

Estimate net:
destination-index demand
-
origin-index liquidation.

Do not treat gross destination flow as net pressure.

Priority: S

## W26R-E05 — Index Share / Float Adjustment Flow

Index-provider changes to shares/float can force passive reweighting without membership change.

Feature:
delta_index_shares
× index price
× tracking assets.

Priority: S-

## W26R-E06 — S&P Announcement Surprise

S&P 500 membership is committee-based rather than a fully mechanical scheduled reconstitution.

Model pre-announcement inclusion probability from public eligibility information.

Research:
actual addition
-
ex ante inclusion probability.

Priority: A+

## W26R-E07 — Nasdaq-100 Quarterly Rank-Removal Pressure

2026 Nasdaq-100 methodology introduced scheduled March/June/September rank-based rebalance mechanics in addition to annual December reconstitution.

Build point-in-time ranks and estimate:
probability of removal/addition
before reference/announcement dates.

Priority: S

## W26R-E08 — Nasdaq-100 Fast Entry Pressure

2026 NDX methodology permits qualifying very large newly listed companies to enter on an expedited basis under defined rank/trading-day conditions.

Research:
candidate eligibility
× expected weight
× tracker assets
× free-float liquidity.

Priority: S

## W26R-E09 — Nasdaq-100 Weight-Cap Redistribution

NDX uses modified market-cap weighting with concentration constraints.

When caps bind, mechanical weight removed from one constituent is redistributed across others.

Estimate full-vector flow, not only capped name flow.

Priority: S

## W26R-E10 — Nasdaq Rebalance Weight Interpolation State

2026 methodology uses a Weight Interpolation Process for certain additions/rebalances.

Research exact target-weight calculation and resulting passive share changes.

Priority: A+

## W26R-E11 — Russell Rank-Day Membership Probability

Primary source:
FTSE Russell public reconstitution process.

2026 schedule uses explicit rank dates, preliminary lists, update dates, lock-down and effective close.

Build:
rank-day eligibility
-> preliminary membership probability
-> final membership.

Priority: S

## W26R-E12 — Russell Preliminary-List Revision Shock

2026 Russell US reconstitution publishes preliminary additions/deletions and subsequent public update lists.

Feature:
change in estimated forced flow
between public list vintages.

Priority: S

## W26R-E13 — Russell Lock-Down Certainty Transition

State:
PRE_RANK
RANKED
PRELIMINARY
QUERY/REVISION
LOCKED
EFFECTIVE.

The value of membership uncertainty falls as the process advances.

Priority: A+

## W26R-E14 — Russell 1000/2000 Migration Flow

Estimate net flow for companies crossing large/small-cap membership boundaries, including retention/banding methodology.

Priority: S

## W26R-E15 — Russell Style Reweight Flow

Growth/value assignments can change materially without a broad-index membership change.

Estimate forced flow from:
growth/value fraction change
× assets tracking affected style benchmarks.

Priority: A+

## W26R-E16 — Tracker Asset Base State

Use public index-provider survey data plus ETF/fund sponsor AUM/shares-outstanding where available.

Output:
lower/base/upper estimate of assets requiring benchmark conformity.

Do not pretend all "assets benchmarked" trade exactly like passive funds.

Priority: S methodology/edge hybrid

## W26R-E17 — ETF Creation/Redemption Confirmation

Sponsor pages for major ETFs publish current holdings, AUM and/or shares outstanding.

Research changes in ETF share count/AUM around rebalance events as confirmation of tracker implementation.

Priority: A

## W26R-E18 — Fund-vs-Index Holdings Tracking Gap

Compare ETF holdings/shares to target index weights where point-in-time sponsor data are available.

Feature:
remaining implementation gap before effective close.

Priority: A+

## W26R-E19 — Auction Imbalance Amplification

Fuse estimated benchmark flow with official exchange closing-auction imbalance feeds where licensed/publicly available.

Question:
does benchmark-flow estimate add information beyond auction imbalance itself?

Priority: S

## W26R-E20 — Rebalance Crowding / Pre-Positioning Saturation

Measure:
pre-effective abnormal return
× abnormal volume
× borrow/short state
× estimated forced flow.

Hypothesis:
heavily pre-positioned additions may have less remaining close pressure and more post-close reversal.

Priority: A+

## W26R-E21 — Rebalance Post-Close Reversal Hazard

Estimate probability/magnitude of reversal after implementation from:
forced-flow ratio,
pre-positioning,
auction impact,
event uncertainty,
fundamental news contamination.

Priority: S-

## W26R-E22 — Index-Flow Cross-Impact on ES/NQ

Aggregate constituent-level forced flow into:
S&P 500 net notional
Nasdaq-100 net notional
sector/mega-cap concentration.

Question:
does concentrated constituent rebalance pressure create measurable closing/futures basis effects in ES/NQ?

Priority: S

## W26R-E23 — CME Equity Futures Roll Migration

Primary source:
CME equity-index roll calendar plus daily volume/open interest.

CME states the customary roll date for U.S. equity-index futures is the Monday before the third Friday expiration.

Build:
nearby OI decay
deferred OI growth
calendar-spread volume
roll completion ratio.

Priority: S-

## W26R-E24 — Abnormal Futures Roll Timing

Compare current ES/NQ roll progression against historical normal curve.

Feature:
early/late roll concentration
× basis/calendar spread.

Potential interpretation:
funding/carry or operational positioning pressure.

Priority: A

## W26R-E25 — Futures Roll × Cash Rebalance Collision

When benchmark reconstitution and quarterly futures roll/expiration overlap:
estimate simultaneous demand on:
cash close,
calendar spreads,
basis arbitrage,
dealer balance sheet.

Priority: S

## W26R-E26 — Special Opening Quotation Expiry State

CME quarterly equity-index futures/options final settlement uses Special Opening Quotations based on component opening prices.

Research:
component opening delay
× SOQ sensitivity
× expiry open flow.

Priority: A+

## W26R-E27 — Opening-Print Concentration Risk

A few high-weight components with delayed/abnormal opening auctions can disproportionately affect NDX/SPX-style settlement values.

Map:
component weight
× opening auction anomaly
× SOQ inclusion clock.

Priority: A

## W26R-E28 — OCC Exercise-by-Exception Mechanical State

OCC expiration processing uses exercise-by-exception rules and can alter/disable automatic exercise for special situations such as halted underlyings.

Track:
normal ex-by-ex
accelerated expiration
manual-exercise-only
adjusted deliverable.

Priority: A+

## W26R-E29 — Options Expiry Assignment Flow Envelope

Estimate a range, not a point forecast, for potential underlying stock delivery from expiring options using public OI, moneyness and exercise rules.

Unknown holder intent means uncertainty bands are mandatory.

Priority: A

## W26R-E30 — Halted-Underlying Expiry Discontinuity

When OCC removes halted securities from automatic exercise:
the normal mechanical exercise process changes abruptly.

Research:
impact on reopening/settlement/liquidity after halt resolution.

Priority: B+

## W26R-E31 — Mechanical Flow Collision Calendar

Combine known clocks:
index additions/deletions
index weight changes
Russell/Nasdaq rebalances
futures roll/expiry
options expiry
ETF rebalance.

Output:
aggregate expected mechanical turnover by security/index/time.

Priority: S

## W26R-E32 — Forced Flow / Adaptive Liquidity Quotient

General form:

FFALQ =
mechanically required net flow
/
adaptive liquidity capacity.

Liquidity capacity:
continuous depth
+ close auction depth
+ market-maker capacity
+ cross-venue liquidity
+ futures/ETF arbitrage capacity.

Priority: S

## Highest-priority W26R tests

1. W26R-E03 Closing-Auction Forced-Flow Ratio
2. W26R-E04 Migrating vs Non-Migrating Index Change
3. W26R-E07 Nasdaq-100 Quarterly Rank-Removal Pressure
4. W26R-E09 Nasdaq-100 Weight-Cap Redistribution
5. W26R-E12 Russell Preliminary-List Revision Shock
6. W26R-E14 Russell 1000/2000 Migration Flow
7. W26R-E19 Auction Imbalance Amplification
8. W26R-E22 Index-Flow Cross-Impact on ES/NQ
9. W26R-E25 Futures Roll × Cash Rebalance Collision
10. W26R-E32 Forced Flow / Adaptive Liquidity Quotient
