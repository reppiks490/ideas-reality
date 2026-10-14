# Wave 70B — Globex Order-Book Microstructure (ES/NQ/GC/ZN/CL)

Namespace: **W70B**

Thesis: CME Globex is a central-limit-order-book venue whose MDP 3.0 feed exposes enough structure (match events, implied book, MBO order priority and display quantity, trade-summary aggressor side) to turn microstructure into computable, falsifiable state variables for ES, NQ, GC, ZN and CL. The value for an intraday multi-asset system is in execution-quality and risk-gate state (queue position, fill-before-move probability, iceberg inference, sweep/resilience, protection-order envelopes, price-limit hazard), not in a claim that any signal earns money.

Boundary: W27V owns equity-security LULD, Rule 201 and reopen mechanics (W70B extends only the futures price-limit analog in E35-E37); W17P owns venue/system status vectors; W63M/W12 own CME performance-bond changes; W26R owns index rebalance flows; W49P owns delivery mechanics; W62C owns CFTC positioning. W70B owns exchange-level order-book structure, order-type mechanics, timestamp contracts and book-state estimators. W78B (execution quality and TCA) consumes these state variables.

All candidates are research hypotheses only. Claude owns later implementation. No profitability is claimed; every candidate must pass the vault's intermediate-outcome promotion gate (source predicts an intermediate microstructure/cost outcome before any return claim) and must beat its named negative control.

## W70B-E01 — Match-Event Commit Boundary Book

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: MDP 3.0 packs the book, trade, statistic and implied updates of one Globex event into several messages; MatchEventIndicator (tag 5799) bit 7 marks the last message of the event, bit 4 the last implied quote, bit 0 the last trade summary. Features computed mid-event see transient crossed or half-updated books.

Features: Commit state only when bit7=1. Compare imbalance I=(Qb-Qa)/(Qb+Qa) and spread computed per-message vs per-event; metric = fraction of messages where per-message state differs in sign of I or has spread<=0.

Target: Next-event mid change, fill-probability calibration error.

Falsify-if: Per-message features give equal or better out-of-sample calibration than per-event features, or the mid-event discrepancy rate is <0.1% on ES/NQ.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: S-

## W70B-E02 — Gateway Send-Delay Staleness Gate

Primary source: CME MDP 3.0 SBE Technical Headers page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457638617/MDP+3.0+-+SBE+Technical+Headers (W70B-D11) + CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: TransactTime (tag 60) is start of event processing; the packet header SendingTime is gateway transmission time (documented as microsecond-synced). Delta d=SendingTime-TransactTime measures engine-to-gateway delay inside CME; ts_recv-SendingTime measures network+capture.

Features: d_event, rolling p50/p99 of d per instrument, burst flag if p99 > k*median. Separate our capture delay from exchange-side delay.

Target: Adverse-fill rate of passive orders, signal decay when d is large.

Falsify-if: d is flat (p99/p50 < 1.5 all session) or d carries no information about subsequent quote staleness beyond event-rate.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W70B-E03 — RptSeq Gap Book-Uncertainty Flag

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: RptSeq (tag 83) is a per-instrument entry sequence; the conflated TCP feed sends RptSeq=0. A gap on the incremental UDP feed means the reconstructed book is wrong until snapshot recovery. Trading on a broken book is an operational loss mechanism.

Features: gap_flag, time_since_last_snapshot, book_checksum_vs_snapshot_diff (ticks of qty). Gate: no passive quoting while flag set.

Target: Slippage and reject rate in flagged vs unflagged minutes.

Falsify-if: Flagged intervals show no excess misestimation of L1 qty vs snapshot (Cohen d<0.2) so the gate only costs opportunity.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W70B-E04 — Entries-Per-Event Burst Intensity

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: NoMDEntries per event and events per second proxy a multi-level sweep, spread-implied cascade or cancel wave; burst size is a state variable distinct from trade count.

Features: n_entries_event, price levels touched per event, ratio of delete to new actions (MDUpdateAction 2 vs 0).

Target: Next-5s realized variance and spread widening.

Falsify-if: After controlling for event rate and trade volume the burst measure has no incremental predictive power for realized variance (nested-model F-test).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W70B-E05 — Implied-Share Of Top-Of-Book Depth

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: MDEntryType E/F (implied bid/offer) are generated by Globex from outright and spread books. Their share of L1 depth varies by instrument and expiry window and is a different liquidity source than customer orders; trade summary entries require at least one real order.

Features: implied_share_L1 = Q_implied/(Q_implied+Q_real) per side; also at L2-L5. Sign-ambiguous: high share may mean thin outright book (bad) or deep spread book (good).

Target: Post-touch refill speed and realized slippage of marketable orders.

Falsify-if: implied_share_L1 has no association with slippage after conditioning on total L1 depth, in ES front month or NQ front month.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W70B-E06 — Implied Quote Flicker Rate

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: Implied quotes update whenever any linked leg changes; high implied update-to-cancel rates without trades signal unreliable depth.

Features: flicker = implied_deletes_per_sec / (implied_deletes+implied_trades); real_flicker analog for customer orders.

Target: Probability that displayed L1 qty is gone before our order arrives (queue_loss).

Falsify-if: Implied flicker adds nothing to queue_loss prediction beyond real-order flicker.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W70B-E07 — Trade-Summary NumberOfOrders Participation Count

Primary source: CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02)

Mechanism: NumberOfOrders (tag 346) in the Trade Summary = number of real orders participating in a match step. Counts resting-order fragmentation consumed per aggressor.

Features: orders_per_step, qty_per_order = qty/NumberOfOrders; low qty_per_order = retail/fragmented depth consumed.

Target: Post-trade 1-5s drift and refill ratio.

Falsify-if: orders_per_step does not differ across informed vs uninformed markout buckets (placebo: shuffle within hour).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W70B-E08 — No-Aggressor Trade Exclusion Mask

Primary source: CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02)

Mechanism: AggressorSide (tag 5797) = 0 (none) at market open, after Pre-Open or Pause, and when customer orders trade against Globex-generated implied orders. Such prints are not signed order flow and contaminate OFI/VPIN if forced to a sign.

Features: mask_noaggr; compute signed-volume imbalance twice (with and without mask); report sign flips.

Target: Error of signed-volume estimators vs next-interval return.

Falsify-if: Including no-aggressor prints (signed by tick rule) improves predictive R2 by >=5% rel in both ES and NQ OOS.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W70B-E09 — MBO Exact Queue-Ahead Reconstruction

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: MBOFD entries carry OrderID, MDOrderPriority and MDDisplayQty with New/Change/Delete actions. Queue ahead of any resting order is computable exactly (display qty only), unlike MBP-only inference.

Features: Q_ahead(order)=sum MDDisplayQty of orders with better MDOrderPriority at same price; track under Change actions that lose priority.

Target: Fill-time prediction error vs MBP-only queue estimates.

Falsify-if: MBO-exact queue improves time-to-fill log-likelihood by <1% over MBP-only proxy on ES L1.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: S-

## W70B-E10 — Executed-Beyond-Display Iceberg Detector

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01) + CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02)

Mechanism: MDDisplayQty is the visible quantity; orders may have additional hidden display quantity (reserve). If cumulative executed quantity against an OrderID at a price exceeds its displayed quantity without a new order, hidden reserve exists. Aggregate-level inference only; no identity.

Features: hidden_est(price)=max(0, executed_total - displayed_at_first_sight) per OrderID; replenish_count; replenish_latency.

Target: Probability price holds at level through next k trades.

Falsify-if: Levels flagged with hidden_est>0 break at the same rate as matched placebo levels (same size, time-of-day).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A+

## W70B-E11 — Reserve Refill Priority Rule Probe

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: Whether a refill of a replenished iceberg order keeps or loses time priority determines how much queue ahead of us is real. Rule details are UNVERIFIED here; MDOrderPriority transitions in MBOFD data can reveal them empirically.

Features: On detected refills, record MDOrderPriority before/after; fraction with priority reset.

Target: Corrected Q_ahead and fill-time prediction.

Falsify-if: Priority never changes on refill (then queue models need no correction) or the refill sample is too small (<500 events) to resolve it.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W70B-E12 — Iceberg Exhaustion Breakout

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01) + CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02) + Bessembinder, Panayides, Venkataraman, Hidden liquidity, JFE 94(3):361-383; Frey, Sandas, CFR Cologne WP 09-06 (W70B-D17)

Mechanism: A level defended by repeated refills absorbs aggressive flow; once reserve is exhausted the level may fail fast because the defender no longer supports it. Equity evidence (hidden liquidity lowers shortfall but fills less) is by analogy only.

Features: refills at level, absorbed_qty, time_since_last_refill; trigger when absorbed_qty>x and refill gap>y.

Target: Next 30s signed move through the level.

Falsify-if: Post-exhaustion continuation does not exceed placebo levels with equal absorbed volume (paired test).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W70B-E13 — Defended-Level Support Persistence

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01) + Bessembinder, Panayides, Venkataraman, Hidden liquidity, JFE 94(3):361-383; Frey, Sandas, CFR Cologne WP 09-06 (W70B-D17)

Mechanism: Levels with repeated refills attract reversals if the defender is passive liquidity provision; but their persistence is confounded with round-number effects.

Features: defended_flag(price,side); distance of mid to defended level in ticks; round-number control.

Target: P(reversal at level) minus round-number placebo.

Falsify-if: Defended levels have no higher reversal rate than non-round non-defended placebo levels.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W70B-E14 — Algorithmic Slicing Fingerprint (Aggregate)

Primary source: CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02)

Mechanism: Repeated same-sign aggressive prints of near-constant size at regular intervals indicate scheduled slicing. Fingerprint is an aggregate flow-pattern, never an identity.

Features: autocorrelation of trade size and inter-arrival at lag1..5 within signed runs; run_length with CV(size)<c and CV(dt)<c.

Target: Signed continuation over next minute.

Falsify-if: Fingerprint-positive runs have continuation equal to size-matched random runs.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W70B-E15 — Round-Lot Display Size Clustering

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: Display quantities cluster on round lots (1, 5, 10, 25, 50, 100). Share of round-lot orders vs odd-lot orders at touch is a participant-mix proxy, not an identity.

Features: round_share_touch per side; entropy of display sizes.

Target: Short-horizon adverse selection (markout) of passive fills.

Falsify-if: Round-lot share carries no markout information after controlling for spread and imbalance.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B

## W70B-E16 — Queue-Reactive Intensity Surface

Primary source: Huang, Lehalle, Rosenbaum, The queue-reactive model, arXiv:1312.0563 (W70B-D12)

Mechanism: Arrival, cancel and market-order intensities depend on the size of the queue at the touch; estimating lambda(q) per instrument gives fill and move probabilities without ad hoc assumptions.

Features: Estimate lambda_add(q), lambda_cancel(q), lambda_mkt(q) in event time from MBO; predict P(touch depletion before replenishment).

Target: Hazard of mid move and queue depletion.

Falsify-if: Constant-intensity model matches OOS depletion-time distribution within KS tolerance (no q-dependence).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: S-

## W70B-E17 — Queue-Position Value Surface

Primary source: Moallemi, Yuan, A model for queue position valuation in a limit order book (Columbia GSB working paper, 2017) (W70B-D14)

Mechanism: An order's value depends on queue position through spread capture versus adverse selection costs; values scale with half-spread in the cited work. Dynamic value surface V(q_ahead,Q_total,I).

Features: V = P(fill)*(half_spread - E[adverse|fill, q]) - (1-P(fill))*E[chase|no fill].

Target: Realized per-order PnL net of markout.

Falsify-if: Realized value is flat in q_ahead after controlling for fill probability.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A+

## W70B-E18 — Fill-Before-Move Probability

Primary source: Huang, Lehalle, Rosenbaum, The queue-reactive model, arXiv:1312.0563 (W70B-D12) + Moallemi, Yuan, A model for queue position valuation in a limit order book (Columbia GSB working paper, 2017) (W70B-D14)

Mechanism: P(filled before the opposite touch depletes, i.e., before price moves against) is the key control variable for passive entries.

Features: p_fbm = F(q_ahead/trade_rate, opposite_depth, I, vol). Calibrate with isotonic regression.

Target: Binary outcome: fill happens before adverse tick.

Falsify-if: Calibration slope outside [0.8,1.2] OOS in two consecutive quarters, or no AUC gain over q_ahead alone.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: S-

## W70B-E19 — Cancel-Ahead Decay Ratio

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: Queue ahead shrinks by cancels as well as trades; ratio cancel/trade of queue ahead of a position predicts time to fill and signals info.

Features: decay_ratio = cancelled_ahead / (cancelled_ahead+executed_ahead) over last 10s.

Target: Time-to-front and fill-conditional markout.

Falsify-if: decay_ratio has no relation to fill-conditional markout after controlling for imbalance.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W70B-E20 — Back-Of-Queue Toxic Fill

Primary source: Moallemi, Yuan, A model for queue position valuation in a limit order book (Columbia GSB working paper, 2017) (W70B-D14) + Lehalle, Mounjid, Limit order strategic placement with adverse selection risk and the role of latency, arXiv:1610.00261 (W70B-D12)

Mechanism: A fill at the back of a queue happens mostly when the level is being consumed through, i.e., when price is about to move through; front fills are earned by being early.

Features: fill_rank_fraction = q_ahead_at_post / Q_total_at_fill; markout(1s,5s) by decile.

Target: Markout curve slope by queue rank.

Falsify-if: Markout is not monotone in fill_rank_fraction (Spearman |rho|<0.05) in both ES and NQ.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W70B-E21 — Time-To-Front Distribution

Primary source: Huang, Lehalle, Rosenbaum, The queue-reactive model, arXiv:1312.0563 (W70B-D12)

Mechanism: Expected time to reach the front = q_ahead/(trade_rate + cancel_rate). Heavy tails matter: median is misleading.

Features: Quantile regression of TTF on q_ahead, trade rate, time-of-day.

Target: Quantiles of time to first fill.

Falsify-if: Simple ratio formula matches empirical TTF 90th percentile within 25% (then regression adds nothing).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W70B-E22 — Implicit-Spread Large-Tick Regime

Primary source: Dayri, Rosenbaum, Large tick assets: implicit spread and optimal tick size, arXiv:1207.6325 (W70B-D12) + CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W70B-D06) + CME contract specs ZN/CL/GC pages (https://cmegroup.com/trading/interest-rates/us-treasury/10-year-us-treasury-note_contractSpecs_futures.html, https://cmegroup.com/trading/energy/crude-oil/light-sweet-crude_contractSpecs_futures.html, https://cmegroup.com/trading/metals/precious/gold_contractSpecs_futures) (W70B-D18)

Mechanism: Large-tick assets (spread mostly 1 tick) have an implicit spread, and queue imbalance is more informative than in small-tick assets. ES, NQ tick 0.25; GC 0.10; ZN 1/64 (0.5/32); CL 0.01. Which are large-tick varies by state.

Features: tick_ratio = tick / (sigma_1min); P(spread==1 tick) in rolling hour; imbalance predictive slope.

Target: Imbalance coefficient in mid-change regression by tick regime.

Falsify-if: Imbalance slope is statistically equal across large-tick and small-tick states in the same instrument.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W70B-E23 — Micro-Price Versus Mid Entry Reference

Primary source: Stoikov, The micro-price, Quantitative Finance 18(12):1959-1966, DOI 10.1080/14697688.2018.1489139 (W70B-D13)

Mechanism: Micro-price is a martingale estimator combining spread and imbalance; it is claimed to beat mid and weighted mid. A third-party thesis found no improvement at most horizons, so the claim is contested. Test both.

Features: mp = mid + g(I,spread) fitted from Markov chain; compare MSE of future mid prediction at 0.1,1,5s.

Target: Future mid-price forecast MSE.

Falsify-if: mp MSE is not lower than mid or weighted mid on OOS for ES and NQ at any horizon.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W70B-E24 — Multi-Level Integrated OFI Depth Slope

Primary source: Cont, Kukanov, Stoikov, The Price Impact of Order Book Events, arXiv:1011.6402 (W70B-D12) + Eisler, Bouchaud, Kockelkoren, The price impact of order book events, arXiv:0904.0900 (W70B-D12)

Mechanism: Order-flow imbalance over book events explains contemporaneous mid changes linearly with slope inversely proportional to depth. Slope estimates are a live depth/impact gauge.

Features: OFI over 1s..10s; beta_t=dMid/OFI rolling; use 1/beta as depth proxy.

Target: Contemporaneous mid change; slope as impact predictor for our slippage.

Falsify-if: Rolling beta does not predict realized taker slippage out-of-sample.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W70B-E25 — Cross-Instrument OFI Lead-Lag (ES NQ ZN)

Primary source: Cont, Kukanov, Stoikov, The Price Impact of Order Book Events, arXiv:1011.6402 (W70B-D12) + Lipton, Pesavento, Sotiropoulos, Trade arrival dynamics and quote imbalance in a limit order book, arXiv:1312.0514 (W70B-D12)

Mechanism: OFI in one liquid futures contract may predict mid changes in a correlated one inside seconds (arbitrage lag). Futures cross-impact is an extension of cited equity-style work and is UNVERIFIED for CME.

Features: OFI_ES(t-τ) -> dMid_NQ(t), τ in 10ms..5s, with ZN->ES for rates-equity channel; require event-time alignment per W70B-E47.

Target: Incremental R2 of lagged cross-OFI.

Falsify-if: Lagged cross-OFI coefficient is zero after own OFI and own-lag controls, or vanishes at our measured information age.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W70B-E26 — Strategy-Pair Self-Match Exposure Monitor

Primary source: CME Globex Self-Match Prevention FAQ, https://cmegroup.com/globex/trade-on-cme-globex/self-match-faq.html (W70B-D04) + CME Market Regulation Advisory RA1614-5 (Rule 534 wash trades), https://www.cmegroup.com/tools-information/lookups/advisories/market-regulation/ra1614-5.html (W70B-D05)

Mechanism: Rule 534 treats entering orders known to match same-beneficial-owner orders as wash trading; incidental unintentional matches are generally tolerated, but frequent or market-moving self-matching draws scrutiny. SMP blocks matches of orders with the same SMP ID. A multi-strategy system on one account risks opposite-side orders crossing.

Features: own_cross_prob = P(strategy A resting order within 0 ticks of strategy B opposite aggressive order); count unsolicited SMP cancels; compliance score.

Target: Compliance gating, not alpha: expected number of potential self-matches per day.

Falsify-if: Zero potential self-cross events in 60 days of shadow logs (then gate is unneeded) -- otherwise gate must remain.

Horizon: INTRADAY
Availability: PUBLIC_SCHEDULED
Priority: A

## W70B-E27 — SMP Activation-Window Config Risk

Primary source: CME Globex Self-Match Prevention FAQ, https://cmegroup.com/globex/trade-on-cme-globex/self-match-faq.html (W70B-D04)

Mechanism: SMP ID changes activate at 16:30 CT Mon-Thu and 09:30 CT Sunday; orders with new or modified IDs before activation are rejected. Configuration changes inside the wrong window cause rejects exactly when positions need management.

Features: calendar gate: freeze SMP config changes outside windows; reject-rate by config-change timestamp.

Target: Reject count after config change.

Falsify-if: No rejects observed on config changes made outside activation windows in test.

Horizon: DAILY
Availability: PUBLIC_SCHEDULED
Priority: B

## W70B-E28 — Pre-Open Self-Match Gap

Primary source: CME Globex Self-Match Prevention FAQ, https://cmegroup.com/globex/trade-on-cme-globex/self-match-faq.html (W70B-D04)

Mechanism: A 2016 advisory (cited in secondary summary) says SMP does not prevent self-matches at the opening when orders are entered in Pre-Open. Opposite-side orders from separate strategies are unsafe pre-open.

Features: Gate: at most one side working per instrument during Pre-Open; own-order opposite pair detector.

Target: Potential self-match count at open.

Falsify-if: Original advisory text, once fetched, contradicts the summarized gap (PROVENANCE_PENDING).

Horizon: INTRADAY
Availability: PUBLIC_SCHEDULED
Priority: B

## W70B-E29 — Messaging Efficiency Budget State

Primary source: CME Globex Messaging Efficiency Program, https://cmegroup.com/globex/trade-on-cme-globex/messaging-efficiency-program.html (W70B-D09)

Mechanism: MEP scores message counts by predefined weights versus executed volume against product-group benchmarks; unsolicited SMP cancels carry a weight of 3 per the FAQ. A reprice-heavy passive strategy consumes budget. Benchmarks and weights for new orders are not retrieved.

Features: msg_score_day = sum w_k * msgs_k; ratio_to_volume by product group; budget fraction used. Benchmarks PROVENANCE_PENDING (MEP v11.6 doc unopened).

Target: Throttle state: probability we reach surcharge/threshold intraday.

Falsify-if: Measured ratio stays below 10% of the published benchmark for all products so the budget is never binding.

Horizon: DAILY
Availability: PUBLIC_SCHEDULED
Priority: B+

## W70B-E30 — Treasury Roll Message-Ratio Constraint

Primary source: CME Globex Messaging Efficiency Program, https://cmegroup.com/globex/trade-on-cme-globex/messaging-efficiency-program.html (W70B-D09)

Mechanism: Secondary reports state a 3,000:1 order-entry-quantity-to-executed-volume benchmark for 5- and 10-year Note futures in the last 10 trade dates before First Notice Day, for firms above 5 million contracts of daily order entry, with a possible $10,000 daily surcharge. Applicability to a small account is doubtful (threshold is firm-size dependent).

Features: roll_ratio = order_entry_qty / executed_qty during ZN roll window; flag if >0.5*3000 when above size threshold.

Target: Surcharge risk; constraint on ZN quoting behavior.

Falsify-if: Primary CME notice, when fetched, shows thresholds not applicable to our size; then edge is downgraded to B.

Horizon: DAILY
Availability: PUBLIC_SCHEDULED
Priority: B

## W70B-E31 — Stop-With-Protection Fill Envelope

Primary source: CME iLink Order Types page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227032/iLink+Order+Types (W70B-D03) + CME Rule 588.H Globex Non-Reviewable Trading Ranges notices (SER-8164, https://www.cmegroup.com/notices/ser/2018/06/SER-8164.html) (W70B-D08)

Mechanism: A stop-with-protection triggers when the market trades at/through the trigger, then becomes a market order with protection price limit = best price +/- protection points; unfilled remainder rests as a limit order at the protection limit. Protection points are described by CME developer text as typically 50% of the Non-Reviewable Range.

Features: Slippage distribution truncated at PP; P(partial fill) = P(depth within PP < size); resting remainder risk.

Target: Exit slippage and fraction of unfilled stops at trigger+5s.

Falsify-if: Observed fill price exceeds trigger+PP (violates envelope) in any logged stop, or P(partial) is zero for all sizes tested.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A+

## W70B-E32 — Market-With-Protection Rejection State

Primary source: CME iLink Order Types page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227032/iLink+Order+Types (W70B-D03)

Mechanism: Market orders with protection are rejected when no opposing bid/offer is working and in any market state except Open. In Pre-Open, Pause or no-opposing-quote moments the planned market exit does not exist.

Features: state_at_submit; opposing_quote_exists; fallback_path success rate.

Target: Exit failure probability and delay.

Falsify-if: No MWP rejects in 90 days of live-or-sim logs, including the Pause cases.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W70B-E33 — Stop Cluster Run Signature

Primary source: CME iLink Order Types page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227032/iLink+Order+Types (W70B-D03) + CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02)

Mechanism: Stop orders with common trigger levels activate as one burst when the level trades, creating a trade burst with large NumberOfOrders and rapid level consumption. Whether the subsequent drift reverses is untested.

Features: burst = events>=n at same aggressor within 200ms right after round/prior-extreme level touch; reversal_ratio over 1,5 min.

Target: Post-burst signed return versus placebo levels.

Falsify-if: Post-burst reversal/continuation equals placebo (matched volume, time-of-day) at 5% level after multiplicity control.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W70B-E34 — Implied-Print Stop Trigger Asymmetry

Primary source: CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02) + CME iLink Order Types page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227032/iLink+Order+Types (W70B-D03)

Mechanism: Trade Summary prints are issued only when at least one real order participates; prints involving implied orders with no real aggressor have AggressorSide 0. Stops trigger on trades; the trigger event type matters.

Features: stop_trigger_type = real_aggressor vs implied-involved; share by instrument.

Target: Stop slippage difference by trigger type.

Falsify-if: Slippage distributions of the two trigger types are identical (two-sample KS p>0.1).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B

## W70B-E35 — Futures Price-Limit Proximity Hazard

Primary source: CME S&P 500 Price Limits FAQ, https://www.cmegroup.com/trading/equity-index/sp-500-price-limits-faq.html (W70B-D07) + CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W70B-D06)

Mechanism: ES overnight has a 7% limit from the reference price (previous day VWAP 14:59:30-15:00 CT) and a 3.5%/hour dynamic circuit breaker with 2-minute pause per CME FAQ; during US hours 7/13/20% moves are tied to NYSE Rule 7.12 rather than CME self-halting. Distance to limit changes behavior near the boundary; extends W27V-E01 (equity LULD distance) to futures.

Features: dist_to_limit_pct, dist_to_dynamic_breaker, time since breaker reset; hazard of pause vs distance.

Target: P(pause or limit state in next 10 min).

Falsify-if: Within 1% of the limit the pause hazard is no different from base rate; also the CME FAQ values change (versioning risk).

Horizon: INTRADAY
Availability: PUBLIC_SCHEDULED
Priority: A

## W70B-E36 — Dynamic Circuit Breaker Pause Reopen Path

Primary source: CME S&P 500 Price Limits FAQ, https://www.cmegroup.com/trading/equity-index/sp-500-price-limits-faq.html (W70B-D07)

Mechanism: A 2-minute pause on a 3.5%/hour move changes liquidity provision before and after. Reopen behavior (spread, depth, aggressor=0 prints at reopen) shapes slippage.

Features: pre-pause 60s volatility, reopen spread/depth ratio vs baseline, first-trade aggressor flag.

Target: Reopen slippage for market-type orders; time to restore baseline depth.

Falsify-if: Depth/spread at 60s post-reopen equal pre-pause baseline (no residual impairment).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W70B-E37 — Cash-Halt Futures Price-Discovery Share

Primary source: CME S&P 500 Price Limits FAQ, https://www.cmegroup.com/trading/equity-index/sp-500-price-limits-faq.html (W70B-D07)

Mechanism: CME states futures do not halt on their own at 7/13/20% moves unless NYSE Rule 7.12 is triggered; if cash halts, ES/NQ remain the live price venue. Interaction with W27V-E05/E06 (halted constituents).

Features: cash_halt flag from NYSE/Nasdaq halts (W17P-E13), futures volume share, spread.

Target: Futures depth/volatility during cash halt.

Falsify-if: Futures spread and depth during cash halts are no different from matched non-halt minutes.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W70B-E38 — Non-Reviewable Range Table Version Shift

Primary source: CME Rule 588.H Globex Non-Reviewable Trading Ranges notices (SER-8164, https://www.cmegroup.com/notices/ser/2018/06/SER-8164.html) (W70B-D08)

Mechanism: Rule 588.H NRR table amendments (SER-8164 in 2018; a 2026 CFTC filing 26-444 dated 2026-09-25 is reported by search excerpt, URL mapping UNVERIFIED) change the range protecting trades from review/bust and thus the stop/MWP protection points. Parameter must be versioned.

Features: NRR_version(instrument,date); PP=0.5*NRR; event study of protected-order slippage around effective dates.

Target: Change in stop/MWP slippage truncation point.

Falsify-if: No change in protection-limited fills around effective dates; or NRR in effect differs from our assumed PP rule.

Horizon: SLOW_PRIOR
Availability: PUBLIC_SCHEDULED
Priority: B+

## W70B-E39 — Market-State At-Submit Gate

Primary source: CME iLink Order Types page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227032/iLink+Order+Types (W70B-D03)

Mechanism: Stops are accepted only in Pre-Open, Open and No Cancel; MWP only in Open; Market-Limit only in Open. A gate on security status prevents impossible orders and defines fallback.

Features: state_at_submit one-hot; order_type_allowed matrix.

Target: Reject rate and time lost.

Falsify-if: No rejects attributable to state in 90 days.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B

## W70B-E40 — Tick-Normalized Cost Ladder

Primary source: CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W70B-D06) + CME contract specs ZN/CL/GC pages (https://cmegroup.com/trading/interest-rates/us-treasury/10-year-us-treasury-note_contractSpecs_futures.html, https://cmegroup.com/trading/energy/crude-oil/light-sweet-crude_contractSpecs_futures.html, https://cmegroup.com/trading/metals/precious/gold_contractSpecs_futures) (W70B-D18)

Mechanism: Tick values: ES 0.25 pt = $12.50; ZN 1/64 pt = $15.625; CL $0.01 = $10; GC $0.10 = $10 (CME specs). Costs compared in ticks and in 1-minute sigma units normalize cross-asset execution.

Features: cost_ticks, cost_sigma=cost_ticks*tick/sigma_1min, cross-asset ranking.

Target: Cross-asset slippage ranking stability.

Falsify-if: Rankings in ticks and in sigma units agree on all days (then normalization adds nothing).

Horizon: DAILY
Availability: PUBLIC_SCHEDULED
Priority: B+

## W70B-E41 — Calendar-Spread Tick And Implied Depth Link

Primary source: CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W70B-D06) + CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: ES calendar spread minimum fluctuation is 0.05 index points (spec) so spread books are finer than outrights, generating implied outright quotes; spread liquidity can feed outright depth.

Features: spread_book_depth; fraction of outright L1 derived from spreads (see E05); spread tick-relative width.

Target: Outright refill speed in roll week.

Falsify-if: Outright refill speed is independent of spread-book depth.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W70B-E42 — ZN Half-32nd Grid Depth Concentration

Primary source: CME contract specs ZN/CL/GC pages (https://cmegroup.com/trading/interest-rates/us-treasury/10-year-us-treasury-note_contractSpecs_futures.html, https://cmegroup.com/trading/energy/crude-oil/light-sweet-crude_contractSpecs_futures.html, https://cmegroup.com/trading/metals/precious/gold_contractSpecs_futures) (W70B-D18)

Mechanism: ZN outrights tick at 1/64 (half of a 32nd) but depth may concentrate on 1/32 multiples. If true, quoting on odd 1/64 ticks inserts into thin queues with different fill/adverse profile.

Features: depth_share on odd vs even 1/64 ticks; fill-markout by tick parity.

Target: Fill probability and markout by parity.

Falsify-if: Depth and markout independent of tick parity.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B

## W70B-E43 — Round-Number Depth And Stop Magnetism

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01) + CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02)

Mechanism: Resting depth and executed volume cluster on round prices (ES whole/half points, CL .00/.50, GC whole dollars). Attraction and stop clusters make touches different from interior ticks.

Features: round_flag(price, modulus per instrument); volume share vs uniform; touch outcomes.

Target: Touch-reversal probability and slippage at round levels.

Falsify-if: Volume/depth uniform across tick residues mod round step after intraday price-range control.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W70B-E44 — Spread-In-Ticks Regime Switch

Primary source: Dayri, Rosenbaum, Large tick assets: implicit spread and optimal tick size, arXiv:1207.6325 (W70B-D12)

Mechanism: Spread in ticks (1 vs >=2) separates states where passive posting adds a tick of edge versus states where queue priority is the only edge. Spread widening to 2+ ticks is itself a stress flag.

Features: spread_ticks; fraction of time >=2 over 5 min; transition matrix.

Target: Slippage and markout conditional on regime.

Falsify-if: Passive fill markout identical across spread=1 and spread>=2 regimes.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W70B-E45 — Settlement-Window Reference Price Microstructure

Primary source: CME S&P 500 Price Limits FAQ, https://www.cmegroup.com/trading/equity-index/sp-500-price-limits-faq.html (W70B-D07) + CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W70B-D06)

Mechanism: Price-limit reference for ES is previous day VWAP of lead month 14:59:30-15:00 CT. The 30s window concentrates volume and may distort touches; limit levels for next session are mechanically set there.

Features: window_volume_share, spread vs prior minute, signed imbalance in window, next-day limit levels.

Target: Window slippage and its predictive power for next session opening gap.

Falsify-if: Window liquidity indistinguishable from adjacent 30s segments.

Horizon: DAILY
Availability: PAID_REALTIME
Priority: B

## W70B-E46 — Information-Age Decomposition

Primary source: CME MDP 3.0 SBE Technical Headers page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457638617/MDP+3.0+-+SBE+Technical+Headers (W70B-D11) + Databento GLBX.MDP3 dataset documentation, https://databento.com/docs/venues-and-datasets/glbx-mdp3 (W70B-D10)

Mechanism: Decision uses data age A = (ts_recv - SendingTime) + (SendingTime - TransactTime) + compute time; signals whose half-life is below A carry no executable value. Databento maps TransactTime to ts_event and SendingTime to ts_in_delta.

Features: A distribution per session; signal half-life tau from autocorr; usable_fraction=P(A<tau/3).

Target: Executable fraction of each signal.

Falsify-if: Signal PnL gross is the same for artificially delayed replays up to 5*A (then latency does not matter).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W70B-E47 — Cross-Instrument Event Atomicity

Primary source: Databento GLBX.MDP3 dataset documentation, https://databento.com/docs/venues-and-datasets/glbx-mdp3 (W70B-D10) + CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: CME sets the end-of-event flag on one message even when the event spans multiple instruments; per-instrument reconstruction therefore needs a synthetic last-record flag. Spread and leg events are atomic across instruments.

Features: group messages by TransactTime and event-id; detect spread-leg events; avoid cross-instrument lead-lag claims within one atomic event.

Target: Frequency of false lead-lag inside atomic events.

Falsify-if: Lead-lag estimates unchanged when atomic events are excluded.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W70B-E48 — Sub-Microsecond Ordering Ban

Primary source: CME MDP 3.0 SBE Technical Headers page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457638617/MDP+3.0+-+SBE+Technical+Headers (W70B-D11)

Mechanism: SendingTime is synchronized to master clock to microsecond accuracy; ordering of different instruments below that resolution is not established by the feed.

Features: Resolution floor tau_min=1us; count events within floor; exclude from lead-lag.

Target: Lead-lag inference validity.

Falsify-if: Controlled replay with permuted sub-us ordering leaves lead-lag unchanged (then floor is harmless).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B

## W70B-E49 — Market-Data-To-Execution-Report Lag

Primary source: CME MDP 3.0 SBE Technical Headers page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457638617/MDP+3.0+-+SBE+Technical+Headers (W70B-D11) + CME iLink Order Types page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227032/iLink+Order+Types (W70B-D03)

Mechanism: The gap between a trade seen on the feed and our execution report for the same fill (ack lag) measures how much market data leads order state; negative gaps reveal feed ordering anomalies.

Features: lag = ts_exec_report - ts_md_trade for own fills; distribution by session.

Target: Cancel race loss rate.

Falsify-if: Lag has no relation to cancel-race losses (cancels sent after fill).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W70B-E50 — Multi-Level Sweep Event Detector

Primary source: CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02) + CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: A single aggressive order consuming several price levels shows as one event with multiple Trade Summary entries and book deletes. Sweep depth in ticks and consumed quantity versus displayed depth define a liquidity-exhaustion measure.

Features: levels_swept, qty_swept/qty_displayed_prior, refill_time to restore best.

Target: Post-sweep 1-30s drift and refill.

Falsify-if: Sweep-conditional drift and refill equal matched non-sweep large trades.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: S-

## W70B-E51 — Sweep Through Implied Liquidity Share

Primary source: CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02) + CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: When a sweep consumes implied depth, the underlying leg orders are in other books and refill differently from outright depth.

Features: implied_fraction_of_swept_qty; refill by source.

Target: Refill asymmetry between implied and real depth.

Falsify-if: No difference in refill time between implied-heavy and real-heavy sweeps.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B

## W70B-E52 — Native Aggressor Versus Inferred Sign Disagreement

Primary source: CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02) + Easley, Lopez de Prado, O'Hara, Flow toxicity and liquidity in a high-frequency world, RFS 25(5):1457-1493 (W70B-D15)

Mechanism: CME supplies aggressor side directly. Disagreement with tick-rule/BVC signing quantifies noise in VPIN-style indicators built on inferred signs. Critique of bulk classification exists (cited in search summary, UNVERIFIED details).

Features: disagree_rate(minute); VPIN_native vs VPIN_BVC; ranking correlation.

Target: Predictive power of toxicity measures for next-hour volatility.

Falsify-if: VPIN_BVC and VPIN_native give statistically equal predictive R2.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W70B-E53 — Signed-Flow Run Persistence

Primary source: CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02)

Mechanism: Signed order flow is positively autocorrelated in many markets (long memory); run length conditional on size and book state predicts continuation or exhaustion. Bibliography for long memory is not retrieved.

Features: run_length (consecutive same-aggressor events), run_volume, current depth vs run_volume.

Target: Run continuation hazard.

Falsify-if: Hazard of run termination is constant (geometric) in run length.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W70B-E54 — Trade-Through Gap Events In Thin Books

Primary source: CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02) + CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: Trades through the prior best by more than one tick indicate book gaps; CL/GC/ZN overnight are likelier. Gap events restore via refill.

Features: gap_ticks, frequency per hour by session; refill_time.

Target: Slippage tail for market-type orders.

Falsify-if: Tail (p99) slippage of market orders is unrelated to preceding gap-event frequency.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W70B-E55 — Micro Versus E-Mini Flow Share

Primary source: CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W70B-D06) + CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02)

Mechanism: Micro E-mini contracts (listed by CME) may carry different participant mix; share of signed flow in micro vs E-mini and its lead-lag is a participant-composition state. Sign ambiguous.

Features: micro_flow_share, lead-lag of micro OFI vs E-mini mid.

Target: Incremental predictability.

Falsify-if: Micro OFI adds nothing to E-mini mid prediction beyond E-mini OFI.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B

## W70B-E56 — Flash-Crash-Style Liquidity Withdrawal Gate

Primary source: Kirilenko, Kyle, Samadi, Tuzun, The Flash Crash, J. Finance 72(3):967-998 (SSRN 1686004) (W70B-D16)

Mechanism: In the cited E-mini S&P audit-trail study, high-frequency intermediaries did not change trading pattern when prices fell, while a large sell program pressured the book; liquidity withdrawal and aggressive one-sided flow are the mechanism. Gate on one-sided flow sustained against thin depth.

Features: signed_vol_5min/depth_L1..5; dropped depth percentile; spread blowout.

Target: Tail-risk of 1% moves in 5 minutes.

Falsify-if: Gate triggers no more informative than random with equal frequency for 5-min tail moves.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W70B-E57 — Post-Sweep Book Resilience Half-Life

Primary source: Obizhaeva, Wang, Optimal trading strategy and supply/demand dynamics, J. Financial Markets 16(1) (bibliographic detail PROVENANCE_PENDING) (W70B-D20) + Gould et al., Limit Order Books, arXiv:1012.0349 (W70B-D12)

Mechanism: After a depth-consuming trade, depth recovers with a resilience rate; the half-life is a state variable for further slicing and for adverse selection.

Features: fit exp recovery of depth after sweeps: D(t)=D_inf-(D_inf-D0)exp(-t/tau); report tau_median by instrument/time-of-day.

Target: Recovery time; impact of second child order.

Falsify-if: Recovery is not exponential-like (R2<0.3) or tau is unrelated to second-order slippage.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W70B-E58 — Bid-Ask Refill Asymmetry

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01) + Obizhaeva, Wang, Optimal trading strategy and supply/demand dynamics, J. Financial Markets 16(1) (bibliographic detail PROVENANCE_PENDING) (W70B-D20)

Mechanism: Faster refill on one side after a symmetric shock indicates passive liquidity supply preference; asymmetry predicts direction.

Features: tau_bid - tau_ask over last k shocks; signed.

Target: Next-minute return sign.

Falsify-if: Signed asymmetry has zero predictive information relative to placebo labels (sides swapped).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W70B-E59 — Depth Percentile Liquidity Gate

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01)

Mechanism: Depth varies sharply over time (public reports of near-zero S&P e-mini liquidity in March 2020 and a ~90% depth collapse in April 2025 per trade press; UNVERIFIED primary). A rolling-percentile gate on total depth within k ticks controls size.

Features: depth_pctile = rank of sum Q(1..5) vs 20-day same-time-of-day baseline.

Target: Taker slippage and fill rate.

Falsify-if: Slippage is unrelated to depth percentile after controlling for volatility.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A+

## W70B-E60 — Book-Level Cancel-To-Trade Stress Ratio

Primary source: CME MDP 3.0 Market Data Incremental Refresh (MBP and MBOFD) page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227795/MDP+3.0+-+Market+Data+Incremental+Refresh+-+MBP+and+MBOFD (W70B-D01) + CME MDP 3.0 Trade Summary page, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227733/MDP+3.0+-+Market+Data+Incremental+Refresh+-+Trade+Summary (W70B-D02)

Mechanism: Aggregated cancel-to-trade ratio at the book (not participant) shows quote churn: high ratio with falling depth means liquidity is retreating rather than turning over. No identity inference.

Features: ctr_book = deletes/(trades) per 10s per level; deviation vs time-of-day baseline.

Target: Spread widening in next minute.

Falsify-if: ctr_book has no incremental information over event rate and volatility.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W70B-E61 — Disruptive-Pattern Compliance Guard

Primary source: CME Rulebook Rule 575 Disruptive Practices Prohibited (exact text not retrieved; PROVENANCE_PENDING) (W70B-D19) + CME Market Regulation Advisory RA1614-5 (Rule 534 wash trades), https://www.cmegroup.com/tools-information/lookups/advisories/market-regulation/ra1614-5.html (W70B-D05)

Mechanism: Rule 575 prohibits disruptive practices; exact elements not retrieved. Our own order lifecycle (fast cancel after placement, layering-like multi-level placement, opposite pair behavior) should be monitored against conservative internal thresholds to avoid even unintentional patterns.

Features: own_order_lifetime distribution; cancel_fraction; multi-level same-side placements count; opposite-side within-window pairs. Thresholds internal, to be set after reading Rule 575.

Target: Compliance score; not alpha.

Falsify-if: Rule text, once read, shows no relevant pattern risk for our order styles; edge then downgraded to B (monitor only).

Horizon: DAILY
Availability: PUBLIC_SCHEDULED
Priority: B+

## Final architecture edge (Truth Ladder)

The Truth Ladder for W70B: (1) rulebook/spec fact (exchange primary, versioned); (2) reconstructed book state from the licensed MDP 3.0 feed with commit-at-event-boundary and sequence integrity; (3) intermediate microstructure outcomes (fill-before-move, refill half-life, sweep absorption, iceberg hold); (4) execution-quality outcomes (slippage quantiles, markouts); (5) only then any return-linked claim. A candidate may influence live behavior only as a risk gate or execution parameter until stage 4 evidence exists.

## Highest-priority W70B tests

1. W70B-E10 Executed-Beyond-Display Iceberg Detector
2. W70B-E09 MBO Exact Queue-Ahead Reconstruction
3. W70B-E18 Fill-Before-Move Probability
4. W70B-E31 Stop-With-Protection Fill Envelope
5. W70B-E32 Market-With-Protection Rejection State
6. W70B-E50 Multi-Level Sweep Event Detector
7. W70B-E16 Queue-Reactive Intensity Surface
8. W70B-E24 Multi-Level Integrated OFI Depth Slope
9. W70B-E26 Strategy-Pair Self-Match Exposure Monitor
10. W70B-E57 Post-Sweep Book Resilience Half-Life
