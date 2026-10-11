# Wave 75A — Research Methods

Namespace: **W75A**

## W75A-M01 — Three-Clock Contract for Text
Store event_time, source_received_time, published_time, first_seen_time, ingested_time per document; use only first_seen_time for decisions per DATA_AVAILABILITY_CONTRACTS section 1.

## W75A-M02 — Deadline Is Not Publication
Never use the 8-K four-business-day deadline (or any filing deadline) as availability; use acceptance/first_seen.

## W75A-M03 — Collector Self-Timestamping
Poll with jitter, record local monotonic and NTP-synced UTC; measure clock offset daily.

## W75A-M04 — Immutable Vintages
Hash every fetched payload (submissions JSON, GKG file, vendor sentiment); never overwrite.

## W75A-M05 — Fair-Access Compliance
Respect SEC 10 requests/second aggregate cap and declared User-Agent policy (UA rule UNVERIFIED); log throttling.

## W75A-M06 — Vendor Plan Gate Log
Record plan/rate-limit failures (AV premium, FMP plan gate seen 2026-10-11) as availability evidence.

## W75A-M07 — Item Parsing Coverage Audit
Compare vendor item list against direct EDGAR parse; 1.05 absent in Financial_Datasets list_filing_item_types.

## W75A-M08 — Lexicon Freezing
Freeze lexicons/models by date; no re-scoring of history with later models.

## W75A-M09 — LLM Lookahead Test
Test LLM-scored text against events after the model training cutoff only.

## W75A-M10 — Diff Alignment
For statement diffs, align sentences by edit distance on normalized text; store diff hash.

## W75A-M11 — Release Clock Source
Obtain release times from the primary page or observed first-seen; treat unstated times as UNVERIFIED.

## W75A-M12 — Event-Cluster De-Duplication
Cluster by SimHash plus entity overlap in window w; evaluate on a hand-labelled sample.

## W75A-M13 — Placebo Calendar
Matched placebo dates (same weekday/hour, no event) for every event study.

## W75A-M14 — Placebo Entities
Matched placebo tickers/pages/queries for attention signals.

## W75A-M15 — Shuffled-Country and Shuffled-Theme Control
Break theme/country mapping for GDELT edges.

## W75A-M16 — Sign-Ambiguity Declaration
State if positive tone can be bullish (surprise) or bearish (priced-in); test both.

## W75A-M17 — Common-News Control
Include concurrent scheduled-news and options-implied move controls.

## W75A-M18 — Latency-Conditional Evaluation
Evaluate each edge by feed tier; report PnL-free reaction capture, not profit.

## W75A-M19 — Multiple-Testing
Count all lexicon variants/windows in the family; BH-FDR or deflated metrics per RESEARCH_PROTOCOL.

## W75A-M20 — Rights and Terms Screen
Before storing X/Reddit/Trends/vendor text, record license, redistribution and derived-data rights.

## W75A-M21 — Intermediate-Outcome Promotion Gate
Promote only after A->B->C->D ladder: source predicts intermediate outcome, then expectation revision, then return, then execution improvement.

## W75A-M22 — Decay Monitoring
Rolling out-of-sample check with automatic retirement if lag-gap or effect t-stat decays.

## W75A-M23 — Missingness Honesty
No event is not zero; absence of 8-K or mentions is coded separately from zero counts.
