# Wave 71K — Crypto Perpetual-Futures & Exchange Microstructure

Namespace: **W71K**

Thesis: crypto perpetual swaps are the one liquid, 24/7 leveraged market whose rules are fully documented, machine-readable and continuously observable: hourly or multi-hour funding formulas with explicit clamps and dead-bands, mark/oracle constructions with published weights and EMA time-constants, liquidation engines with explicit partial-liquidation sizes and cooldowns, backstop vaults, insurance-fund triggers and ADL queues. Each rule creates a deterministic state variable (distance to a clamp, pending mark revision, liquidation-slice schedule, insurance-fund drawdown) that can be computed from public feeds before the consequence is priced. The research target is the rule-state, not "funding is high so fade it". Where the system trades CME BTC/MBT or uses crypto as a risk-appetite proxy for NQ/ES, these states are candidate regime, risk-gate and entry-confirmation inputs.

Boundary: W3-E61..E70 (crypto capital routing: stablecoin migration, CME basis pressure E64, CME-vs-offshore dispersion E65, ETF-CME-spot graph E66, collateral stress triangle E69) own the coarse cross-venue ideas; W71K adds venue-rule mechanics at second-to-hour resolution and names increments where it extends them. W63 (clearing margin), W69 (options microstructure), W70 (Globex microstructure), W77 (volatility products) and W78 (execution quality) own the equity/futures analogues; W79 (on-chain/stablecoin/ETF flow) owns chain-level flow state. W71K does not duplicate any of those.

All candidates are research hypotheses only. Claude owns later implementation. No profitability is claimed; every item is subject to the vault's intermediate-outcome promotion gate. Items resting on facts not verified from a primary page carry PROVENANCE_PENDING.

Common conventions: `t` = event time at exchange; `rx` = our receive time; features use only data with rx <= decision time. Funding sign convention: positive = longs pay shorts (verified for Hyperliquid, Binance, OKX docs). Thresholds written as parameters (theta_*, k_*) are placeholders to be calibrated out-of-sample, never claimed values.

---

## Block A — Funding mechanics

## W71K-E01 — Funding Dead-Band Occupancy and Exit Distance
Primary source: Binance Futures funding FAQ (https://www.binance.com/en/support/faq/detail/360033525031) — F = [P + clamp(I - P, -0.05%, +0.05%)] / (8/N); if P in [-0.04%, +0.06%] the funding equals the 0.01% interest component. Hyperliquid funding doc has the same clamp form with +/-0.0005.
Mechanism: inside the band the funding gradient with respect to premium is zero (funding is "inert"); outside it, funding moves one-for-one with premium. Positioning cost therefore changes discontinuously at the band edges, so crowd behaviour should differ between states.
Features: dist_up = (I + 0.0005) - P_hat; dist_dn = P_hat - (I - 0.0005); band_state in {INERT, LIVE_POS, LIVE_NEG}; time-in-state; P_hat = running mean of 5s premium samples in the current window.
Target: next-15m/60m signed return, realized vol, and next-window funding change, conditional on band_state and OI change.
Falsify-if: conditional distributions of return/vol are indistinguishable between INERT and LIVE states after controlling for |premium| level (placebo: shuffle band edges by a random offset); sign is ambiguous a priori (LIVE_POS may mean crowded longs, or confirmed trend).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: A

## W71K-E02 — Intra-Window Funding Forecast Error (Partial-Average Surprise)
Primary source: Hyperliquid Funding doc (https://hyperliquid.gitbook.io/hyperliquid-docs/trading/funding) — premium sampled every 5 seconds and averaged over the hour; paid hourly at 1/8 of the computed 8h rate; capped at 4%/hour.
Mechanism: after m minutes only m/60 of the hour's premium samples are known; the rest is deterministic-in-expectation given current premium persistence. The gap between the partial-average implied final rate and the previous hour's paid rate is a known-in-advance cash transfer between sides.
Features: F_partial(m) from our own 5s premium reconstruction (impact-price formula with impact_notional 20,000 USDC for BTC/ETH, 6,000 for others); F_hat_final = AR(1) projection; surprise_m = F_hat_final - F_prev_hour; also compare with API predictedFundings.
Target: flow/return in the final 10 minutes of the hour, and the change in OI across the hour boundary.
Falsify-if: surprise_m has no incremental information over |premium| level and OI change in a nested regression; negative control: use a time-shifted hour boundary (+17 minutes).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: A-

## W71K-E03 — Funding Settlement Boundary Flow Window
Primary source: Hyperliquid Funding doc (hourly), Binance FAQ (default 00:00/08:00/16:00 UTC, switchable to 1h/4h), Bybit v5 funding history (https://bybit-exchange.github.io/docs/v5/market/history-fund-rate; interval per symbol).
Mechanism: holders of a position at the settlement timestamp pay or receive funding; marginal traders with large |F| have an incentive to flatten just before payment (payers) or hold through (receivers), producing time-localised flow around deterministic clocks.
Features: minutes-to-next-settlement per venue (use per-symbol interval, not an assumed 8h), |F_pred|, signed F_pred, taker imbalance in T-10..T-0 and T..T+10.
Target: signed return and volume in [T-5m, T+5m] windows relative to matched non-settlement windows at the same UTC minute offset.
Falsify-if: windows at settlement show no excess |return| or volume vs minute-matched controls; or effect vanishes after removing Asia/Europe/US session open overlaps (00:00, 08:00, 16:00 UTC coincide with session transitions — the main confound).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B+

## W71K-E04 — Binance Funding-Interval Switch State
Primary source: Binance funding FAQ — interval switches to 1 hour (effective 2025-05-02) when the previous settlement hits the cap or floor; reverts to 4 hours (effective 2026-01-02) after 16 consecutive 1-hour cycles with |F| <= 0.025% (change takes effect on the 17th cycle).
Mechanism: the interval switch is a public marker that a symbol hit its funding cap/floor, i.e. an extreme one-sided leverage episode; the reversion rule gives a deterministic "cool-down" clock.
Features: interval_h per symbol (from exchange info / funding info endpoint — endpoint name PROVENANCE_PENDING), cycles_since_switch, time-to-revert.
Target: forward 1h-24h drawdown/volatility of the symbol and of BTC; cross-sectional event study across alts.
Falsify-if: post-switch return/vol is not distinguishable from matched cap-touch events that did not switch (the rule changed in 2025-05, so pre-rule history is structurally different — version it).
Horizon: DAILY
Availability: PUBLIC_REALTIME
Priority: B+

## W71K-E05 — Cross-Venue Predicted-Funding Dispersion
Primary source: Hyperliquid info endpoint `predictedFundings` (https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint/perpetuals) — returns predicted funding for HlPerp, BinPerp and BybitPerp; only first perp dex.
Mechanism: the three predicted rates are computed on different books with different impact notionals and clamps; their dispersion shows venue-specific leverage demand and arbitrage capacity (funding arbitrageurs equalise rates only up to transaction and margin costs).
Features: spread_HL_Bin, spread_HL_Byb (normalised per hour: Binance/Bybit interval may differ — convert to per-hour rate first), z-score vs trailing 7d, sign agreement of all three.
Target: next-1h convergence of spread; signed return of the high-funding venue's premium; basis tightening.
Falsify-if: spread z-score does not predict convergence beyond a no-change forecast; mismatched interval normalisation removes the effect (this is the primary data-quality trap).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: A

## W71K-E06 — Impact-Notional Depth Fragility of the Premium
Primary source: Hyperliquid Funding doc: impact_price_difference uses average execution price for impact_notional_usd on each side; contract specs: 20,000 USDC for BTC/ETH, 6,000 for others. Binance FAQ: IMN = 200 USDT / initial margin rate at max leverage.
Mechanism: the premium is a function of the book only out to the impact notional; if depth to that notional is thin, the premium (and thus funding) is dominated by a few resting orders and is cheap to move.
Features: depth_ratio = displayed depth within +/-x bps / impact_notional; premium_noise = std of 5s premium samples over last 60s; fragile flag when depth_ratio < theta.
Target: whether high |funding| signals are informative only when the book is robust (interaction test); reversal of premium within 60s when fragile.
Falsify-if: funding-based signals perform equally in fragile vs robust states; placebo: random depth labels.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B+

## W71K-E07 — HIP-3 Mid-Based Premium Formula Regime
Primary source: Hyperliquid Funding doc: for HIP-3 perps premium = 0.5*(impact_bid_px + impact_ask_px)/oracle_px - 1 (a more responsive formula), with funding multiplier and interest rate set by deployers; info `perpDexs` exposes `assetToFundingMultiplier` and `assetToStreamingOiCap`.
Mechanism: the mid-based premium has no dead-zone from impact-price max() terms, so HIP-3 funding reacts to any oracle/mid gap; deployers' multipliers rescale carry cost. Funding is therefore a faster stress gauge for HIP-3 equity/commodity/index perps than for crypto perps.
Features: premium_mid, multiplier, effective hourly funding, gap persistence.
Target: oracle-mid gap closure speed on HIP-3 gold/index perps; whether the gap predicts the next oracle update.
Falsify-if: gap-closure half-life is independent of multiplier; HIP-3 asset list/params are deployer-controlled and change — version them.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B+

## W71K-E08 — Funding Sign Persistence Run-Length Prior
Primary source: Hyperliquid `fundingHistory` (hourly), Bybit `/v5/market/funding/history` (limit 200, per-symbol interval), OKX `/api/v5/public/funding-rate` (settFundingRate, settState), Deribit `public/get_funding_rate_history` (hourly).
Mechanism: persistent same-sign funding means one side keeps paying to hold; carry drag accumulates and marginal holders of the paying side leave, but trend followers may also persist. Run-length is a slow-moving crowding prior.
Features: consecutive same-sign hours, cumulative funding paid over run, run-length percentile within symbol-year.
Target: hazard of sign flip; subsequent 4h/24h return skew.
Falsify-if: sign-flip hazard is flat in run length (geometric); negative control: sign-shuffled funding with same marginal distribution.
Horizon: DAILY
Availability: PUBLIC_REALTIME
Priority: B+

## W71K-E09 — OKX Funding Settlement State and Forecast Revision
Primary source: OKX docs v5 Get funding rate (https://www.okx.com/docs-v5/en/) — fields fundingRate (predicted for upcoming period), settFundingRate, settState (processing/settled), min/maxFundingRate, premium, impactValue, formulaType (noRate/withRate), nextFundingTime.
Mechanism: OKX exposes both the forecast and the last settled rate plus per-instrument caps, enabling a clean "forecast revision" series and cap-proximity measure.
Features: rev = fundingRate_t - fundingRate_{t-1h}; cap_prox = fundingRate / maxFundingRate; formulaType switch events.
Target: forward premium change; liquidation intensity in next hour when cap_prox is high.
Falsify-if: cap_prox has no relation to subsequent liquidation intensity once OI and vol are controlled. formulaType semantics beyond the doc string are PROVENANCE_PENDING.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E10 — Deribit Damped Funding vs Dated-Future Carry
Primary source: Deribit support, Inverse Perpetual (https://support.deribit.com/hc/en-us/articles/31424954847133-Inverse-Perpetual) — damper: premium within +/-0.025% maps to 0 funding, otherwise shifted toward zero by 0.025%; cap +/-0.5% (BTC), +/-1% (ETH) per 8h. (Page returned 403 to direct fetch; values from search snippet — PROVENANCE_PENDING until re-read.) API: ticker fields `current_funding`, `funding_8h`.
Mechanism: Deribit's funding is continuous and damped differently from Binance's dead-band, making it a distinct (options-venue) read of leverage demand, and Deribit lists dated futures on the same index, giving an in-venue carry curve.
Features: funding_8h, perp-vs-dated-future annualised basis on the same index, ticker mark/index.
Target: consistency residual: basis_annualised - k*funding_8h*3*365; residual mean-reversion horizon.
Falsify-if: residual is not mean-reverting after transaction cost (use He-Manela-Ross-von Wachter bounds as cost model, see E50).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E11 — Hyperp (Pre-Launch) Funding Damping and Conversion Event
Primary source: Hyperliquid Hyperps doc (https://hyperliquid.gitbook.io/hyperliquid-docs/trading/hyperps) — oracle = 8h-EWMA of minutely marks (capped at 4x one-month mean mark); funding premium samples are 1% of the usual formula; mark capped at 3x the 8h EMA; converts to a normal perp shortly after ABC/USDT spot lists on Binance, OKX or Bybit.
Mechanism: with funding damped 100x and oracle self-referential, early hyperp prices are momentum-prone; the conversion event swaps the oracle to external spot, creating a price-regime break.
Features: hyperp mark/oracle ratio, distance to 3x cap, hours to expected conversion, CEX pre-launch perp price (third mark component).
Target: return and vol around the conversion timestamp; cap-binding episodes.
Falsify-if: conversion-window abnormal return indistinguishable from matched listing events; sample size is small (flag).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E12 — Funding-Cost Break-Even for Intraday Carry of Crypto Proxy Exposure
Primary source: Hyperliquid Funding doc (payment = position_size * oracle_price * funding_rate; oracle not mark), Binance FAQ (interest 0.01%/8h baseline).
Mechanism: for a system using BTC perps as intraday hedge/proxy, expected funding paid over a holding window is a deterministic cost; it matters only when |F| is large relative to expected edge. Computing it exactly (hourly vs 8h, oracle vs mark notional) avoids bias in backtests that ignore funding.
Features: cost_bps(hold) = sum of predicted hourly F over the hold window; interaction with entry signal.
Target: net-of-funding P&L attribution; threshold at which funding flips a signal's sign.
Falsify-if: net result is insensitive to funding in a replay (then funding is a nuisance, not an edge — still a valid, useful finding).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

---

## Block B — Mark / index / oracle construction

## W71K-E13 — Pending Mark Revision (Oracle Staleness Gap)
Primary source: Hyperliquid Robust price indices doc (https://hyperliquid.gitbook.io/hyperliquid-docs/trading/robust-price-indices) — oracle = weighted median of CEX spot prices, updated by validators ~every 3 seconds; mark is updated whenever new oracle prices are published; mark/liquidation/TP-SL use the mark.
Mechanism: between publications the mark is fixed in time while CEX prices keep moving; the deterministic mismatch gap_t = cex_weighted_mid_t - oracle_last is information about the sign and size of the next mark update, which in turn triggers liquidations/TP-SL on a ~3s grid.
Features: gap_bps, time_since_last_update, sign(gap)*|gap|/atr_3s.
Target: sign and size of next mark change; probability of a liquidation event in the next update.
Falsify-if: gap has no incremental predictive power for next-update direction beyond the last 3s return of the CEX mid (it may be fully mechanical, which is itself the validation); placebo: use gap computed against a stale (>=60s old) oracle.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: A+

## W71K-E14 — Mark Median Input Identity (Which Leg Is Binding)
Primary source: same page — mark = median of (i) oracle + 150s EMA of (HL mid - oracle), (ii) median(best bid, best ask, last trade on HL), (iii) weighted median of Binance, OKX, Bybit, Gate IO, MEXC perp mids with weights 3,2,2,1,1; if exactly two of three exist, add the 30s EMA of leg (ii).
Mechanism: the median selects whichever leg lies between the other two; when HL-local book diverges from CEX perps, the CEX leg or the EMA leg binds. Binding leg identity tells whether HL-local pressure or cross-venue price is driving liquidation triggers.
Features: binding_leg in {EMA, LOCAL, CEX}; fraction of last 5 minutes with LOCAL binding; mark - leg_ii spread.
Target: probability that HL liquidations fire at prices off the local book; reversion of HL-local book to mark.
Falsify-if: binding-leg state does not change the relation between mark-book divergence and subsequent book reversion.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B+

## W71K-E15 — 150-Second EMA Basis Stickiness
Primary source: same page; EMA update ema = num/den with num -> num*exp(-t/2.5min) + sample*t, den -> den*exp(-t/2.5min) + t.
Mechanism: leg (i) embeds the recent HL premium with a 150s time constant; after a fast move the mark carries a decaying memory of the pre-move premium, so mark lags fast regime shifts by design.
Features: reconstruct EMA exactly from mid/oracle history; ema_residual = (mid - oracle) - ema.
Target: reversion half-life of the mark-vs-book gap vs 150s; asymmetry up vs down.
Falsify-if: half-life is not near the stated constant (would imply our reconstruction or the doc is stale — re-verify before use).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E16 — Cross-Source Price Dispersion as Stress Gauge
Primary source: Hyperliquid oracle (CEX weighted median), Deribit index (`index_price` in ticker, https://docs.deribit.com/api-reference/market-data/public-ticker), CME CF indices (BRR/BRTI, https://www.cfbenchmarks.com/data/indices/BRR), OKX/Bybit index prices (Bybit ticker `indexPrice`).
Mechanism: each index uses different constituents/weights/outlier handling; dispersion across them widens when a constituent venue lags, depegs (USDT/USD) or is dislocated.
Features: max-min across indices in bps, z-scored; contribution by outlier source.
Target: next 30m realized vol and liquidation intensity; early warning of constituent-specific dislocations.
Falsify-if: dispersion z-score has no relation to forward vol after conditioning on current vol; BRTI real-time requires licence (rights status PENDING) — fall back to three free indices.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B+

## W71K-E17 — CF BRR Observation-Window Distortion (15:00-16:00 London)
Primary source: CME CF Bitcoin Reference Rate methodology (https://cmegroup.com/trading/files/bitcoin-reference-rate-methodology.pdf; CF suitability analysis https://docs.cfbenchmarks.com/BRR-suitability-analysis.pdf) — observation window 15:00-16:00 London, 12 five-minute partitions, per-partition volume-weighted median, arithmetic mean of partitions. (Current methodology revision PROVENANCE_PENDING; found via search of older docs.)
Mechanism: CME BTC/MBT futures settle (final settlement and, for options/futures expiry, reference) to BRR; participants with BRR-linked exposure may trade in the window to influence or hedge the fix; equal weighting of partitions means flow in a quiet partition has more influence per unit volume.
Features: partition index k=1..12, partition volume share, partition VWM minus running price; window abnormal volatility vs same clock at non-expiry days.
Target: partition-level mean-reversion after window end (16:00-16:30 London); effect on last-trading-day expiries.
Falsify-if: no excess volume/volatility in the window vs minute-matched control days; note the window coincides with US pre-open and NQ/ES data times (confound — control with NQ volume).
Horizon: INTRADAY
Availability: PUBLIC_SCHEDULED
Priority: B+

## W71K-E18 — Stablecoin-Denomination Quanto Gap on USDC-Margined USDT-Priced Perps
Primary source: Hyperliquid Contract specifications (https://hyperliquid.gitbook.io/hyperliquid-docs/trading/contract-specifications) — crypto perps are USDC-margined, oracle priced in USDT, "no conversions with the USDC/USDT exchange rate are applied" (quanto); only PURR and HYPE oracles are USDC-denominated.
Mechanism: if USDT trades below USDC (or USDT-USD CEX pairs dislocate), the oracle denominated in USDT mispriced vs USDC collateral flows through marks, funding and liquidations without any change in the underlying coin.
Features: USDT/USDC spot ratio (from CEX pair), deviation in bps, correlation with HL premium.
Target: premium residual attributable to stablecoin ratio; liquidation events when ratio deviates > theta.
Falsify-if: premium residual is unrelated to the ratio in deviation episodes; extreme depeg samples are rare — pool across events with caution. Links to W79 stablecoin state.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E19 — Index-Constituent Venue Outage / Latency Detection
Primary source: Hyperliquid oracle docs (weights by CEX liquidity), Bybit ticker (100ms delta pushes), OKX mark price channel; own timestamp comparison.
Mechanism: weighted-median oracles and mark legs silently down-weight or drop stale constituents; a lagging constituent biases the oracle and temporarily mispricess funding and liquidation triggers.
Features: per-venue staleness = rx - last update; venue price minus consensus median; staleness-weighted consensus error.
Target: next-oracle error; probability of liquidation clusters on the lagging side.
Falsify-if: staleness events do not precede oracle revisions; constituent dropout rules for HL are not publicly specified beyond weights (PROVENANCE_PENDING) — only measure externally observable symptoms.
Horizon: INTRADAY
Availability: UNKNOWN_MEASURED
Priority: B

## W71K-E20 — Mark-vs-Last Divergence Trigger Asymmetry on Liquidation Venues
Primary source: Hyperliquid Liquidations doc: "Liquidations use the mark price ... during times of high volatility ... mark price may be significantly different from book price"; OKX liquidation-orders `bkPx` = liquidation mark price.
Mechanism: forced orders fire on the mark path, not last trade; when mark leads the book (E13) liquidations hit the book after the fact; when mark lags, positions survive longer than book prices imply and then liquidate in bunches on catch-up.
Features: sign and size of (mark - book mid), recent change; count of positions within 0.5% of liquidation price on the mark path (if observable).
Target: liquidation burst size in next 10s conditional on lead vs lag mark state.
Falsify-if: lead/lag mark state has no effect on burst size; need position coverage (E21) to be meaningful.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B+

---

## Block C — Liquidation engines

## W71K-E21 — Liquidation Price Cluster Proximity (Public-Position Heatmap)
Primary source: Hyperliquid Liquidations doc (formula liq_price = price - side*margin_available/position_size/(1 - l*side), l = 1/maintenance leverage; maintenance margin = half initial at max leverage) and Margin tiers doc (https://hyperliquid.gitbook.io/hyperliquid-docs/trading/margin-tiers; BTC 40x to 150M notional, 20x above). Info `clearinghouseState` is per-user; aggregate coverage via Coinversa Pulse `live_liquidation_heatmap` (third-party; coverage PROVENANCE_PENDING).
Mechanism: HL positions are public by address, so the notional liquidating at each price can be summed; a large cluster just beyond the current mark is a known magnet/accelerant for stop-run dynamics.
Features: cluster_notional(+/-d%) / displayed depth(d%), side, nearest cluster distance in ATR units.
Target: probability of touching the cluster within 30m; post-touch overshoot and reversion.
Falsify-if: touch probability is no higher than for matched random price levels (placebo: levels shifted by a random multiple of ATR); position snapshot must be time-stamped to avoid look-ahead.
Horizon: INTRADAY
Availability: UNKNOWN_MEASURED
Priority: A

## W71K-E22 — Partial-Liquidation Slice and 30-Second Cooldown Schedule
Primary source: Hyperliquid Liquidations doc — for liquidatable positions > 100k USDC only 20% is sent as a market order; after a block with a partial liquidation of any of a user's positions there is a 30-second cooldown during which all market liquidation orders for that user are for the entire position.
Mechanism: a large account is liquidated in a known sequence: first slice 20% of position, then (if still liquidatable after the 30s cooldown) a full-position order. The second wave is therefore larger than the first and its timing is predictable once the first slice prints.
Features: first-slice detection from `userEvents` liquidation or trades with liquidation flags; implied remaining size = 4x first slice; countdown = 30s from block.
Target: size/timing of the second liquidation wave; price impact after the first slice.
Falsify-if: second-wave size distribution does not exceed first-slice size, or timing does not cluster after 30s (doc may have changed — version "Last updated 1 year ago").
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: A+

## W71K-E23 — Backstop-vs-Book Liquidation Share
Primary source: Hyperliquid Liquidations doc: below 2/3 of maintenance margin a position can be taken by the liquidator vault (component strategy of HLP); backstop transfers positions without book execution; Coinversa `pulse_backstop_events` (third-party).
Mechanism: book liquidations impact price; backstop liquidations transfer risk to HLP without book impact but add HLP inventory that HLP must later unwind or hold.
Features: share of liquidated notional via backstop in rolling 1h; HLP net inventory after event (if observable via vault state — source PENDING).
Target: price impact per $ liquidated for book events vs backstop; subsequent HLP-driven flow.
Falsify-if: impact per $ is identical for both channels, or backstop share does not predict subsequent reversals.
Horizon: INTRADAY
Availability: UNKNOWN_MEASURED
Priority: B

## W71K-E24 — Liquidation Notional to Book-Depth Ratio and Reversal
Primary source: Bybit `allLiquidation.{symbol}` (https://bybit-exchange.github.io/docs/v5/websocket/public/all-liquidation; 500ms pushes, fields T,s,S,v,p; S=Buy means long liquidated), Hyperliquid l2Book/trades WebSocket (https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/websocket/subscriptions).
Mechanism: forced flow is price-insensitive; when liquidated size is large relative to resting depth, price overshoots fundamental value and mean-reverts as liquidity returns (inventory/overshoot logic).
Features: R = liq_notional(10s) / depth(25 bps); signed by S; overshoot = peak deviation from pre-burst VWAP; recovery fraction after 60s/300s.
Target: recovery fraction vs R; separate momentum (first seconds) from reversal (later).
Falsify-if: no monotone relation between R and recovery; placebo: same bursts replaced by volume-matched non-liquidation bursts (identify via venue flag).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: A+

## W71K-E25 — Liquidation-Feed Sampling Censoring Index
Primary source: Binance USDS-M `@forceOrder` and `!forceOrder@arr` streams (https://developers.binance.com/docs/derivatives/usds-margined-futures/websocket-market-streams/Liquidation-Order-Streams): 1000ms update, only the latest liquidation order per symbol in the window (search-confirmed; page content did not render directly — PROVENANCE_PENDING on field list). OKX liquidation-orders "doesn't represent the total number of liquidations on OKX"; ordering not guaranteed (OKX docs).
Mechanism: public liquidation feeds are censored samples; during cascades the fraction of 1s windows with at least one event approaches 1 and the observed count saturates, understating true intensity.
Features: sat_frac = fraction of last 60 one-second windows with an event; corrected intensity via cross-venue scaling to Bybit (500ms) counts.
Target: use sat_frac itself as a cascade-in-progress indicator and test whether correcting for censoring improves burst-size prediction.
Falsify-if: sat_frac adds no information beyond observed notional; saturation could simply track volatility (control with realized vol).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: A-

## W71K-E26 — Multi-Venue Cascade Composite (OI-Normalised)
Primary source: Bybit allLiquidation, OKX liquidation-orders (instType SWAP), Binance forceOrder, Hyperliquid userEvents/liquidation (WsLiquidation); OI from each venue (Bybit/OKX tickers, Binance openInterestHist).
Mechanism: leverage is spread across venues with different liquidation engines; a cascade is cross-venue when liquidations on one venue move prices that trigger others.
Features: C_t = sum_v liq_notional_v(60s)/OI_v; lead-lag of first-venue onset; fraction of long vs short.
Target: duration and total size of cascade; next-hour realized vol; spillover into CME BTC/MBT and, as a risk-gate, NQ/ES (see E29).
Falsify-if: composite no better than best single-venue feed; venue feeds differ in censoring (E25) — normalise before combining. Increment over W3-E69: second-level, engine-specific.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: A

## W71K-E27 — Long-vs-Short Liquidation Skew x Funding Sign (Squeeze vs Capitulation)
Primary source: Bybit allLiquidation `S` side semantics (Buy = long liquidated); funding rates per E01/E09.
Mechanism: long liquidations under positive funding indicate capitulation of crowded longs; long liquidations under negative funding indicate trend-following shorts winning. Same liquidation sign, different crowding context.
Features: skew = (L_long - L_short)/(L_long+L_short) over 5m; funding sign and percentile; OI change.
Target: forward 30m return and vol by 4 cells (skew sign x funding sign).
Falsify-if: the four cells have equal forward distributions; sign pre-registered as ambiguous: capitulation (reversal) vs continuation both plausible.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: A-

## W71K-E28 — Post-Cascade OI Flush Completion
Primary source: Binance `/futures/data/openInterestHist` (5m min period, 30-day history, fields sumOpenInterest, sumOpenInterestValue; limit default 30, max 500; https://developers.binance.com/docs/derivatives/usds-margined-futures/market-data/rest-api/Open-Interest-Statistics), Bybit ticker openInterest, Hyperliquid `metaAndAssetCtxs` openInterest.
Mechanism: forced closure removes OI; once OI drops by a large fraction and liquidation intensity decays, the leverage stock has been reset and fragility is lower; a continuing OI decline signals the cascade is not done.
Features: dOI_coin/OI over cascade window (coin-denominated to avoid price effect), liquidation decay half-life, funding normalisation.
Target: forward 1h-6h vol compression and reversal probability after "flush complete" vs "flush ongoing".
Falsify-if: OI drop fraction has no relation to forward vol/reversal after controlling for the magnitude of the price move. Binance history is only 30 days: archive continuously.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: A

## W71K-E29 — Crypto Liquidation Burst as Equity-Index Risk Gate
Primary source: cross-asset hypothesis; crypto data per E26; NQ/ES state from Globex data (W70 owns microstructure). Context: Oct 10-11, 2025 episode reported ~$19B open interest erased (secondary sources; academic "Anatomy of the Oct 10-11, 2025 Crypto Liquidation Cascade" not read — PROVENANCE_PENDING).
Mechanism: leveraged crypto liquidations can coincide with macro risk-off (same news) and may transmit via risk-parity/volatility-targeting and retail cross-holdings; the claim is a conditioning gate, not causation.
Features: C_t (E26) percentile; NQ 5m realized vol; sign of macro news in same minute (placebo conditioning).
Target: NQ/ES forward 15m/60m absolute return and spread/volatility; whether C_t adds information beyond VIX-futures and NQ own vol.
Falsify-if: no incremental information beyond NQ own volatility and scheduled-news dummies; high chance of confounding by common shocks; most likely outcome is a null — a valid kill.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E30 — Cross-Margin Contagion Sequencing (Majors Lead Alts)
Primary source: Hyperliquid Margining doc: cross margin shares collateral across cross positions; backstop liquidation of a cross position transfers all cross positions and margin; unified/portfolio margin extend sharing across DEXs with same collateral.
Mechanism: a loss on a major (BTC/ETH) reduces account equity, pushing alt positions in the same cross account toward liquidation without any alt-price move; liquidation of alts can therefore lag BTC moves by seconds-minutes.
Features: BTC/ETH move over last 30-120s; alt long OI held by accounts with large BTC exposure (requires position-level data, coverage PENDING); alt liquidations in the next 2 minutes.
Target: alt liquidation intensity conditional on BTC move vs alt's own beta-implied move.
Falsify-if: alt liquidation intensity is fully explained by alt's own price move; effect requires account-level join (data-rights check).
Horizon: INTRADAY
Availability: UNKNOWN_MEASURED
Priority: B

## W71K-E31 — Margin-Tier Notional Cliffs
Primary source: Hyperliquid Margin tiers doc — maintenance_margin = notional*rate - deduction; tier rate = (initial margin rate at max leverage at tier)/2; BTC: 0-150M notional at 40x, >150M at 20x (maintenance 1.25% then 2.5%).
Mechanism: a single huge position crossing a tier boundary sees its maintenance requirement jump (continuous because of deduction, but with a steeper slope), shrinking its liquidation distance; whales near boundaries have nonlinear risk.
Features: for each public large position: distance to liquidation price computed with the tier slope; positions within theta of boundary.
Target: liquidation hazard of whales vs matched notional below boundary.
Falsify-if: hazard is continuous across tier boundary after controlling for distance-to-liquidation; margin tables change (versioned in `meta`).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E32 — Max Order Value Caps as Impact Ceiling
Primary source: Hyperliquid Contract specifications — max market order value $30,000,000 for max leverage >= 25, $5,000,000 for [20,25), $2,000,000 for [10,20), else $500,000; max limit order = 10x.
Mechanism: the engine caps single-order size, so whale entries/exits must be sliced across blocks; observable repeated near-cap prints indicate a large parent order.
Features: count of near-cap market orders in 1 minute, same address (public), cumulative notional.
Target: continuation vs reversal after sliced parent-order detection.
Falsify-if: no excess drift after detection vs size-matched uncapped prints.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

---

## Block D — Auto-deleveraging and insurance funds

## W71K-E33 — OKX ADL-Warning State Machine
Primary source: OKX `adl-warning` WebSocket channel (https://www.okx.com/docs-v5/en/, public channel): data pushed once per second only in states `warning` or `adl`; fields state, bal (real-time security fund balance), instType, instFamily, ts; adlType events rate_adl_start, bal_adl_start, pos_adl_start (premarket); several other fields deprecated.
Mechanism: absence of messages means normal; presence signals the insurance fund is under stress, and ADL (forced position reduction against profitable counterparties) may begin. These are venue-published tail-risk flags.
Features: state in {NORMAL(no msg), WARNING, ADL}; time-in-state; bal trend while in warning.
Target: forward 1h-24h tail volatility of the family (BTC-USDT) and of BTC overall; cross-venue contagion.
Falsify-if: warning occurrences do not precede higher tail frequency vs matched stressed periods without warnings. Absence of message must be treated as NORMAL only when WS connection verified alive (missingness class SOURCE_DOWN vs TRUE_ZERO).
Horizon: INTRADAY
Availability: PUBLIC_EVENT_DRIVEN
Priority: A+

## W71K-E34 — Bybit Insurance-Pool Drawdown-to-Trigger Distance
Primary source: Bybit help center, Auto-Deleveraging (ADL) Mechanism (https://www.bybit.com/en/help-center/article/Auto-Deleveraging-ADL) — ADL can trigger when a pair's 8-hour insurance-fund drawdown reaches the trigger line measured against the 8h high; isolated pools update every minute by API and every second via WebSocket, shared pools every 24h (details from search excerpts; locale pages differ — PROVENANCE_PENDING until the English article is read in full).
Mechanism: the ratio drawdown_8h / trigger_line is a bounded stress index per symbol; closeness to 1 implies imminent deleveraging of winners on the other side.
Features: dd = 1 - bal/max_8h(bal); proximity = dd/trigger; derivative of dd.
Target: probability of ADL event within 1h; price behaviour of the affected symbol (squeeze of winners' exits).
Falsify-if: proximity has no relation to subsequent ADL or tail events; endpoints for the pool (Insurance History) not verified.
Horizon: INTRADAY
Availability: UNKNOWN_MEASURED
Priority: B+

## W71K-E35 — Hyperliquid ADL Queue Crowding on the Winning Side
Primary source: Hyperliquid Auto-deleveraging doc (https://hyperliquid.gitbook.io/hyperliquid-docs/trading/auto-deleveraging): when an account/isolated position value is negative, opposite-side users are ranked by sort index (mark_price/entry_price)*(notional_position/account_value); those positions close at the previous mark price against the underwater user; users with no open positions never socialise losses.
Mechanism: the most profitable, most levered winners are the first forced out, at a known price; if the ADL queue head is dominated by a few large winners, ADL removes late trend followers exactly when the move is extended.
Features: queue head concentration (share of opposite-side OI in top-k index ranks), distance of top-ranked positions to being ADL'd (requires a loser insolvency), historical frequency (Oct 2025 event referenced in secondary sources only).
Target: after an ADL event: persistence of trend vs mean reversion; change in opposite-side OI.
Falsify-if: post-ADL returns equal matched large liquidation days without ADL; ADL events are very rare — sample-size caveat; treat as event case study not a signal.
Horizon: DAILY
Availability: UNKNOWN_MEASURED
Priority: B

## W71K-E36 — Own-Position ADL Quantile as Execution Risk Gate
Primary source: Binance USDS-M `Position ADL Quantile Estimation` endpoint (https://developers.binance.com/docs/derivatives/usds-margined-futures/trade/rest-api/Position-ADL-Quantile-Estimation) — endpoint exists in docs; response fields not read (page truncated in fetch) — PROVENANCE_PENDING. HL analogue: sort index in E35 is computable from own state.
Mechanism: if the system runs crypto positions, its own ADL rank is a venue-side forced-exit risk; high rank during profit streaks implies the profitable leg can be closed involuntarily.
Features: own ADL quantile per symbol; PnL/margin ratio.
Target: risk gate: reduce leverage when rank high and market in cascade state (E26).
Falsify-if: nothing market-wide to falsify; test via paper-trading logs whether forced-exit events correlate with high quantile.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E37 — Insurance Fund to Open-Interest Ratio Slow Prior
Primary source: Binance `Insurance Fund Balance` endpoint (docs page name seen in site map; fields unverified), Bybit Insurance History page, OKX adl-warning `bal`.
Mechanism: loss-absorption capacity relative to leverage stock determines how soon exchanges ADL; thin insurance relative to OI means shocks of a given size propagate to ADL more readily.
Features: IF/OI per venue; trend over weeks.
Target: slow prior for tail-vol conditional on shocks; conditioning for E33/E34.
Falsify-if: IF/OI ratio does not modulate the shock-to-ADL mapping in event samples.
Horizon: SLOW_PRIOR
Availability: UNKNOWN_MEASURED
Priority: B

## W71K-E38 — Security-Fund Decline Rate (OKX rate_adl_start Trigger Proximity)
Primary source: OKX docs adl-warning: adlType rate_adl_start = ADL begins due to high security-fund decline rate (bal vs maxBal over past 8h; decRate/adlRate fields now deprecated and returned empty).
Mechanism: OKX documents a rate-based trigger distinct from balance-based; with deprecated rates, the system must reconstruct decline rate itself from bal history.
Features: bal_t / max_{8h}(bal) from our own archived stream.
Target: lead time between decline-rate breach and observed adlType event.
Falsify-if: our reconstructed ratio does not precede published events (then fields are internal-only). Reconstruction depends on archiving ≥8h of messages emitted only in warning state — data gap when the fund is normal.
Horizon: INTRADAY
Availability: PUBLIC_EVENT_DRIVEN
Priority: B

---

## Block E — Open-interest dynamics

## W71K-E39 — Price x OI Quadrant State at 5-Minute Resolution
Primary source: Binance `/futures/data/openInterestHist` (5m), Hyperliquid `metaAndAssetCtxs` (openInterest, markPx, funding, premium, oraclePx, dayNtlVlm, impactPxs).
Mechanism: price up/OI up = new longs (or shorts squeezed with fresh shorts), price up/OI down = short covering, price down/OI up = new shorts, price down/OI down = long liquidation/exit. Different quadrants imply different continuation odds.
Features: sign(dP), sign(dOI_coin), magnitudes in sigma units; persistence of quadrant.
Target: next 15m/60m return by quadrant, after controlling for funding.
Falsify-if: no quadrant effect vs shuffled OI timestamps; sign ambiguity pre-registered (continuation or exhaustion).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: A-

## W71K-E40 — OI Turnover Ratio (New-Position Share)
Primary source: Hyperliquid `dayNtlVlm`, `openInterest`; Bybit ticker openInterest + volume24h (field availability in Bybit docs: openInterest verified).
Mechanism: dOI / traded volume estimates the fraction of volume that opened or closed positions; high ratio during moves = conviction; low ratio = churn among existing holders.
Features: tau_t = |dOI_coin| / volume_coin over 15m.
Target: whether trend persistence after breakouts depends on tau.
Falsify-if: tau gives no information beyond volume and volatility.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B+

## W71K-E41 — Hyperliquid OI-Cap Binding State
Primary source: Hyperliquid info `perpsAtOpenInterestCap` (listed in perpetuals info endpoint); info `perpDexs` `assetToStreamingOiCap` (HIP-3).
Mechanism: when a market is at its OI cap new risk-increasing orders are rejected on the capped side/total, so premium and funding must absorb excess demand instead of OI; price-discovery changes from quantity to price adjustment.
Features: capped flag, time at cap, funding level during cap, volume/OI during cap.
Target: funding and premium behaviour while capped; spillover to other venues' premiums.
Falsify-if: premium/funding behaviour while capped equals matched uncapped high-OI episodes. Exact cap semantics (which side) PROVENANCE_PENDING.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E42 — Account-Count Long/Short Ratio vs Funding Divergence (Retail Crowd Gauge)
Primary source: Binance `/futures/data/globalLongShortAccountRatio` (5m min, 30 days, fields longShortRatio, longAccount, shortAccount), Bybit `/v5/market/account-ratio` (periods 5min..1d, buyRatio/sellRatio; history since 2020-07-20).
Mechanism: account-count ratio reflects the number of traders, not notional; when account ratio is extreme while funding/premium is neutral, small accounts lean one way without capital behind it. Divergence between account and notional views identifies retail crowding.
Features: z(account_ratio) minus z(funding); cross-venue agreement Binance vs Bybit.
Target: forward 1h return skew; reversal frequency.
Falsify-if: no information beyond funding; sign ambiguity (contrarian vs momentum).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E43 — Top-Trader vs Global Positioning Divergence
Primary source: Binance Top-Trader Long/Short Ratio endpoints (docs page "Top-Trader-Long-Short-Ratio" present in market-data list; fields and definition NOT verified — PROVENANCE_PENDING) vs global account ratio (verified in E42).
Mechanism: if the top-trader ratio (by position or account) diverges from the global ratio, larger/better-capitalised accounts are positioned opposite to the crowd.
Features: ratio_top - ratio_global z-score; persistence.
Target: forward return alignment with the top-trader side.
Falsify-if: no alignment after controlling for price momentum; definition change by exchange invalidates series — version.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E44 — Cross-Venue OI Migration (Offshore vs Onshore vs CME)
Primary source: Hyperliquid/Binance/Bybit/OKX OI (above); CME volume and OI (https://www.cmegroup.com/market-data/volume-open-interest.html, per W3-E64 source); Coinversa `pulse_exchange_oi` (third-party).
Mechanism: OI share shifting between venue classes reveals which participant group is adding risk (offshore speculators vs regulated institutions); transmission to equity-index risk differs by group.
Features: share_HL, share_Bin, share_CME changes over 1h/1d; CME OI is end-of-day so intraday uses only offshore.
Target: forward vol and basis. Increment over W3-E65: adds Hyperliquid and 24/7 CME (E47) and intraday resolution on offshore legs.
Falsify-if: migration shares add no information beyond total OI and funding.
Horizon: DAILY
Availability: PUBLIC_BATCH
Priority: B

## W71K-E45 — Coin-Denominated vs USD OI Mechanical Inflation Filter
Primary source: Binance openInterestHist fields sumOpenInterest (coin) and sumOpenInterestValue (USD).
Mechanism: USD OI rises when price rises with no new positions; models using USD OI mistake price for leverage growth.
Features: dOI_USD_residual = dOI_USD - P*dOI_coin; comparison of signals built from each.
Target: show whether coin-OI-based quadrant (E39) outperforms USD-OI version; a data-hygiene edge that changes sign classification in rallies.
Falsify-if: signals identical (then simplify). This is a control for E39/E40/E28.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

---

## Block F — Cross-venue basis and regulated-venue structure

## W71K-E46 — CME 24/7 Weekend Trading: Gap Removal and Weekend Price-Discovery Handoff
Primary source: CME Group press coverage (https://cmegroupinc.gcs-web.com/node/55391/pdf; theblock.co 2026-02; CME release 2026-06-01 via search) — 24/7 crypto futures and options trading live from 4:00 p.m. CT Friday 2026-05-29; minimum two-hour weekend maintenance window; weekend/holiday trades get the next business-day trade date; first weekend ~7,200 contracts (~$50M notional). Primary CME notice itself not read — PROVENANCE_PENDING.
Mechanism: before 2026-05-29 CME BTC had weekend gaps; now regulated futures price discovery continues through weekends, so Sunday-evening NQ/ES open conditioning can use CME BTC/MBT drift plus offshore perps. Data conventions change: trade-date stamping differs from calendar date.
Features: weekend CME BTC return, CME-vs-perp weekend basis, maintenance-window gaps.
Target: Sunday 18:00 ET NQ/ES opening gap sign/size; Monday-open BTC-NQ correlation.
Falsify-if: weekend BTC return has no explanatory power for NQ opening gap after the regime change vs pre-change sample (structural break test, M-series); small weekend volume implies low reliability.
Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W71K-E47 — HIP-3 Index/Commodity Perps as Off-Hours Shadow Prices for NQ/ES/Gold
Primary source: Hyperliquid `perpDexs` info (verified), Margining doc (HIP-3 DEX margin modes), Coinversa Pulse description of builder dexes (xyz: stocks/commodities/indices/FX such as xyz:GOLD; mkts: US500, USTECH; third-party description, checked 2026-09-23 — PROVENANCE_PENDING for the official HIP-3 spec, whose page URL did not resolve in my fetch).
Mechanism: HIP-3 markets trade 24/7 collateralised in USDC; when CME equity-index/gold futures are closed or thin (weekends, daily halts, holidays), HIP-3 mids are a market-implied shadow price whose gap to the Friday close predicts the next open. Oracle design is deployer-defined, so quality varies.
Features: shadow_gap = hip3_mid(t) / last_cme_settle - 1; oracle freshness; OI and spread of the HIP-3 market.
Target: Sunday-evening and early-Asia NQ/ES/GC move; fraction of CME open gap explained. Compare against equal-time-lag placebo (previous week's gap).
Falsify-if: shadow_gap explains < theta of the open gap vs naive Asian-session index futures (NK/HSI) benchmark; deployer oracle may simply track CME futures when open (then it is derivative, no independent information while CME is open).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: S-

## W71K-E48 — Perp-vs-Spot-Index Lead/Lag by Regime (Binance vs Uniswap v2; CME vs Spot)
Primary source: arXiv 2506.08718 "Price Discovery in Cryptocurrency Markets" (https://arxiv.org/abs/2506.08718): Binance generally leads Uniswap v2 for ETH in five 2024 event windows; BTC spot vs CME futures shows mixed results in high volatility (search summary; full paper tables not read).
Mechanism: information share varies by volatility and event type; a state classifier of "who leads right now" decides which venue to use for entry confirmation and which to treat as lagging price.
Features: rolling Hayashi-Yoshida cross-correlation lead (asynchronous), information share proxy per 15-min window.
Target: leader identity stability; improvement of forward 1-minute return prediction using leader's last-minute return.
Falsify-if: leader identity not persistent beyond one window; lead of venue disappears after latency alignment (clock sync is the main trap).
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: A-

## W71K-E49 — Annualised Basis vs Funding Consistency Residual
Primary source: Binance `/futures/data/basis` (periods 5m..12h, 30 days, fields basis, basisRate, annualizedBasisRate, futuresPrice, indexPrice, contractType), funding series (E01).
Mechanism: dated-futures basis and perpetual funding price the same leverage demand; their no-arbitrage relation (Ackerer-Hugonnier-Jermann, arXiv 2310.11771) implies consistency up to interest and cost terms.
Features: resid = annualizedBasisRate(quarterly) - 3*365*mean_funding_8h over matched horizon.
Target: resid mean reversion; sign of future perp premium change.
Falsify-if: resid is within transaction-cost band; need to account for settlement differences (USDT vs coin-margined).
Horizon: DAILY
Availability: PUBLIC_REALTIME
Priority: B+

## W71K-E50 — No-Arbitrage-Bound Violation Intensity (He-Manela-Ross-von Wachter)
Primary source: arXiv 2212.06888 (https://arxiv.org/abs/2212.06888v6): no-arbitrage prices and bounds with trading costs for perpetual futures; deviations in crypto much larger than in FX, comove across coins, and diminish over time.
Mechanism: perp price minus implied no-arb price, beyond a cost band, is a mispricing; co-movement across coins means a common (market-wide) component.
Features: dev_i,t; cross-sectional common component (PC1); band = fees + half-spread.
Target: reversion horizon of deviation beyond band, intraday; PC1 as a market-wide leverage-demand index.
Falsify-if: after-cost reversion not significant in the post-2024 period (paper says deviations shrank over time). Intraday evidence is the increment over the paper's mostly daily analysis.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B+

## W71K-E51 — Spot-Index Premium on Regulated US Venues (US-Hours Coinbase-Type Premium)
Primary source: hypothesis; requires a US-regulated spot venue API (e.g. Coinbase Exchange) vs offshore perp index — API documentation not read in this wave: PROVENANCE_PENDING. Aligns with W3-E66.
Mechanism: US-hours demand (including ETF-related hedging) shows up as spot premium on US venues relative to offshore index; premium flips during Asia hours.
Features: premium_bps (US spot - offshore index), time-of-day-adjusted z-score.
Target: forward BTC return and NQ co-movement in the US cash session.
Falsify-if: premium has no information beyond offshore perp returns; time-of-day control mandatory.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E52 — CME BTC/MBT vs Offshore Perp Basis at the US Cash Open
Primary source: CME BTC contract spec facts from 2017 filing (5 BTC; tick $5; special price limits 7%/13%/20% with 2-minute cooling — launch-era, UNVERIFIED for 2026; verify at https://www.cmegroup.com/markets/cryptocurrencies/bitcoin/bitcoin.contractSpecs.html which returned 503), MBT 0.10 BTC multiplier.
Mechanism: the CME futures are regulated, margin-based and priced through BRR; at 09:30 ET equity open and during US data prints, basis relative to offshore perps can shift abruptly as institutions (ETF-hedgers, basis traders) rebalance.
Features: CME mid minus offshore index-implied fair value (carry-adjusted), change around 09:30 and 08:30 ET releases.
Target: whether basis jumps at scheduled US releases predict the next 15m BTC move and NQ move. Increment over W3-E64: event-time resolution, using CME 24/7.
Falsify-if: basis jumps equal those at placebo times; need synchronized clocks.
Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

---

## Block G — Microstructure, clocks and engine-specific mechanics

## W71K-E53 — Block-Synchronous BBO Clock (Event-Time Alignment)
Primary source: Hyperliquid Websocket subscriptions doc: `bbo` updates are sent only if the BBO changes on a block; `l2Book`, `trades`, `activeAssetCtx`; also `fastAssetCtxs` subscription.
Mechanism: HL's market state changes on blocks (not per message); using wall-clock features across venues mixes block-clock and continuous-clock venues, creating spurious lead/lag.
Features: block height index; per-block book change count; per-block trade imbalance.
Target: re-estimate lead/lag with HL block as clock; check whether HL appears to lag CEX by less than one block.
Falsify-if: lead/lag estimates do not change when block-aligned; otherwise the alignment is mandatory in all cross-venue HL features.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B+

## W71K-E54 — Bybit 100ms Delta Ticker: Mark/Index/Funding Event Stream
Primary source: Bybit v5 WebSocket ticker (https://bybit-exchange.github.io/docs/v5/websocket/public/ticker): 100ms push for derivatives; snapshot/delta with absent fields unchanged; fields markPrice, indexPrice, fundingRate, nextFundingTime, openInterest, basisRate, predictedDeliveryPrice.
Mechanism: field-level change events (mark jump without index jump; OI jump) are clean event markers with exchange-stamped time.
Features: inter-event times of markPrice vs indexPrice updates; OI step sizes (large OI steps in a delta message ≈ large position open/close).
Target: order-flow shock detection: large OI step predicts short-term price drift.
Falsify-if: OI step predictions vanish after conditioning on concurrent trade imbalance.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B+

## W71K-E55 — HLP Vault Inventory as Counterparty-Pressure State
Primary source: Hyperliquid Protocol vaults doc (https://hyperliquid.gitbook.io/hyperliquid-docs/hypercore/vaults/protocol-vaults): HLP provides liquidity via multiple market-making strategies, performs liquidations, accrues fees; 4-day deposit lock-up. Vault position API not read — PROVENANCE_PENDING.
Mechanism: HLP is a large passive counterparty; its net inventory after backstop liquidations and market making is a state for forthcoming skewed quoting/liquidation of its own inventory.
Features: HLP net position by coin (public on-chain), change over 1h, relation to premium.
Target: premium and short-term return conditional on HLP inventory extremes.
Falsify-if: no relation after controlling for OI/funding.
Horizon: INTRADAY
Availability: UNKNOWN_MEASURED
Priority: B

## W71K-E56 — Hyperliquid Historical Archive Lag and Requester-Pays Data Governance
Primary source: Hyperliquid Historical data doc (https://hyperliquid.gitbook.io/hyperliquid-docs/historical-data): S3 hyperliquid-archive (L2 book snapshots, asset contexts) updated approximately monthly, no guarantee of timely updates or completeness, requester pays; node fills/trades (`hl-mainnet-node-data/node_fills_by_block`), explorer blocks, misc events (funding, transfers).
Mechanism: historical edges built on archives are subject to missingness and delayed availability; live edges need self-recorded streams. Data-engineering edge: continuous self-archiving beats archive dependency.
Features: archive coverage ratio per day; gap detection.
Target: quantify how many research windows have complete L2 + asset-ctx coverage; decide which E-items can be backtested at all.
Falsify-if: coverage is complete for the chosen windows (then proceed); otherwise mark items live-forward-only. Governance item, not an alpha claim.
Horizon: SLOW_PRIOR
Availability: PUBLIC_BATCH
Priority: A-

## W71K-E57 — Liquidation Bankruptcy-Price Gap (Bybit `p`) vs Mark
Primary source: Bybit allLiquidation field `p` = bankruptcy price; OKX liquidation-orders `bkPx` (liquidation mark price) and `bkLoss` (bankruptcy loss).
Mechanism: distance between bankruptcy price and the actual market price at liquidation shows how much margin buffer was consumed; large negative-equity-at-liquidation increases insurance-fund draw and ADL risk.
Features: sum over bursts of bkLoss; ratio of bkLoss to notional.
Target: insurance-fund draw proxy; predicts E33/E34 state transitions.
Falsify-if: bkLoss accumulation does not precede OKX warning state; OKX data are not exhaustive, so lower bounds only.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E58 — Funding-Time-of-Day Seasonality vs Equity Session Overlap
Primary source: Hyperliquid fundingHistory (hourly), Binance 00/08/16 UTC schedule, CME BRR window (15:00-16:00 London).
Mechanism: premium (hence funding) is plausibly time-of-day dependent because liquidity providers and US/EU/Asia flows change through the day; separating funding level seasonality from signal avoids mislabelling normal session variation as crowding.
Features: hour-of-day mean/dispersion of premium; deseasonalised premium.
Target: improvement in E01/E05 features after deseasonalisation.
Falsify-if: no improvement. Pure hygiene control for all funding-based edges.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E59 — Deribit DVOL Intraday Change vs Perp Stress (Options-Venue Cross-Check)
Primary source: Deribit `public/get_volatility_index_data` (https://docs.deribit.com/api-reference/market-data/public-get_volatility_index_data; candle data, resolution parameter in seconds as shown in examples — field semantics PROVENANCE_PENDING).
Mechanism: DVOL moves with option demand; perps stress often leads option-implied vol repricing or vice versa; joint state distinguishes "leverage unwind" (perp stress, flat DVOL) from "hedging panic" (DVOL up, perp calm).
Features: dDVOL 15m, funding z, liquidation composite.
Target: 2x2 state forward vol of BTC and NQ. Increment over W3-E68 and W77 (vol products): perp-microstructure cross-state.
Falsify-if: 2x2 states give no distinct forward distributions.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

## W71K-E60 — Weekend and Holiday Thin-Liquidity Funding Distortion
Primary source: CME 24/7 notice (weekend trades dated next business day), perp funding series; HL L2 depth.
Mechanism: during weekends, depth in offshore perps thins while macro information is stale; funding/premium noise and liquidation susceptibility rise (E06 fragility).
Features: weekend flag, depth ratio, premium noise.
Target: liquidation frequency per unit move, weekend vs weekday.
Falsify-if: no excess liquidation sensitivity after depth control.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: B

---

## Final architecture edge (Truth Ladder)

## W71K-E61 — Perp Microstructure State Vector and Truth Ladder
The Truth Ladder for W71K: (1) rule/spec fact versioned by effective date and exact doc page snapshot (funding formula, clamps, intervals, mark legs, liquidation sizes, ADL sort index, margin tiers); (2) raw venue streams recorded with exchange time and our receive time, message-complete (WS reconnect gap accounting); (3) exact rule reconstruction (premium, funding, mark, liquidation price, ADL index) reconciled to venue-published values to within tolerance; (4) state variables (band_state, pending mark revision, slice schedule, cascade composite C_t, insurance-fund state, OI quadrant) with named placebo and sign-ambiguity notes; (5) conditional distributions of intraday outcomes relative to matched controls, calibrated out-of-sample with the vault's intermediate-outcome promotion gate; (6) only then any trading-rule or net-of-cost return claim. This is a conditioning layer for crypto exposure and a cross-asset risk gate, not a standalone signal.
Horizon: INTRADAY
Availability: PUBLIC_REALTIME
Priority: S

## Highest-priority W71K tests

1. W71K-E47 HIP-3 Index/Commodity Perps as Off-Hours Shadow Prices for NQ/ES/Gold
2. W71K-E13 Pending Mark Revision (Oracle Staleness Gap)
3. W71K-E22 Partial-Liquidation Slice and 30-Second Cooldown Schedule
4. W71K-E24 Liquidation Notional to Book-Depth Ratio and Reversal
5. W71K-E33 OKX ADL-Warning State Machine
6. W71K-E26 Multi-Venue Cascade Composite (OI-Normalised)
7. W71K-E21 Liquidation Price Cluster Proximity (Public-Position Heatmap)
8. W71K-E46 CME 24/7 Weekend Trading: Gap Removal and Weekend Price-Discovery Handoff
9. W71K-E05 Cross-Venue Predicted-Funding Dispersion
10. W71K-E28 Post-Cascade OI Flush Completion
