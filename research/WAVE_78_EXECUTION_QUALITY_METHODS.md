# Wave 78B — Research Methods

Namespace: **W78B**

## W78B-M01 — Decision-time clock
Decision price is the mid/micro-price at the legal decision timestamp (feed ts_recv <= decision); arrival price at order send; never use fill-time information in benchmarks.

## W78B-M02 — Benchmark pre-registration
Pre-register arrival benchmark (mid default, micro-price alternate) before analysis; report sensitivity per W78B-E02.

## W78B-M03 — Fill reconciliation
Reconcile own execution reports to exchange statements daily; unreconciled fills excluded and counted.

## W78B-M04 — Markout horizons
Fix markout horizons {1s,5s,30s,300s} in advance; use mid at event commit boundaries (W70B-M01).

## W78B-M05 — Role labeling
Label each fill maker/taker from aggressor flag and our order type at arrival; accidental takers separate.

## W78B-M06 — Counterfactual fill simulation
Use MBO queue reconstruction; fills need queue-ahead exhaustion; validate vs live shadow (reality gap).

## W78B-M07 — Selection bias in passive samples
Passive fills are a selected subset; compare with placebo timestamps and with unconditional drift; use inverse-probability weights where order intent known.

## W78B-M08 — Censoring
Treat unfilled/cancelled intents as censored in survival models; never drop them.

## W78B-M09 — State vector versioning
Version definition of each state variable (spread_ticks, depth_pctile, event_prox); recompute on definition change.

## W78B-M10 — Quantile calibration
Evaluate slippage quantile forecasts by pinball loss and coverage (q90 coverage 0.9 ± tolerance).

## W78B-M11 — Monotonicity diagnostics
Run isotonic monotonicity checks (size, urgency, latency) before using a cost model; failure blocks promotion.

## W78B-M12 — Fee and cost versioning
Version fee tables by effective date and account class; store statement evidence; no current fees applied to past dates.

## W78B-M13 — Rule version control
NRR/protection points, tick sizes, trading hours versioned (W70B-M05).

## W78B-M14 — Latency replay
Replay signals with injected delay distribution from own telemetry; do not assume zero latency or fixed latency.

## W78B-M15 — Randomized A/B in shadow
Where possible compare policies (e.g., schedule randomization) by randomized assignment in live shadow; log assignment.

## W78B-M16 — Control policies
Every decision rule compared to always-aggressive, always-passive and random-gate controls at matched trade counts.

## W78B-M17 — Multiplicity
Count instruments x states x horizons; BH-FDR; terminal holdout untouched by adaptive tuning.

## W78B-M18 — Walk-forward purge
Purged walk-forward by day with embargo covering holding horizon plus latency.

## W78B-M19 — Regime stratification
Report by session segment, roll window, event proximity, depth percentile, spread ticks.

## W78B-M20 — Capacity honesty
Report size in lots and as fraction of L1 depth and 1-min volume; no results without size context.

## W78B-M21 — Intermediate-outcome promotion gate
Promotion: (1) cost model calibrated OOS, (2) decision rule beats controls OOS in >=2 quarters, (3) live shadow >=20 sessions, (4) only then net return claims.

## W78B-M22 — Secondary-source cap
Edges depending on fee or rule values seen only in secondary sources are capped at B+ until the CME primary is archived with hash.

## W78B-M23 — No profitability claims
Reports state cost estimates and diagnostics only; no statement that a policy earns money.
