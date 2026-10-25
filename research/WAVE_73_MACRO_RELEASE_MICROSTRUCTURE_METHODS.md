# Wave 73E — Research Methods

Namespace: **W73E**

## W73E-M01 — Three-Clock Discipline

Store event_time (scheduled release instant), published_time (first public instant observed), ingested_time (our parse time) for every release. Features are legal only if published_time <= decision_time. Use exchange timestamps for the tape and NTP/PTP-disciplined clocks locally; record clock offset.

## W73E-M02 — Calendar Point-in-Time Snapshots

Snapshot BLS, BEA, Census, Fed, ECB, BoE and BoJ calendars at least daily with content hash. Backtests read the snapshot with published_time <= decision_time, never the current calendar. Record reschedules and cancellations (see 2025 shutdown precedent).

## W73E-M03 — First-Print Vintage Storage

Store the first-published value of each series and every later revision as separate vintages. Targets built on revised values are labelled revision studies only. Consensus is the last pre-release snapshot.

## W73E-M04 — Consensus Licensing Boundary

Consensus feeds are licensed. Record vendor, field, collection time, and rights status; if unlicensed, the edge is research-only and cannot promote. Do not scrape.

## W73E-M05 — Surprise Standardization Rule

Surprise sigma uses only prior events (expanding or rolling window, current event excluded). Report results for raw difference and z-score. Handle series with unit changes, base-year changes and methodology breaks via explicit regime breaks.

## W73E-M06 — Event-Window Definition Grid

Pre-register windows (pre: -30m,-5m,-60s,-10s; post: 0-1s,0-5s,0-60s,0-5m,5-15m,15-60m). Do not choose windows after seeing results. Use event time, not wall time.

## W73E-M07 — Placebo Clock Construction

For each release build matched placebo timestamps: same weekday and minute-of-day in non-release weeks, same holiday adjacency, same prior-day range tercile. Effects must exceed placebo distribution.

## W73E-M08 — Negative-Control Events

Use day one of two-day FOMC meetings, GDP second/third estimates, BoJ minutes and summaries as negative controls whose effect should be small. A model that fires on them is mis-specified.

## W73E-M09 — Latency Budget and Race Realism

For first-print strategies measure end-to-end latency (source to parsed value to order). Edges requiring sub-second response are marked execution-bound and fail unless measured latency beats the first displacement in the target share of events.

## W73E-M10 — Timezone and DST Handling

All schedule math uses IANA tz database. Release times are stored with source timezone and converted at event date. Test across US-EU DST misalignment weeks and the Japan no-DST case.

## W73E-M11 — Multiple-Testing Control

Edges share the same events; control FDR across release types and windows (e.g., Benjamini-Hochberg or reality-check/SPA). Report the number of window-asset-release combinations tried.

## W73E-M12 — Few-Events Power Rule

Monthly releases give about 12 events a year. Pool across tiers only with explicit hierarchical model; report effective sample size; require minimum N occurrences before any promotion.

## W73E-M13 — Purged Walk-Forward With Event Embargo

Purge observations within +/- the longest evaluation window of each event; embargo equal to window plus decay half-life h. Terminal holdout consumed once.

## W73E-M14 — Overlapping Event Handling

When two events overlap (E03 collisions, central bank clusters) treat as a single composite event or include interaction terms; never double count returns.

## W73E-M15 — Sign-Ambiguity Declaration

Every directional edge pre-registers two-sided tests; report sign by regime. No sign is assumed. Continuation versus reversal are separate hypotheses.

## W73E-M16 — Cost Model at Event Times

Use event-time spreads and slippage, not average-day costs; apply cost multipliers by tier from measured spread ratios. Include data/parse cost and failed fills.

## W73E-M17 — Regime Break Registry

Maintain a registry of structural breaks: end of lock-ups June 2020, pre-FOMC drift disappearance after 2015 (Kurov et al.), shutdown data gaps late 2025, FOMC communication changes. Fit pre/post separately.

## W73E-M18 — Survivorship of Release Series

Series are discontinued or redefined; keep a series_id map with effective dates. Test only on series live at decision time.

## W73E-M19 — Missing and Cancelled Event Treatment

Cancelled or delayed releases are events themselves; do not impute zeros. Label as MISSING_EVENT and test market response to the cancellation notice.

## W73E-M20 — Cross-Wave Collision Check

Before promotion, check overlap with W75A-E16..E19 (FOMC text and gate), W70B (book), W77 (vol products), W78B (execution), W55 (Treasury financing). Declare the incremental information over each.

## W73E-M21 — Promotion Gate (Intermediate Outcomes)

Promotion requires: (1) event-window effect beating placebo, (2) stability across regimes with pre-registered splits, (3) cost-adjusted improvement in a gate or execution metric (slippage tail, adverse selection) rather than only P&L, (4) live shadow evidence on at least a pre-set number of events, (5) multiple-testing control. Intermediate outcomes (gate accuracy, time-in-state error) must pass before P&L is evaluated.

## W73E-M22 — Rights and Confidentiality Boundary

Only lawfully public data. No inference about identities of traders or lockup participants. Pre-release informed-trading studies are aggregate statistical tests of public tape only.

## W73E-M23 — Replication Package

Each edge ships code, parameter list, calendar snapshot hash, and consensus vendor snapshot id so results are reproducible and not re-tuned on the holdout.
