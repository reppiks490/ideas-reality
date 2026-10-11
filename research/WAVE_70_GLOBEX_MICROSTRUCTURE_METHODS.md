# Wave 70B — Research Methods

Namespace: **W70B**

## W70B-M01 — Event-boundary timing
Compute any book feature only after MatchEventIndicator bit7=1 for the event; never mid-event. Store per-message and per-event versions for comparison.

## W70B-M02 — Four clocks
Preserve TransactTime, SendingTime, capture ts_recv and decision time; decision-legal data requires ts_recv <= decision_time. Never use TransactTime as availability.

## W70B-M03 — Sequence integrity
Track RptSeq gaps per instrument; reconstruct book from snapshot+incrementals; mark windows with gaps invalid for backtest and live gate.

## W70B-M04 — Instrument identity / roll mapping
SecurityID is not reused until next trade date after expiry; map continuous series by explicit roll rule (volume crossover), versioned. No back-adjusted prices for microstructure.

## W70B-M05 — Rule versioning
Version tick, NRR/protection points, price limits, trading hours, SMP and MEP rules by effective date. A backtest on 2022 data must use 2022 parameters.

## W70B-M06 — Leakage: imbalance and queue
Queue ahead and imbalance must use state before the order arrival time (minus measured latency). Fill labels must not use post-fill queue information.

## W70B-M07 — Aggressor sign handling
Use native AggressorSide; set no-aggressor prints (value 0) to unsigned and report sensitivity; never fill unsigned prints with tick rule silently.

## W70B-M08 — Iceberg inference hygiene
Aggregate-level inference only; no identity or participant attribution. Report false-positive rate via synthetic injection of hidden size into replay.

## W70B-M09 — Placebo levels
For level-based edges (defended levels, stop clusters) use matched placebo levels: same distance from touch, same time-of-day, same prior volume, non-round and round variants.

## W70B-M10 — Placebo timestamps
For event studies shift event times by random offsets within same session to create timestamp placebos; preserve event clustering.

## W70B-M11 — Negative control: side swap
For directional features swap sides labels; signal must vanish. For refill asymmetry, swap bid/ask.

## W70B-M12 — Multiplicity control
Count each instrument x horizon x state bucket as a test; control FDR (BH) at pre-registered level; keep terminal holdout unexposed to adaptive search.

## W70B-M13 — Walk-forward / purge
Purged, embargoed walk-forward by day; embargo >= max horizon plus latency; no cross-day queue state leakage.

## W70B-M14 — Latency realism
Replay with measured decision-to-arrival latency distribution; sub-microsecond ordering across instruments is disallowed (W70B-E48).

## W70B-M15 — Fill simulator validation
Validate fill simulators against live shadow fills by queue rank before trusting passive results; report reality gap.

## W70B-M16 — Regime stratification
Report all results by session segment (Asia, Europe, RTH open, midday, close, settlement window), by spread-ticks regime, by depth percentile.

## W70B-M17 — Rule-text verification gate
Any rule-dependent edge (Rule 534/575, SMP, MEP, NRR) is capped at B until the rule text itself (not a summary) is archived with hash.

## W70B-M18 — Compliance edges are not alpha
E26-E30 and E61 are compliance/operations edges; never include them in PnL attribution or alpha search.

## W70B-M19 — Data licensing
MDP 3.0 and derived data are licensed; do not redistribute raw messages; store derived features only where license permits (Databento/CME terms to be reviewed).

## W70B-M20 — Versioned archive
Archive each fetched spec page with content hash and retrieval time; CME wiki pages carry 'Updated' stamps and can change without notice.

## W70B-M21 — Intermediate-outcome promotion gate
Promotion requires: stage-3 intermediate outcome effect vs placebo, stage-4 execution-quality improvement OOS in >=2 non-overlapping quarters, then live shadow of at least 20 sessions.

## W70B-M22 — Instrument transfer
Do not assume ES results hold for NQ/GC/ZN/CL; test per instrument, per tick regime; micro contracts separate.

## W70B-M23 — Sign ambiguity register
Each edge with ambiguous sign (implied share, micro flow share) is tested two-sided with the sign fixed only on training folds.
