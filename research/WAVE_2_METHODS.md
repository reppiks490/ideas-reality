# Wave 2 Research Methods

## M21 — Time-Series Knockoff / FDR Feature Selection

Problem:
The alternative-data feature library can become enormous. Ordinary feature importance is not evidence, and classic model-X knockoffs can fail if time dependence is mishandled.

Research directions:
- Time-Series Knockoff Inference (TSKI)
- DeepLINK-T style temporal knockoffs
- dependency-aware T-Rex variants

Goal:
Control feature-selection false discoveries while respecting serial dependence.

Use:
screen huge physical/macro feature libraries before expensive downstream tests.

## M22 — Double Machine Learning for Time Series

A 2026 preprint adapts Double Machine Learning to macro time series using reverse cross-fitting.

Potential use:
estimate causal/event effects after flexibly controlling for many confounders.

Important:
Predictive tuning quality is not necessarily causal-score quality.

Application examples:
- auction shock -> NQ return controlling for rates/volatility
- port shock -> retail-sales surprise
- regulation -> sector return controlling for market beta

## M23 — Invariant Feature Survival

Research:
seqICP / invariant causal prediction / modern invariant-learning methods.

Question:
Which relationships remain stable across:
- years
- volatility regimes
- sessions
- macro regimes
- structural rule changes
- geographies

Prefer features with lower peak backtest performance but stronger environment invariance.

## M24 — Environment Discovery Before Invariance

Problem:
Market regime labels are often hand-wavy.

Approach:
infer candidate environments from:
volatility, rates, liquidity, macro state, event density, source behavior.

Then test feature stability across discovered and predefined environments.

Never allow environment inference to use future target values.

## M25 — Prequential Evidence Ledger

For each model, score predictions sequentially in timestamp order.

Store:
- prediction
- probability/interval
- realized target
- loss
- calibration
- log score
- evidence increment

Advantage:
makes live degradation visible and discourages retrospective cherry-picking.

## M26 — Sequential FDR / e-Value Research

For continuous hypothesis generation investigate:
- online e-BH
- e-LOND
- e-GAI
- e-LORD
- e-SAFFRON
- LORD/SAFFRON where assumptions hold

Reason:
the research engine may create hypotheses indefinitely; fixed-batch multiple-testing logic is insufficient.

## M27 — Event Randomization Inference

For sparse events:
auctions, regulations, disasters, large outages.

Construct placebo event times matched on:
weekday, time-of-day, volatility, macro calendar, liquidity.

Compare observed effect to matched placebo distribution.

## M28 — Mechanism-Matched Placebos

Examples:
Port of LA cargo shock should affect import-heavy sectors more than unrelated domestic services.
Mississippi lock shock should affect exposed agricultural basis more than tech.
Aerospace directive should affect exposed manufacturers/suppliers more than random industrials.

A mechanism that cannot beat exposure-matched placebo tests is weak.

## M29 — Counterfactual Chain Validation

For each composite edge, validate every link:

source -> intermediate physical/economic outcome
intermediate -> expectation revision
expectation revision -> market response

A broken link invalidates the causal story even if the final regression is significant.

## M30 — Search-Intensity Accounting

Log:
number of feature transformations
targets tried
horizons tried
models tried
regimes tried
hyperparameter trials
agent-generated variants

Use this as metadata in promotion decisions.

A 3-sigma result after 100,000 adaptive tries is not a 3-sigma discovery.

## M31 — Source-Latency Distribution Modeling

Do not store one fixed latency.

Estimate:
P(latency <= t | time-of-day, source, load, event type)

Backtests use conservative quantiles or actual historical publication timestamps.

## M32 — Revision-Surface Analysis

For forecast/revisable data:
model the full sequence of vintages.

Features:
- revision size
- revision direction persistence
- disagreement
- time-to-event
- revision acceleration

This is often more realistic than using final values.

## M33 — Edge Capacity Stress

A predictive feature is not necessarily monetizable.

Stress:
- spread ×2/×3
- slippage quantiles
- partial fills
- delayed fill
- size scaling
- volatility jumps
- overnight gaps

Output:
edge value vs capital/capacity.

## M34 — Market Impact Endogeneity Test

For high-frequency models, verify whether the "signal" predicts price or simply identifies moments when own execution would move price.

Use:
depth, expected impact, trade size, refill speed.

## M35 — Causal Direction Stress

For every lead-lag relation:
test A->B and B->A under multiple lags.

Require:
incremental forecasting after conditioning on own history and shared drivers.

## M36 — Information Arrival Decomposition

Decompose return around event into:
pre-event drift
instantaneous jump
post-event continuation/reversal

This separates:
possible leakage / anticipation
efficient repricing
true delayed diffusion.

## M37 — Abstention Calibration

Models must be allowed to say:
NO EDGE / UNKNOWN / SOURCE STALE / REGIME OUT-OF-DISTRIBUTION.

Measure whether abstention improves conditional accuracy and reduces tail losses.

## M38 — OOD Distance Gate

For every live feature vector compute distance to training support.

Candidates:
Mahalanobis in stable latent space
density-ratio estimation
ensemble disagreement
conformal nonconformity

Do not trade on extremely out-of-support states unless the strategy is specifically designed for them.

## M39 — Falsification-First Ranking

Research priority score should reward:
clear mechanism
clean timestamp
orthogonality
cheap falsification
good historical coverage
reproducibility

and penalize:
vague sentiment
unverifiable source
heavy revisions
short history
high model complexity
high licensing friction.

## M40 — Null Discovery Benchmark

Every research campaign should include synthetic null features with similar autocorrelation and distribution.

The pipeline's observed false discovery rate on these nulls becomes a health metric.

If the system "discovers" many nulls, stop the campaign.
