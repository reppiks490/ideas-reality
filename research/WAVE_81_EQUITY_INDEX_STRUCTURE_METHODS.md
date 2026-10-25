# Wave 81E — Research Methods

Namespace: **W81E**

## W81E-M01 — Rule-Version Registry for Auction Mechanics

Encode cutoff times (MOC/LOC/IO), dissemination cadences and order-type availability per venue and effective date. The Nasdaq FAQ read here is dated 2019 (cutoff 3:55 MOC, 3:58 LOC); current Nasdaq rule text must be fetched before use. NYSE fact sheet (2024) shows 3:50 cutoff. Never hard-code times.

## W81E-M02 — Venue Window Matrix and Look-Ahead Audit

Build a matrix of which imbalance fields are available at time t for each venue and listing (NYSE 3:50 onwards, Arca/American 3:00 onwards, Nasdaq 3:50 early then 3:55). Every feature is tagged with its earliest legal timestamp.

## W81E-M03 — Exchange Timestamp Contract

Use source (exchange) timestamps from NYSE Pillar SourceTimeNS and Nasdaq NOII timestamp; record receive time; compute clock skew. Features at decision time t use messages with receive_time <= t.

## W81E-M04 — Update-If-Changed Handling

NYSE publishes every second only if changed; absence of a message means no change, not missing data. Forward-fill with explicit staleness counters; do not treat as null.

## W81E-M05 — Zero-Default Fields Are Missing

Pillar fields such as ContinuousBookClearingPrice default to 0 for regulatory imbalances; map zero to missing before any arithmetic.

## W81E-M06 — Index Weight Vintage

Constituent weights must be point-in-time; use provider holdings or reconstruct from float shares and prices on the as-of date. Third-party concentration blog numbers are never inputs.

## W81E-M07 — Constituent Listing-Venue Map

Maintain listing exchange per constituent with effective dates; share class duplicates (e.g., dual classes) treated as separate securities with shared issuer id.

## W81E-M08 — Aggregate Imbalance Scaling

Scale imbalance by ADV20 (excluding event days) and winsorize; report results for raw, ADV-scaled and dollar-scaled.

## W81E-M09 — Futures Mapping Window

Map the cash close to futures time with explicit handling of the futures session after 4:00 p.m. ET (CME hours PROVENANCE_PENDING); do not assume ES stops at 4:00.

## W81E-M10 — Placebo Days and Matched Controls

For close-related edges construct placebo windows (15:20-15:30) and matched days (same weekday, similar volatility, non-rebalance, non-expiry). Exclude days owned by W26R and W69O (rebalances, quarterly expiry).

## W81E-M11 — Rebalance-Day Exclusion Rule

Non-rebalance edges exclude S&P/Nasdaq/Russell rebalance and quarterly expiry days or include them as stratified regimes so W26R effects are not double counted.

## W81E-M12 — Negative Controls

Early-close days, days with data outages and the custom-basket boundary serve as negative controls; effects must not appear where mechanics differ.

## W81E-M13 — Multiple Testing Across Names and Windows

Across hundreds of constituents and many windows, control FDR at the index-aggregate level, pre-registering aggregate definitions (WIP etc.).

## W81E-M14 — Data Rights and Licensing

NYSE Pillar imbalance and Nasdaq NOII feeds are paid real-time products; record entitlements. Public FINRA files are public with caveats.

## W81E-M15 — FINRA File Vintage Storage

Store first-posted and updated versions separately; published_time upper bound 18:00 ET same day; next-session features only.

## W81E-M16 — Short-Volume Interpretation Rule

Short sale volume is not short interest and not bearishness; hedging by market makers and APs mixes in. All tests two-sided.

## W81E-M17 — Exchange Rule Change Monitor

Subscribe to exchange rule filings (SEC SRO filings) and NYSE/Nasdaq notices; any change retires or re-versions an edge. SEC releases cited by search (NYSE 34-84804, 34-85021; Nasdaq 34-85292, 34-91096) are PROVENANCE_PENDING until read.

## W81E-M18 — Event-Time Versus Wall-Time Alignment

Align to seconds-to-close and to step identifiers (E02) rather than wall clock to handle early closes.

## W81E-M19 — Cost Model for Last-10-Minute Trading

Use measured spread, depth and auction participation; include inability to cancel after cutoff for order types; futures cost separate from cash.

## W81E-M20 — Purged Walk-Forward With Daily Embargo

Close-based features embargo the following open; overlapping windows purged; terminal holdout consumed once.

## W81E-M21 — Cross-Wave Collision Check

Check overlap with W26R (rebalance flows), W27V (LULD, halts, Rule 201), W33S (short constraint), W69O (options), W70B (book), W78B (execution), W73E (macro clocks). State the increment.

## W81E-M22 — Promotion Gate (Intermediate Outcomes)

Promotion requires: (1) feature legality at decision time, (2) placebo and negative control pass, (3) improvement in intermediate outcomes (imbalance-to-close prediction, slippage tail) before P&L, (4) stability across regimes including non-rebalance and rebalance strata, (5) live shadow evidence, (6) multiple-testing control.

## W81E-M23 — Confidentiality Boundary

Public and licensed exchange data only; no inference about AP baskets, client orders or identities.
