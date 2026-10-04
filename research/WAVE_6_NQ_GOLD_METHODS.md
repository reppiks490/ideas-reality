# Wave 6N Research Methods

All IDs are canonical.

## W6N-M01 — Foreign Disclosure Point-in-Time Reconstruction
Store per issuer:
- report_period
- disclosure_timestamp
- source_publish_timestamp
- ingested_timestamp
- correction_timestamp

Never use report period as availability time.

## W6N-M02 — Time-Varying Supply-Chain Graph
Every supplier/customer edge must include:
source, confidence, effective_from, effective_to and estimated materiality.

A current supply-chain graph cannot be projected backward into old backtests.

## W6N-M03 — Fundamental-First Validation
For NQ physical inputs:
physical/fundamental signal -> earnings/revenue KPI -> sector repricing -> index.

Direct index-return mining is secondary.

## W6N-M04 — Physical Gold Reconciliation
Cross-check observed changes across:
ETF trusts, COMEX stocks/deliveries and public trade/import information where available.

Unexplained metal movement is a residual, not assumed bullish/bearish flow.

## W6N-M05 — Delivery-Cycle Normalization
Normalize issues/stops/stocks by:
first notice day, delivery month, roll state, OI and seasonality.

## W6N-M06 — ETF Timing Integrity
Separate:
trade date, creation notification, share issuance, settlement-date bar state and publication time.

If exact public intraday timing is uncertain, use a conservative next-session availability assumption.

## W6N-M07 — Credit Common-News Control
Control corporate-bond/equity lead-lag for:
EDGAR events, macro releases, Treasury rates, sector return, broad market, options shock and known company news.

## W6N-M08 — Credit Residualization
Neutralize bond changes for:
duration, Treasuries, rating, sector credit and broad credit indices before defining issuer-specific shock.

## W6N-M09 — Public-Company Entity Resolution
Use stable legal identifiers where possible.
Fuzzy name alone cannot map a government recipient, sanctioned entity or subsidiary to a ticker.

Store:
legal entity ID, public parent, effective dates, mapping evidence and confidence.

## W6N-M10 — Procurement Availability Lag
Estimate:
action_date -> first_public_seen

by source, agency and event type.

Backtests use first public time, never only administrative action date.

## W6N-M11 — Procurement Funnel State Model
Model transition probabilities and durations through:
sources sought -> solicitation -> award -> modification -> obligation -> outlay.

## W6N-M12 — Sanctions Delta Archival
Archive structured full OFAC/BIS lists plus official hashes/deltas where available.

Compute point-in-time changes reproducibly.

## W6N-M13 — Regulatory Exposure Predefinition
Define product/geography/supply-chain exposure before observing subsequent returns.

## W6N-M14 — Hurricane Forecast Vintage Archive
Store every NOAA/NHC forecast vintage.
Never backfill the final track into a pre-landfall research decision.

## W6N-M15 — Restoration Curve Validation
Validate shutdown AND recovery.

For each event:
forecast additional shutdown, 50% recovery, 90% recovery and full normalization.

## W6N-M16 — Clearing-Firm Identity Caution
CME issues/stops clearing-firm identity does not identify beneficial-owner motive.

Use concentration as a structure feature only.

## W6N-M17 — Physical Inventory Location Model
Metal can migrate among London, COMEX, ETF custodians and other vault networks.

Exchange outflow is not global supply destruction.

## W6N-M18 — Global Timezone Integrity
Keep native disclosure timezone plus UTC.
Never U.S.-date-bucket Taiwan/Korea events before timestamp normalization.

## W6N-M19 — Correction / Vintage Handling
Foreign revenue corrections, award modifications, sanctions-list changes and trust updates remain separate immutable vintages.

Never silently overwrite what the market originally knew.

## W6N-M20 — Secondary Evidence Firewall
Practitioner, vendor and industry research may generate hypotheses.

Production research datasets should be anchored to primary official/issuer sources wherever possible.

## W6N-M21 — Cross-Channel Disagreement Test
Explicitly model disagreement states rather than averaging independent channels together.

Examples:
- strong Taiwan revenue + deteriorating tech credit
- bullish GC options + ETF redemptions
- large procurement pipeline + weak realized obligations

Disagreement can be a regime/volatility feature even when direction is uncertain.

## W6N-M22 — Materiality Normalization
Scale events to the relevant economic object:
- award / issuer revenue
- credit shock / debt outstanding
- delivery / nearby OI
- ETF ounces change / trust ounces
- shutdown / regional production
- restriction / exposed revenue

## W6N-M23 — Exposure-Matched Placebo
Every event hypothesis gets:
1. unrelated controls,
2. similarly exposed controls,
3. matched-time placebo events.

A mechanism should beat its exposure-matched placebo set.

## W6N-M24 — Preannouncement Efficiency Curve
For scheduled/known events, measure information entry at:
announcement -> pre-event -> event -> result -> settlement/effective date.

## W6N-M25 — Data-Rights Gate
Each source receives one deployment classification:
PUBLIC_COMMERCIAL_OK
PUBLIC_NONCOMMERCIAL
ATTRIBUTION_REQUIRED
ACCOUNT_REQUIRED
LICENSED
TERMS_REVIEW
FUTURE

Research access does not automatically imply production rights.

## W6N-M26 — Intermediate-Outcome Gate
Before direct return promotion, require the data to predict or explain the mechanism's intermediate outcome when one exists.

Examples:
- Taiwan revenue pulse -> U.S. hardware revenue surprise
- BSEE forecast -> realized shut-in
- procurement pipeline -> future obligations
- physical gold flow -> inventory/basis state
- credit shock -> subsequent issuer equity repricing

## W6N-M27 — Physical/Financial Lead-Lag Matrix
For each composite keep four directional tests:
physical -> financial
financial -> physical
common shock -> both
feedback loop

Do not promote a "physical lead" if financial markets actually lead the measured physical proxy.

## W6N-M28 — Channel-Specific Half-Life
Estimate effect half-life independently by channel.

Expected examples:
credit microstructure: minutes-hours
regulatory event: minutes-days
monthly revenue: days-weeks
procurement pipeline: weeks-months
physical gold relocation: days-weeks

## W6N-M29 — Structural-Break Replay
Replay each edge before/after relevant market-structure changes:
ETF launches, disclosure-rule changes, sanctions regimes, procurement-system changes, exchange reporting changes and major logistics disruptions.

## W6N-M30 — Canonical Provenance Contract
Every research result records:
canonical_id
source_file
content_hash
dataset_vintage
code_version
campaign_id
hypothesis_count_before_test
terminal_holdout_status

This prevents research provenance from being lost when ideas are later synthesized.
