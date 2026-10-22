# Negative Controls and Adversarial Tests

These tests are intended to kill false edges.

## N01 — Timestamp permutation
Randomly shift source timestamps within a realistic window. A genuine causal signal should degrade.

## N02 — Future-time trap
Deliberately include an obviously future-only field in a sandbox model. The validation harness must detect/block it.

## N03 — Publication-lag inflation
Add conservative latency beyond documented publication. Measure edge decay.

## N04 — Revision trap
Compare first-release vintage versus latest revised history. Large performance gains only in revised data are disqualifying for live claims.

## N05 — Wrong-market placebo
Test the feature on economically unrelated instruments. Broad significance everywhere suggests hidden market beta or leakage.

## N06 — Wrong-geography placebo
For physical data, remap a shock to unrelated regions/facilities.

## N07 — Wrong-time-of-day placebo
Apply intraday microstructure feature at time windows where its mechanism cannot operate.

## N08 — Sign inversion
If both original and sign-inverted strategy look profitable under different tuning, suspect search overfit.

## N09 — Random-label challenge
The research pipeline should not discover persistent alpha against randomized labels at the claimed false-discovery rate.

## N10 — Synthetic-spurious feature
Inject a feature correlated in training but structurally broken in validation. Check whether selection rejects it.

## N11 — Source outage
Drop random blocks of source data. Confirm fail-closed behavior and no accidental forward-fill across long outages.

## N12 — Duplicate-event attack
Duplicate filings/trades/alerts and confirm event identity prevents double counting.

## N13 — Clock skew
Shift one source timezone/DST handling. Integration tests must catch impossible ordering.

## N14 — Market-close boundary
Ensure after-hours filings/events never appear in same-session features before availability.

## N15 — Cross-fold label contamination
For each label, explicitly assert label_end_time < next-fold train boundary.

## N16 — Same-interval causality trap
Do not let a feature and target use information from the same interval unless the decision point is strictly inside the interval and inputs are proven available.

## N17 — Selection-count audit
Recompute statistical evidence using the number of hypotheses actually searched, not the number finally reported.

## N18 — Regime leave-one-out
Discover on all-but-one regime; test on held-out regime. Repeat.

## N19 — Year leave-one-out
Useful for slow physical/macro features.

## N20 — Event-family leave-one-out
For weather/disasters/auctions, hold out entire event families, not random observations.

## N21 — Counterfactual event date
Move historical event dates to nearby non-event days preserving weekday/time. Signal should disappear.

## N22 — Forecast-vintage integrity
For forecast features, reconstruct only the forecast value available at each historical decision timestamp.

## N23 — Availability vs event-time gap
Features must key off publication/availability, never only event time.

## N24 — Data snooping kill switch
Once terminal holdout is exposed, lock the campaign. Further tuning creates a new campaign ID.

## N25 — Latency monotonicity
Edge strength should generally decay as latency increases. Non-monotonic anomalies trigger investigation.

## N26 — Cost monotonicity
Increasing slippage/fees should not magically increase performance. If it does, inspect simulator logic.

## N27 — Fill-probability realism
For maker strategies, model adverse selection and queue position. A 2025 live-trading study documented a negative relationship between fill probability and post-fill returns.

## N28 — Survivorship control
Maintain dead/delisted securities and expired historical entities where applicable.

## N29 — Corporate-action control
Adjust constituent/history membership with point-in-time index composition.

## N30 — Schema drift test
Replay old and new source schemas through ingestion; unknown fields cannot silently remap semantics.


## Operationalized donor controls (WSM-D01)

These extend existing controls such as N02, N11, N17, N22 and N24. They do not replace them.

## N31 — Future-poison prefix invariance
For every decision time T, mutate every source value strictly after T (10×, NaN, shuffled rows, revised future vintages, future universe membership). The canonical prediction and evidence hash at T must remain identical. A failure blocks the model family.

## N32 — Single-use reserve receipt
Reserve opening must be recorded before downloading or scoring the reserve. A second attempt with the same campaign/protocol/reserve identity must fail before any data I/O. Interrupted attempts remain consumed and auditable.

## N33 — Whole-universe completeness
Remove one required asset, date path, source vintage or event row. The experiment must fail closed or use a predeclared abstention rule. It may not silently shrink the declared universe to successful downloads.

## N34 — One-shot model-call commitment
For a reserved model/run/attempt, timeout, HTTP 429, malformed JSON, invalid schema, missing output or late response consumes the attempt. No retry may generate a second forecast under the same observation. Verify the durable reservation receipt exists before model invocation.

## N35 — Causal fill custody
Reject fills produced in the same run as the intent, without a successful prior-run receipt, with quote time earlier than decision/receipt, with stale quotes, or with missing/out-of-tolerance independent corroboration.

## N36 — Hash-chain replay and terminal-state agreement
Recompute the event chain from genesis. Mutate, reorder, truncate or duplicate an event and require the auditor to stop before new processing. Compare the final chain hash/count against the persisted summary. Do not claim external immutability unless protected history and independent attestations exist.

## N37 — Lifetime research-debt monotonicity
Add an abandoned, failed, interrupted or unopened candidate family. The campaign/lifetime search burden must not decrease. A new branch, month, agent, model name or file path does not reset multiplicity.

## N38 — Family-cloning invariance
Duplicate an expert within a methodology family. The family's top-level vote/weight must remain unchanged. New independent families require explicit source/provenance and evidence; model count alone is not independent evidence.

## N39 — Deterministic scheduler retry
Force a publication race after a deterministic slot has been computed. Retry the same slot/idempotency key/payload; do not silently regenerate a different state. Report expected-cycle coverage, missed slots, retry result and backup path separately.

## N40 — Frozen cohort and delayed grading
Freeze the eligible universe and its hash at ranking time. Grade every member at predeclared horizons, including failures, delisted names and missing outcomes. Do not rebuild the cohort after observing returns.

## N41 — Anchor-freeze versus rolling-update equivalence
Compare a frozen-anchor policy and a rolling-update policy on the same starting cohorts, target horizons, costs and data availability rules. The rolling policy may only use data published before each target decision interval.
