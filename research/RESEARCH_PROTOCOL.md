# Research Protocol

## 1. Discovery and proof must be separate systems

Discovery may be aggressive.
Promotion must be conservative.

Discovery can use:
nonlinear models, causal discovery, representation learning, graph search, feature interactions, symbolic regression.

Promotion must use:
pre-registered hypotheses, timestamp-safe data, purged walk-forward evaluation, multiple-testing control, terminal holdout and live shadow evidence.

Never let the same adaptive search loop repeatedly consume the terminal holdout.

## 2. Every observation gets three times

- event_time: when the underlying event occurred
- published_time: when the source made it public
- ingested_time: when our system received it

Features are legal only if published_time <= decision_time.
For feeds with uncertain delays, use conservative latency.

## 3. Vintage-first storage

For any revisable source:
store raw vintages immutably.

Never backtest a 2024 decision using a 2026-revised value unless the test explicitly studies revised data.

Sources needing special vintage care:
macro data, Indeed, port forecasts, weather forecasts, grid forecasts, company filings/amendments, analyst-like expectation feeds.

## 4. Hypothesis template

Each idea requires:
- economic/physical mechanism
- source
- target
- expected sign or state dependency
- horizon
- publication latency
- confounders
- falsification condition
- primary metric
- capacity assumptions
- cost model

## 5. Causal timing ladder

Prefer testing in this order:
A. source predicts a real-world intermediate outcome
B. source predicts expectation revisions
C. source predicts target return
D. source improves execution/timing of an existing edge

This reduces spurious direct-return mining.

## 6. Multiple-testing control

An always-on research engine creates sequential hypotheses; ordinary p<0.05 is invalid.

Research candidates:
- online e-BH / e-value methods
- LORD / SAFFRON family where assumptions fit
- e-GAI/e-LORD/e-SAFFRON research
- Model Confidence Set / Superior Predictive Ability for surviving model groups

The exact statistical procedure must match dependence/stopping assumptions.

## 7. Environment invariance

A candidate should be tested across meaningful environments:
- high vs low vol
- RTH vs overnight
- pre/post structural rule change
- rate regimes
- crisis vs ordinary
- years
- assets
- geography when physical data

Do not reward a feature solely because one regime dominates the sample.

## 8. Purging and embargo

For forward-return labels:
purge examples whose label horizon crosses folds.
Apply embargo around fold boundaries.
The required embargo depends on the maximum information horizon.

## 9. Terminal holdout discipline

One immutable terminal holdout per research campaign.
No feature engineering after reading its results.
If it is consumed, record that fact and establish a new future holdout rather than pretending it remains clean.

## 10. Sequential evidence

For live shadow testing:
use anytime-valid/e-process style methods where appropriate rather than repeatedly peeking at fixed-sample p-values.

## 11. Uncertainty calibration

A model must output uncertainty or abstention state.
Research modern conformal methods under change points/nonstationarity.

Reject a model whose confidence does not degrade when its environment changes.

## 12. Regime shift detection

Track:
feature distribution, residuals, calibration error, execution quality, source latency and target response.

Candidate methods:
ADWIN-type detectors, unsupervised drift detection, conformal drift, change-point models, ensemble disagreement.

Drift detection does not automatically authorize retraining.

## 13. Negative controls are mandatory

See NEGATIVE_CONTROLS.md.

## 14. Model family diversity

Compare:
linear/sparse baseline
tree boosting
state-space/regime model
simple causal mechanism model
complex learner

If the complex model cannot beat a mechanism-aware simple baseline out of sample, do not promote it.

## 15. Trading evaluation follows prediction evaluation

First prove information.
Then simulate trading.

Metrics:
- out-of-sample loss improvement
- calibration
- information coefficient
- hit rate only where meaningful
- conditional effect size
- turnover
- slippage sensitivity
- drawdown
- capacity

No promotion from Sharpe alone.

## 16. Source failure simulation

Backtest with:
missing feed
late feed
stale feed
revised feed
duplicate data
timezone errors
schema changes
source outage

A candidate that becomes dangerous when its data disappears must fail closed.

## 17. Delay stress test

Artificially delay every alternative source by:
+1 minute / +5m / +15m / +1h / +1d as applicable.

A robust edge should show a sensible decay curve.
If performance improves when data are delayed, inspect for timing bugs or confounding.

## 18. Cost of discovery

Log:
number of hypotheses tried
number of transformations
number of model families
number of parameter searches
researcher/agent interventions

Statistical confidence should be interpreted in the context of search intensity.

## 19. Promotion states

IDEA
DATA_VERIFIED
MECHANISM_VERIFIED
OOS_SIGNAL
ROBUST_SIGNAL
TERMINAL_HOLDOUT_PASS
LIVE_SHADOW
PAPER_ELIGIBLE
IMPLEMENTATION_CANDIDATE
RETIRED

No shortcut from IDEA to IMPLEMENTATION_CANDIDATE.

## 20. Research output contract for Claude

For each promoted candidate provide:
- source schema
- timestamp contract
- immutable raw-data path
- feature specification
- test specification
- known failure modes
- evidence table
- reproduction command/spec
- reason for promotion
- reason it could still be wrong


## 21. Source promotion gate

No candidate may enter DATA_VERIFIED unless every production-relevant source has:
- exact primary source URL, document, endpoint, or feed specification
- source owner and dataset/feed name
- source class from DATA_AVAILABILITY_CONTRACTS.md
- event, reporting-deadline, public-availability, ingest, and revision semantics
- current rule/schema version and effective dates where applicable
- access/rights/redistribution status
- immutable raw-vintage plan
- explicit missing/stale/failure behavior

A statutory filing or reporting deadline is never equivalent to public availability unless the primary source explicitly makes them the same event.

If public latency is undocumented, label it UNKNOWN_MEASURED, measure historical first-seen latency prospectively, and use a conservative availability assumption. Do not label it LIVE merely because the underlying event is reported quickly.

A generic homepage, source name, research paper, or secondary article is not sufficient provenance when a primary rule, API, file, specification, or notice exists.

## 22. Provenance completeness is fail-closed

If a candidate lacks reproducible provenance, timing, or rights metadata:
- keep the hypothesis,
- downgrade the source/candidate to PROVENANCE_PENDING or RETROSPECTIVE_ONLY as appropriate,
- prohibit live-style backtesting and production ingestion,
- do not fill missing semantics by inference.

Killing or downgrading a weak source is a successful research outcome.

## 23. Rule and schema versioning

For regulatory, exchange, index, clearing, filing, operational, and administrative sources:
- preserve the exact rule/schema version effective at decision time
- store amendment/effective dates
- revalidate after every source/rule change
- never apply today's rule backward to an older period unless historically valid
