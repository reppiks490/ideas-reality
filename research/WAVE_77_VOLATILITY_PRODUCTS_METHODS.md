# Wave 77O — Research Methods

Namespace: **W77O**

## W77O-M01 — Three-Clock Timing
Store event_time, source_received/published_time, first_seen_time, ingested_time per DATA_AVAILABILITY_CONTRACTS; decision_time must be >= published_time. Never use SIP/OPRA exchange timestamps as availability.

## W77O-M02 — Vintage-First Storage
Retain raw OPRA/OCC/Cboe files immutable with content hash. Never overwrite a vintage.

## W77O-M03 — Rule-Version Pinning
Version Cboe, OCC, CME and ETP prospectus rules by effective date; apply only rules in force at event_time.

## W77O-M04 — Leakage: Same-Bar Quote/Trade
Quotes at or after trade time must not sign the trade; use last quote strictly before trade timestamp with latency offset.

## W77O-M05 — Leakage: Settlement Values
Do not use end-of-day OI, SOQ, or settlement to condition intraday decisions earlier than published.

## W77O-M06 — Named Placebo Requirement
Each edge must run a named placebo (shuffled strikes, pseudo-expiry days, shifted quotes, shuffled flows) before promotion.

## W77O-M07 — Multiple-Testing Control
Pre-register parameter grids; apply deflated Sharpe/White reality check across all W69O/W77O candidates.

## W77O-M08 — Purged Walk-Forward
Purge and embargo at least one session around expiry/settlement events; terminal holdout used once.

## W77O-M09 — Regime Splits
Report results separately pre/post Cboe daily SPXW expiries (2022) and pre/post 2018-02-27 ETP multiple change.

## W77O-M10 — Parameter-as-Calibrated
Thresholds are parameters to calibrate on training folds only; no value is claimed to work.

## W77O-M11 — Cost and Latency Realism
Include ES/NQ spread, slippage and data-latency distribution; edges using paid feeds must state feed latency.

## W77O-M12 — Sign-Ambiguity Reporting
Every flow-sign inference reports results under all sign conventions and the disagreement state.

## W77O-M13 — Coverage Bias Note
Cboe Open-Close covers Cboe only; document venue coverage per product and do not generalize.

## W77O-M14 — Confidentiality Boundary
Use only public/licensed data; never infer identities of specific participants or use non-public data.

## W77O-M15 — Missingness Taxonomy
Distinguish TRUE_ZERO, SOURCE_STALE, SOURCE_DOWN, ACCESS_DENIED; do not forward-fill indefinitely.

## W77O-M16 — Intermediate-Outcome Promotion Gate
Before financial alpha require improvement in intermediate outcomes (e.g., hedge-flow estimate vs observed flow proxy, variance forecast) then conditional strategy outcome.

## W77O-M17 — Estimator Robustness
Compare alternative estimators (RV kernel vs 5-min; gamma flat IV vs per-strike) and report dispersion.

## W77O-M18 — Reproducibility Hashing
Hash configuration, code version and input vintages per run.

## W77O-M19 — Kill Criteria
Kill an edge when placebo reproduces the effect or when sign instability exceeds a pre-set tolerance.

## W77O-M20 — Primary-Source Status
Mark any fact from secondary sources UNVERIFIED and source status PROVENANCE_PENDING until the primary artifact is read.

## W77O-M21 — Data Rights Gate
Production use requires explicit rights status for OPRA, CME, Cboe LiveVol, ETP data; scientific validity is not production rights.

## W77O-M22 — Live Shadow
Run live shadow logging for >= pre-set number of sessions before any capital use.
