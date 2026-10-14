# Wave 71K — Research Methods

Namespace: **W71K**

## W71K-M01 — Rule Snapshot Versioning
Store a dated snapshot (hash + retrieval time) of each venue doc page used (funding, mark, liquidation, ADL, margin tiers). Hyperliquid pages show "Last updated" stamps; Binance changed intervals in 2025-05 and 2026-01. Backtests use the rule in force at event time, never the current page.

## W71K-M02 — Three-Clock Contract
Every message stores exchange time `t`, our receive time `rx`, and decision time. Features at decision time D use only messages with rx <= D. Hyperliquid state is block-clocked (M03).

## W71K-M03 — Block Clock for Hyperliquid
Index HL events by block height; `bbo` updates only fire when BBO changes on a block. Cross-venue lead/lag is estimated after aligning to block time and again on wall-clock; report both.

## W71K-M04 — Exact Rule Reconstruction Before Prediction
Reconstruct premium, funding, mark, liquidation price and ADL index from raw inputs and reconcile to venue-published values (e.g. `metaAndAssetCtxs` funding/premium/markPx). Do not trade a feature whose reconstruction error exceeds tolerance.

## W71K-M05 — Funding Unit Normalisation
Normalise every funding rate to per-hour using the symbol's current interval (Hyperliquid 1h, Binance 1/4/8h dynamic, Bybit per-symbol, OKX per-instrument). Never assume 8h. Record interval changes as events.

## W71K-M06 — Stream Completeness Accounting
Log WebSocket reconnects, sequence gaps, and heartbeat ages. Event-driven feeds (OKX adl-warning, liquidation streams) must distinguish TRUE_ZERO from SOURCE_DOWN using a liveness probe on a sibling channel.

## W71K-M07 — Liquidation Feed Censoring Correction
Binance forceOrder keeps one latest event per symbol per 1000ms; OKX liquidation feed is non-exhaustive and unordered; Bybit allLiquidation pushes snapshots every 500ms. Treat all as censored samples; report saturation fraction; never sum raw notional across venues without calibration.

## W71K-M08 — Coin-Denominated Open Interest
Use coin-denominated OI for dynamics; USD OI only for size-weighting. Show results for both to expose mechanical inflation (E45).

## W71K-M09 — Overlapping-Window Inference
Intraday outcomes at 5m/15m/60m horizons overlap; use block bootstrap by day or clustered standard errors by cascade episode. Cascades are few and clustered — effective sample size is episodes, not minutes.

## W71K-M10 — Event Definition Pre-Registration
Define cascade/burst/warning events with parameters (theta, window) frozen before outcome inspection; parameter grid reported in full; no post-hoc threshold selection.

## W71K-M11 — Matched Controls
Each event study uses controls matched on time-of-day, realised volatility decile, day-of-week (weekend flag), and OI decile. Minute-matched controls for clock-based edges (E03, E17).

## W71K-M12 — Named Placebos
Required: time-shifted clocks (+17 min), shuffled band edges (E01), levels shifted by random ATR multiples (E21), stale-oracle gap (E13), previous-week gap (E47), volume-matched non-liquidation bursts (E24).

## W71K-M13 — Sign-Ambiguity Registry
For each edge store both candidate signs (momentum vs exhaustion; squeeze vs capitulation) before testing; report which cell is two-sided significant out of sample. No sign is chosen post hoc.

## W71K-M14 — Structural Break Handling
Known breaks: Binance interval rule (2025-05-02; 2026-01-02), CME 24/7 (2026-05-29), spot-ETF in-kind (2025-07-29, see W79), Hyperliquid HIP-3 launch, Oct 10-11 2025 cascade. Fit models separately across breaks; test for stability with pre/post splits.

## W71K-M15 — Cross-Asset Gate Evaluation
Crypto-to-index gates (E29, E46, E47) evaluated against NQ own-vol, scheduled-news dummies and VIX-futures state as baselines. Gate must improve a pre-registered loss (risk-adjusted drawdown or abnormal-move detection AUC) over baseline to proceed.

## W71K-M16 — Execution Realism for Perp Features
Features requiring sub-second reaction (E13, E22, E24) need latency-adjusted backtests: add measured round-trip delay from collection to order acknowledgement; lag the signal by that amount and by 2x.

## W71K-M17 — Rights and Licensing Check
Before ingest: record ToS/rights status per source. Third-party aggregators (Coinversa Pulse, CoinGlass-type) are treated as derived, non-authoritative; prefer primary venue streams. CF BRTI real-time requires licence.

## W71K-M18 — Third-Party Data Provenance Rule
Any figure from blogs, news or aggregators (e.g. Oct 2025 cascade size) is labelled secondary and cannot enter a promotion decision.

## W71K-M19 — Rare-Event Sample-Size Gate
ADL, backstop, hyperp conversion and cascade events are rare: require minimum episode count (parameter) before any hypothesis moves beyond RESEARCH; otherwise label CASE_STUDY and exclude from signal portfolios.

## W71K-M20 — Archive Dependence Audit
Hyperliquid S3 archives update ~monthly, requester-pays, completeness not guaranteed; Binance OI/ratio endpoints retain 30 days. Classify each edge LIVE_FORWARD_ONLY or HISTORICAL_OK and start recorders before testing.

## W71K-M21 — Cost Model for Perp Edges
Use venue fee schedules and measured impact; include funding paid over holding window (E12) and bid/ask crossing. Use He-Manela-Ross-von Wachter style cost bands when judging mispricing.

## W71K-M22 — Intermediate-Outcome Promotion Gate
Stages: replicates reconstruction (M04) -> state distribution stability -> conditional outcome difference vs matched/placebo controls -> out-of-sample/time-split -> cost-aware decision-level test -> paper/shadow. Failure at any stage kills or downgrades; kills are logged as successes.

## W71K-M23 — Information Leakage Traps
Typical leaks: using final hourly funding in features before the hour ends; using post-hoc "settled" fields (OKX settFundingRate) before settlement; revised OI history; archive timestamps vs receive times; aggregator back-filled series.

## W71K-M24 — Universe and Symbol Hygiene
Symbols are delisted/renamed; HIP-3 assets change by deployers; Binance contract types differ (perpetual vs quarterly). Store universe snapshot per day; include delisted symbols in cross-sectional tests.
