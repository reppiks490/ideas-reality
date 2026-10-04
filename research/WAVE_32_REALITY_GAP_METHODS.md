# Wave 32R — Research Methods

Namespace: **W32R**

## W32R-M01 — Expected-Lag Contract
For every source pair predefine plausible causal direction and lag distribution.

Do not compare unsynchronized layers as if simultaneous.

## W32R-M02 — Conditional Residual Gap
Define disagreement relative to E[B|A,state], not raw A-B.

## W32R-M03 — Uncertainty Standardization
Scale residual by predictive uncertainty so noisy pairs do not dominate.

## W32R-M04 — Source Independence Graph
Map common upstream dependencies.

Two feeds derived from the same source do not count as two independent confirmations.

## W32R-M05 — Reliability Discount
Weight each modality by point-in-time reliability:
staleness,
missingness,
revision history,
forecast error,
coverage.

## W32R-M06 — Conflict Is Not Fusion
Preserve the conflict score before combining evidence.

A fusion model can hide disagreement that is itself informative.

## W32R-M07 — Conflict-Guided Fusion
Investigate evidence-theory / uncertainty-aware conflict discounting as methodology inspiration.

Do not import Dempster-Shafer assumptions blindly into markets.

## W32R-M08 — Bayesian Surprise
Measure prior-to-posterior belief change using KL/information-gain-like metrics only where distributions are calibrated.

## W32R-M09 — Nowcast Revision Decomposition
Decompose forecast changes into:
new observations,
data revisions,
parameter/model changes.

Do not label a back-revision as new real-world information.

## W32R-M10 — Forecast Vintage Archive
Every forecast/model output used in disagreement research must be point-in-time archived.

## W32R-M11 — Online Change Detection
Compare robust Bayesian online change-point methods and collective-anomaly models for persistent residual shifts.

## W32R-M12 — Conformal Residual Monitoring
Investigate conformal anomaly scores/prediction regions for calibrated residual alerts.

Time dependence/exchangeability assumptions must be tested.

## W32R-M13 — Source-Failure Negative Control
Simulate stale/frozen/noisy feeds.

System must classify source health failure separately from economic contradiction.

## W32R-M14 — Wrong-Geography Placebo
Pair the same source with unrelated regions/facilities.

A genuine local RealityGap should weaken.

## W32R-M15 — Lag-Permutation Placebo
Shift one layer beyond plausible causal window.

Signal should degrade.

## W32R-M16 — Contradiction Persistence Threshold
Calibrate persistence thresholds from historical timing noise and publication-lag variance.

## W32R-M17 — Resolution Target Pre-Registration
Before studying a gap, specify what resolution means:
A moves,
B moves,
both,
or third-variable explanation.

## W32R-M18 — Third-Cause Search
Before calling A->B, test whether C jointly explains the disagreement.

## W32R-M19 — Abstention Calibration
Reward correct abstention when disagreement reflects uncertain source health.

## W32R-M20 — Meta-Edge Promotion Gate
Promote only if the contradiction adds OOS information beyond both component signals individually.
