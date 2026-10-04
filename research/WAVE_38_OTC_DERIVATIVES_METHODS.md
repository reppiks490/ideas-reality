# Wave 38O — Research Methods

Namespace: **W38O**

## W38O-M01 — Public-Time Ledger
Store execution, reporting, dissemination and ingest timestamps separately.

## W38O-M02 — No Counterparty Identity Inference
Public swap/SBS dissemination is intentionally anonymous.

Never assign a trade to a named institution from public SDR prints.

## W38O-M03 — No Fake Customer Direction
If the public field set does not identify economically valid payer/receiver/buyer/seller direction, do not synthesize it from price movement.

## W38O-M04 — Part 43 vs Part 45 Separation
Part 45 regulatory reporting contains fields that may not be public under Part 43.

Use only fields actually disseminated for public-signal research.

## W38O-M05 — SBSR vs CFTC Jurisdiction
Single-security/narrow-based security swaps fall under SEC security-based-swap rules; broad swaps fall under CFTC jurisdiction.

Route products correctly.

## W38O-M06 — Censored Notional Model
Rounded/capped notionals are interval-censored.

Use lower bounds / likelihood methods and retain cap flags.

## W38O-M07 — Block Delay Model
Use applicable historical block/large-notional dissemination delay by asset/product/date.

## W38O-M08 — Rule-Version Ledger
CFTC/SEC reporting rules, thresholds, fields and compliance relief change.

Backtests use the rule effective at the historical timestamp.

## W38O-M09 — UPI Vintage
UPI/reference-data mappings can evolve.

Archive product reference attributes point-in-time.

## W38O-M10 — SDR Coverage Map
Measure repository share by product/time before using any one SDR as market proxy.

## W38O-M11 — UTI / Dissemination Deduplication
Use lifecycle identifiers/action types to prevent double-counting corrections, novations and resubmissions.

## W38O-M12 — Cross-SDR Clock Alignment
Repositories may disseminate with different operational latency/maintenance schedules.

## W38O-M13 — Weekend/Maintenance Handling
Public feeds can pause during scheduled maintenance and release queued reports later.

Do not interpret maintenance bursts as contemporaneous trading.

## W38O-M14 — Package Reconstruction
Package legs should be linked only using public package identifiers/terms.

Do not guess package membership from time proximity alone.

## W38O-M15 — Price-Notation Normalization
Normalize rate, spread, points, currency, percentage and other price notation before comparison.

## W38O-M16 — Product-Liquidity Baseline
Expected trade count/size varies drastically by UPI/tenor/currency.

Use product-specific baselines.

## W38O-M17 — Event-Time Neutralization
Control:
Fed/ECB/BoE decisions,
Treasury auctions,
CPI/jobs,
earnings,
index rolls,
major credit events.

## W38O-M18 — Public Rights / Use Gate
Repository public pages may distinguish direct public use from redistribution/commercial use.

Tag licensing/usage terms before production ingestion.

## W38O-M19 — Cross-Market Intermediate Gate
Before return alpha require OOS improvement in:
swap curve,
credit spread,
basis,
volatility,
cash-credit stress,
or other mechanistic intermediate target.

## W38O-M20 — Counterfactual Repository Test
Where multiple SDRs cover the same product family, test whether signal persists across repository-specific samples and is not a reporting artifact.
