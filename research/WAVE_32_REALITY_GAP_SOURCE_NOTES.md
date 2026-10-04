# Wave 32R — Source & Method Notes

Namespace: **W32R**

This wave primarily composes existing repo sources rather than introducing a new external feed family.

## W32R-D01 — Existing Truth Layers
Reuse canonical waves:
physical telemetry,
institutional flow,
regulatory/legal state,
operations,
claims/financial loss,
credit,
market microstructure.

No duplicate connectors.

## W32R-D02 — Real-Time Vintage Principle
All source pairs must use their actual point-in-time public vintages.

This is the core source contract for W32R.

## W32R-D03 — Nowcast Revision Analysis
Method literature decomposes nowcast changes into:
new observations,
data revisions,
and parameter/model revisions.

Use this decomposition as methodological inspiration for attribution of forecast changes.

## W32R-D04 — Robust Bayesian Online Changepoint Detection
Recent Bayesian online changepoint work provides robust sequential posterior frameworks for detecting structural changes in streaming data.

Use as method candidate, not proof of market alpha.

## W32R-D05 — Collective Anomaly vs Changepoint
2025 research explicitly models collective anomalies and changepoints jointly, helping distinguish temporary disagreement from permanent relationship change.

Methodology inspiration only.

## W32R-D06 — Conformal Multivariate Anomaly Detection
Recent conformal time-series work uses calibrated predictive regions/anomaly scores for multivariate operational systems.

Assumption validation is mandatory under financial time dependence.

## W32R-D07 — Conflict-Guided Multimodal Fusion
AISTATS 2025 and WACV 2025 work studies uncertainty-aware/conflict-guided evidence fusion, including discounting unreliable modalities.

Use the principle:
conflict should increase uncertainty or downweight suspect evidence.

Do not treat autonomous-vehicle results as financial evidence.

## W32R-D08 — Forecast Disagreement Literature
Financial/economic literature finds forecast disagreement can carry state-dependent information about uncertainty/pricing.

Use as motivation to test, not as universal directional rule.

## W32R-D09 — Internal Canonical Cross-References
High-value pairs include:
W31C catastrophe loss <-> W13H/W15X/W18G physical recovery,
W25C credit <-> equity/options,
W27V cash <-> futures/options,
W29L legal labor state <-> W16S throughput,
W30W legal water state <-> physical hydrology/output,
W24M formal port state <-> queue/throughput.

## W32R-D10 — Dependency Warning
Many "different" public datasets share a common upstream source.

Maintain provenance graphs and never count correlated descendants as independent confirmation.
