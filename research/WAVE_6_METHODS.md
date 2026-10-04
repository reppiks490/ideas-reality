# Wave 6 Research Methods

## M91 — Adoption-to-Economics Validation Ladder

Do not test digital telemetry directly against stock returns first.

Prove:
developer/user adoption
-> product KPI
-> company KPI
-> expectation revision
-> return.

Reject signals that skip every intermediate mechanism.

## M92 — Automation/Bot Decontamination

Package downloads and repository activity can be dominated by:
CI,
mirrors,
bots,
dependency refreshes,
security scanners.

Use available user-agent/environment/version patterns and robust transformations to separate plausible human/deployment demand from automation.

## M93 — Ecosystem Share Instead of Raw Growth

Absolute downloads/stars often trend structurally upward.

Prefer:
candidate product / peer ecosystem total
or
candidate growth - peer-basket growth.

## M94 — Release-Cohort Normalization

Compare a release to historically similar releases:
major/minor/patch,
project age,
installed base,
weekday,
season,
marketing event.

Measure abnormal diffusion rather than raw post-release activity.

## M95 — Dependency-Weighted Adoption

One dependency addition by a critical downstream project may matter more than thousands of shallow downloads.

Weight adoption by downstream centrality, production relevance and persistence.

## M96 — Metric Identity Versioning

Digital platforms change counting methodology.

Store:
API version,
field definition,
rate-limit behavior,
bot filters,
historical methodology changes.

Never splice incompatible metric definitions without regime labels.

## M97 — Prospective Archive Requirement

Some valuable APIs provide only current state or limited history.

Begin archiving prospectively before claiming historical alpha.

Examples:
Steam current players,
short-retention public event APIs.

## M98 — Business-Model Conditioning

Usage does not map to revenue identically across:
ad-funded,
subscription,
usage-based,
open-source,
premium game,
free-to-play.

Estimate separate translation functions.

## M99 — Government Flow Schedule Reconstruction

For SPR/public commodity actions reconstruct:
announcement,
solicitation,
award,
nomination,
delivery,
inventory recognition.

Backtests use the first public version of each schedule.

## M100 — Physical Flow Rate Conversion

Convert headline quantities into time-distributed flow:
barrels/day,
MMBtu/day,
head/day,
tons/day.

Compare with normal market flow and storage capacity.

## M101 — Cross-Market Leader Stability

For TRACE/equity leadership:
require leadership to persist beyond one lucky interval and survive transaction/reporting latency.

Measure state probability and switching cost.

## M102 — Credit Liquidity Adjustment

A bond price move with one tiny trade is not equivalent to broad credit repricing.

Weight by:
trade count,
size,
bond liquidity,
issue age,
rating,
maturity,
bid/ask proxy if available.

## M103 — Geographic Exposure Quality

For municipal/local signals, headquarters is weak exposure.

Build multiple mappings:
HQ
facilities
employees
sales
customers
tax base.

Test which economic exposure channel actually mediates the relation.

## M104 — Estimate-to-Actual Revision Model

USDA and other physical daily estimates can revise.

Store first estimate, later estimate and actual separately.

Research both:
predictive content of first release
and
revision surprise.

## M105 — Balance-Equation Residual Audit

For natural gas/commodity balances:
do not let model silently absorb accounting residual.

Track residual distribution, revisions and component missingness.
Large residuals trigger data-quality review before signal generation.

## M106 — Capped-Trade Robustness

Public TRACE size caps truncate large trades.

Do not treat capped size as exact.
Use censored-data methods, cap indicators or rank-based size classes.

## M107 — Public Access vs Subscriber Access

Municipal, exchange and digital data products can differ by license/tier.

Every test records exact access class.
A result is not reproducible if the input silently came from a richer subscriber feed.

## M108 — Product-to-Issuer Mapping with Revenue Materiality

Open-source/game/model telemetry must map to the public issuer and to material economics.

Store:
product
publisher/owner
effective ownership dates
estimated revenue exposure
confidence.

## M109 — Cross-Product Cannibalization Control

Growth in one product can come from migration away from the same company's other product.

Measure issuer-level net adoption as well as product-level growth.

## M110 — Truth-Layer Monotonicity Test

If a low-truth proxy claims alpha but fails to predict the next-higher truth layer, lower its prior probability and require stronger evidence before promotion.
