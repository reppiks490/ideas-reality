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
