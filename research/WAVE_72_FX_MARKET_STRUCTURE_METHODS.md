# Wave 72X — Research Methods

Namespace: **W72X**

## W72X-M01 — Four-clock timestamps for every FX observation
Store event_time, source_received_time (venue), published_time (benchmark/ECB/CFTC/CLS), first_seen_time and ingested_time. Features are legal only if published_time <= decision_time. ECB rate: snapshot ~14:10 CET but published ~16:00 CET.

## W72X-M02 — DST-resolved clocks from IANA tz
Compute all fix, cut and settlement instants from Asia/Tokyo, Europe/Frankfurt, Europe/London, America/New_York, America/Chicago zone rules per date. Never hard-code ET hours for London or ECB events; include the UK/US mismatch weeks (2026: 25 Oct to 31 Oct).

## W72X-M03 — Benchmark window version registry
Version WMR window (one-minute historical per Evans' sample; 5-minute per LSEG factsheet) with effective dates; any test spanning the change must be split. Exact change date is PROVENANCE_PENDING and must be sourced from the WMR methodology archive.

## W72X-M04 — Placebo-clock requirement
Every fix-conditional test must include placebo clocks (e.g. +37 minute shift, :20 past the hour, random days) matched on time-of-day, day-of-week and event calendar. A rule that does not beat placebo is retired.

## W72X-M05 — Month-end and holiday calendar control
Flag last business day, UK bank holidays (London fix on non-US business days), US holidays, Japan gotobi candidates, and index rebalance dates; fit effects with and without these controls.

## W72X-M06 — Event-window censoring
Remove or flag minutes within +/-2 minutes of tier-1 scheduled releases when estimating fix effects, unless the test is explicitly about collision (W72X-E24).

## W72X-M07 — Tick and increment normalization
After the 2024 EBS changes, normalise spreads and impact to pips and to 1-minute sigma; keep pre/post Q1 2024 separate for EUR/USD and AUD/USD.

## W72X-M08 — Venue-source attribution
Record data source per observation (EBS, LSEG Matching, CME Globex, LP streams, vendor composite). Do not mix composite quotes with firm-book data; label as indicative vs firm.

## W72X-M09 — Futures-vs-spot basis hygiene
When using CME 6E/6J as spot proxies, remove carry using SOFR and the foreign rate over the days to expiry; handle roll and IMM date; physical-delivery expiry minute is excluded.

## W72X-M10 — Cross-currency basis data rights
Basis series (e.g. Bloomberg/Refinitiv) are licensed; publish only derived statistics. Use CME FX Link deviation as the public-feasible proxy and label it as a proxy.

## W72X-M11 — Release-lag measurement for slow sources
For CLS monthly reports, BIS tables and Fed H.4.1, measure first_seen minus nominal period end for >=12 releases and store as latency distribution before any forecasting use.

## W72X-M12 — Vintage-first storage
Store raw vintages of BIS triennial (preliminary Sept 2025 vs later final), ECB reference rate corrections, WMR republications (0.03% overall, 0.26% for 4pm per LSEG 2015-2020), CFTC revisions; never backtest on revised data without flagging.

## W72X-M13 — Purged walk-forward with embargo
Purge +/- the longest label horizon plus the fix window; embargo overlapping windows; month-end samples are few (12 per year), so use block bootstrap by month with the minimum events per bucket declared in advance.

## W72X-M14 — Multiple-testing control
The fix, ECB, option-cut, settlement and CLS families create many hypotheses; use a pre-registered family list and hierarchical FDR (Benjamini-Yekutieli) at the wave level.

## W72X-M15 — Sign-ambiguity declaration
State the sign hypothesis ex ante or declare the test two-sided: pre-fix USD drift, hedging-flow direction and gotobi directional effects are sign-sensitive; record sign convention (USD per foreign currency vs inverse).

## W72X-M16 — Cost-aware evaluation
Evaluate FX-conditional rules with the W78B cost ledger (fees, spread, impact, latency); gross effects that vanish net of costs are retired for execution use but may remain as gates.

## W72X-M17 — Last-look data hygiene
Only own order records are used for last-look edges; never infer counterparty identities; LP names are pseudonymised; rejections and acceptance timestamps stored with client and server clocks.

## W72X-M18 — Confidentiality and rights boundary
Do not redistribute LSEG WMR, CLS licensed, CME licensed or Bloomberg data; store hashes and derived features; respect redistribution restrictions listed in SOURCE_NOTES.

## W72X-M19 — Mechanical-vs-informational classification
Tag each state as MECHANICAL_CLOCK (benchmark, settlement), FLOW_PROXY (BTIC, positioning) or INFORMATION_PROXY; promote MECHANICAL_CLOCK states first because they are knowable ahead of time.

## W72X-M20 — Negative-control library
Maintain controls: non-fix hours, non-FX contracts for COT tests, random dates, shuffled labels, alternative currency pairs not referenced by the benchmark.

## W72X-M21 — Intermediate-outcome promotion gate
Promotion requires stage 3 (intermediate microstructure outcomes) then stage 4 (execution outcomes) before any return claim; no PnL claim from stage 2 evidence.

## W72X-M22 — Source-failure handling
If a primary page returns 403/404/503 or only an unreadable PDF, record SOURCE_DOWN or ACCESS_DENIED, not zero; keep the prior verified snapshot hash.

## W72X-M23 — Reproducibility manifests
Each run logs data vintage hash, code git hash (by the lead), parameter values, calibration windows and seeds; fix-window length, ramp length L and slice period are calibrated parameters with declared ranges.
