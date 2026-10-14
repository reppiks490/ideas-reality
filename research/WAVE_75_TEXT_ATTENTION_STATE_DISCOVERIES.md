# Wave 75A — Text, News & Attention-Derived State for Intraday Gating

Namespace: **W75A**

Thesis: text and attention become tradeable state only if they are timestamped on the clock when the market could first see them. SEC filings, central-bank statements, call transcripts, news-event databases, pageviews, search interest and social metrics each have different latency tiers, revision behavior and terms. This wave turns them into gates, confirmations and slow priors rather than naive sentiment trades, and measures latency first.

Boundary: W27V owns LULD/halt/reopening mechanics (W75A only links halt news to filings); W32 issuer-flow, W41 deal-completion, W65 debt-access and W6N/W8R own specific 8-K-driven mechanics; W55T owns Treasury refunding text; W34D owns provider-incident digital signals. W75A owns general 8-K Item latency, statement-diff tooling, attention and headline-latency measurement.

All candidates are research hypotheses only. Claude owns later implementation.

## W75A-E01 — 8-K Item-Level First-Seen Latency Surface

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation); EDGAR accession acceptance timestamps

Mechanism: Public availability of an 8-K is the moment it becomes retrievable, not the deadline. SEC states the submissions API is typically updated in under a second (longer at peak). Latency differs by item because filers batch and time filings (e.g. earnings vs governance), so one global latency constant mis-times features.

Features: per-Item (1.01..9.01) distribution of (first_seen_time - acceptance_datetime), p50/p95/p99, by hour-of-day and by filing-count-in-5min

Target: Calibrated conservative published_time per Item for every downstream W75A edge

Falsify-if: p95 first-seen lag is statistically indistinguishable across Items and hours, or exceeds the decision horizon so that no Item is usable intraday

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: S

## W75A-E02 — Filing-Burst Congestion Lag Inflator

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation)

Mechanism: SEC says latency may exceed one second at peak filing times; earnings-season after-close bursts concentrate thousands of 8-Ks in minutes, which inflates lag exactly when signals matter most.

Features: rolling count of accepted filings per minute, lag(t) regressed on burst intensity, polling-interval jitter

Target: Burst-conditional latency model used to widen the feature embargo

Falsify-if: Lag shows no dependence on burst intensity (slope CI contains 0)

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: A

## W75A-E03 — Fair-Access Polling Budget as a Latency Floor

Primary source: SEC developer resources (https://www.sec.gov/about/developer-resources): 10 requests/second per user across machines

Mechanism: A 10 req/s ceiling shared across all machines bounds how many CIKs can be polled; polling N tickers round-robin imposes expected added delay of N/(2*rate). Universe design therefore sets a latency floor independent of SEC speed.

Features: N_watch, poll_rate<=10/s, effective added delay = N/(2*rate), use of per-CIK submissions vs daily index files

Target: Latency-optimal watch universe (NDX top weights plus ES sector leaders) under the cap

Falsify-if: Measured detection delay is not monotone in N/rate, or index-file polling dominates per-CIK polling at all N

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: B+

## W75A-E04 — Item 2.02 Exhibit-99 Earnings Release vs Wire Gap

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation) Item 2.02 filings; Financial_Datasets get_filing_items (Item-2.02)

Mechanism: Companies issue the earnings press release on wires and furnish it under Item 2.02 Exhibit 99.1. The EDGAR copy can lag or lead wires; the gap measures how much of the surprise is already priced before EDGAR parsing.

Features: t_edgar - t_first_public_wire for NDX constituents, headline EPS/revenue parse, guidance parse

Target: Identification of which constituents EDGAR parsing can still trade vs only confirm

Falsify-if: Median EDGAR lag exceeds 30s-class reaction half-life for all names (parameter to calibrate) so confirm-only use is the sole use

Horizon: INTRADAY

Availability: PUBLIC_EVENT_DRIVEN

Priority: A

## W75A-E05 — Item 7.01 Furnished-vs-Filed Content Classifier

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation) Item 7.01 and Item 8.01

Mechanism: Item 7.01 (Reg FD) and 8.01 are catch-alls; information content varies from investor-deck boilerplate to guidance changes. A text classifier on the exhibit separates informative from boilerplate before any reaction is modelled.

Features: exhibit token novelty vs trailing 4 filings, numeric-change count, presence of guidance verbs

Target: P(abs 5-min return > k*sigma | informative) vs boilerplate

Falsify-if: Informative and boilerplate classes have equal abnormal-move rates

Horizon: INTRADAY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B+

## W75A-E06 — Item 5.02 Officer Departure Severity

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation) Item 5.02 (Financial_Datasets list_filing_item_types confirms Item-5.02 exists)

Mechanism: Departure of CEO/CFO/CAO or principal officers carries more information than director changes; sudden departures without successor announce internal conflict or restatement risk.

Features: role regex (CEO/CFO/COO), 'effective immediately', successor-named flag, retire-vs-resign wording

Target: Abnormal 1d return and implied-vol change for NDX mega-caps

Falsify-if: Sudden-departure class shows no abnormal-return difference vs scheduled-retirement class after market-beta control

Horizon: DAILY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B+

## W75A-E07 — Item 4.02 Non-Reliance Restatement Shock

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation) Item 4.02

Mechanism: Non-reliance on previously issued financials is a discrete credibility event; high-information, rare, usually followed by 10-K/A or late filing.

Features: Item 4.02 presence, auditor involvement text, affected periods count

Target: Abnormal return drift and subsequent NT 10-K probability

Falsify-if: No abnormal return vs matched placebo days

Horizon: DAILY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B

## W75A-E08 — Item 1.05 Cybersecurity Incident Disclosure Latency

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation) Item 1.05 (UNVERIFIED this session; note Financial_Datasets item list omits 1.05, a coverage gap to test)

Mechanism: Material cybersecurity incidents are reported under a dedicated 8-K item with a business-day deadline (deadline text UNVERIFIED this session). Vendor item parsers that omit 1.05 would miss it, so the edge includes a coverage audit.

Features: Item 1.05 presence by direct EDGAR parse vs vendor parse, text severity, cross-filer breadth

Target: Missed-event rate per vendor and abnormal return around Item 1.05

Falsify-if: Vendor parse recall is 100 percent and abnormal return is null

Horizon: INTRADAY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B

## W75A-E09 — Items 1.01/1.02 Material Agreement Entry-Termination Pair

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation) Items 1.01 and 1.02

Mechanism: Entry into or termination of material agreements (supply, financing, customer) transmits supply-chain information to counterparties named in the exhibit.

Features: counterparty entity extraction, contract value, termination-for-convenience flag

Target: Counterparty abnormal return vs filer

Falsify-if: Counterparty effect is zero vs matched non-named peers

Horizon: DAILY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B

## W75A-E10 — Item 3.01 Listing Deficiency Notice

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation) Item 3.01

Mechanism: Exchange delisting/deficiency notices alter holder base (index deletion risk, forced selling).

Features: deficiency type (price, MVLS, late filing), cure period text

Target: Abnormal 3-day return and volume

Falsify-if: Null abnormal return vs matched deficient-but-undisclosed peers

Horizon: DAILY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B

## W75A-E11 — Item 8.01 Ambiguity Resolver via Same-Day Co-Items

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation) Item 8.01 with Item 9.01 exhibits

Mechanism: Item 8.01 is a residual bucket; same-filing co-items and exhibit type disambiguate its content.

Features: co-item vector, exhibit type (press release, deck, agreement), length

Target: Return-informativeness prediction before text modelling

Falsify-if: Co-item vector has no incremental AUC over 8.01-only

Horizon: INTRADAY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B

## W75A-E12 — 8-K/A Amendment Revision State

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation) amendments

Mechanism: Amendments correct or complete earlier items (e.g. Item 5.02 compensation details); a material amendment is a second information event that naive deduplication discards.

Features: amendment-to-original lag, changed-token share, item overlap

Target: Second-event abnormal move

Falsify-if: Amendment moves indistinguishable from placebo days

Horizon: DAILY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B

## W75A-E13 — Filing Time-of-Day Strategic Timing Prior

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation); EDGAR operating hours (UNVERIFIED this session; not stated on pages read)

Mechanism: Filers choose timing; negative disclosures are plausibly shifted to after-close or pre-holiday. Time-of-day is a prior on item sentiment.

Features: acceptance hour bucket, Friday/pre-holiday flag, item mix

Target: Sign prior for text sentiment conditional on timing

Falsify-if: Timing carries no incremental information over text sentiment

Horizon: DAILY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B

## W75A-E14 — Index-Constituent 8-K Breadth Pulse

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation)

Mechanism: Simultaneous filings across many NDX/S&P constituents (earnings season) change the systematic variance share intraday; breadth is a regime variable for index futures rather than a name signal.

Features: constituent-weighted count of accepted 8-Ks per 15 minutes, weight-by-index-share

Target: Subsequent realized-vol of NQ/ES over the next 30 minutes

Falsify-if: Breadth does not add to calendar+VIX-based vol forecast

Horizon: INTRADAY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B+

## W75A-E15 — Exhibit Size and Structure as Information Richness

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation)

Mechanism: Large exhibit sets (decks, supplemental tables) delay human reading and increase parse time; tiny filings are fast to digest.

Features: exhibit bytes, table count, parse-time

Target: Reaction-time half-life by filing size

Falsify-if: Half-life invariant to size

Horizon: INTRADAY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B

## W75A-E16 — FOMC Statement Token-Diff Hawkishness Index

Primary source: Federal Reserve FOMC statement/minutes (https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm); archived statement texts

Mechanism: Each statement is a small edit of the prior; changed phrases (not level) carry policy-path information. Token diff against previous statement, weighted by a lexicon of hawkish/dovish edits, forms an instantly computable score.

Features: added/removed n-grams, lexicon signed weight, paragraph-position weight, vote-dissent flag

Target: 5-minute and 30-minute returns of ZN/ZT, ES, 6E, GC after release

Falsify-if: Diff score has no explanatory power for rate futures after controlling for the concurrent market-implied surprise

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: S

## W75A-E17 — Statement-to-Press-Conference Divergence

Primary source: Federal Reserve FOMC statement/minutes (https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm); live transcript/captions (UNVERIFIED availability)

Mechanism: Press conference starts after the statement; tone divergence from statement can reverse the first reaction. Uses live-transcript chunk scores, not the later official transcript.

Features: statement diff score, rolling 2-minute chunk score of speaker, divergence = chunk - statement

Target: Sign of return from statement+5m to conference+30m

Falsify-if: Divergence does not predict continuation/reversal vs placebo meeting-days

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: A

## W75A-E18 — FOMC Minutes Revealed-Preference Gap

Primary source: Federal Reserve FOMC statement/minutes (https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm) (minutes released three weeks after the decision, verified)

Mechanism: Minutes disclose discussion nuance 3 weeks later; the gap between minutes tone and statement tone is a delayed information update to terminal-rate pricing.

Features: minutes-vs-statement tone gap, 'many/several/a few participants' counts

Target: Return and rate-vol on minutes day at release time

Falsify-if: No effect beyond OIS-implied move

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W75A-E19 — FOMC Calendar-Anchored Intraday Gate

Primary source: Federal Reserve FOMC statement/minutes (https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm) (2026 dates listed and marked tentative)

Mechanism: Meeting days are fixed in the calendar; statement release time not stated on the page fetched (UNVERIFIED). Gate: block new entries within a calibrated window before/after statement; the dates are tentative until confirmed at the preceding meeting.

Features: meeting-day flag, minutes-day flag, SEP-meeting flag, minutes-to-statement spacing

Target: Reduction in tail loss of existing intraday strategies when gate on

Falsify-if: Gate does not reduce loss tail beyond random-window placebo

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: A

## W75A-E20 — ECB Decision-Statement Diff vs Press-Conference Window

Primary source: ECB monetary policy decision and press conference (https://www.ecb.europa.eu/press/pressconf/html/index.en.html) (press conference watched live at 14:45 CET per page; decision release time UNVERIFIED)

Mechanism: ECB separates decision and press conference by a gap; the two windows have distinct information (Altavilla et al. type target/path/QE factors are literature, UNVERIFIED here). Diff in decision text sets the first-window move; conference sets the second.

Features: decision diff score, conference chunk score, window segmentation by clock

Target: Bund/BTP/EURUSD return decomposition by window

Falsify-if: Second-window return is unrelated to conference chunk score

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: A

## W75A-E21 — Cross-Central-Bank Statement Spillover

Primary source: Federal Reserve FOMC statement/minutes (https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm) and ECB monetary policy decision and press conference (https://www.ecb.europa.eu/press/pressconf/html/index.en.html)

Mechanism: Statement tone from one bank moves global duration and USD; tone divergence between Fed and ECB maps to EURUSD and carry.

Features: diff scores for Fed, ECB; difference; same-day overlap flag

Target: EURUSD and ZN 60-minute return

Falsify-if: Difference of scores adds nothing to rate-differential surprise

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W75A-E22 — Central-Bank Speaker Quiet-Period Exposure Map

Primary source: Federal Reserve FOMC statement/minutes (https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm) (blackout rules not on the fetched page; UNVERIFIED)

Mechanism: Outside blackout periods unscheduled speeches are information shocks; during blackout, surprise risk falls. Mapping the state allows lower risk gates.

Features: days-to-meeting, blackout flag (needs verified rule), speaker-hawkishness score

Target: Unscheduled headline density and vol

Falsify-if: Headline density same inside/outside blackout

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: B

## W75A-E23 — GDELT 15-Minute GKG Tone Shock

Primary source: GDELT 2.0 Events/GKG 15-minute files (https://www.gdeltproject.org/data.html)

Mechanism: GKG updates every 15 minutes (verified) with tone/themes/entities per article. Aggregating tone over economy/market themes yields a rolling attention-valence state that lags primary news by at least the file cadence plus crawl delay.

Features: mean tone and count per theme in latest file, z-score vs 30-day same-quarter-hour baseline

Target: NQ/ES 1h-ahead realized vol and sign conditional on shock

Falsify-if: Theme-tone shock has zero incremental power over VIX and calendar

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: B+

## W75A-E24 — GDELT Event-Root Conflict Burst for Oil and Gold

Primary source: GDELT 2.0 Events/GKG 15-minute files (https://www.gdeltproject.org/data.html) (CAMEO root codes; code-table UNVERIFIED here)

Mechanism: Bursts in conflict-class events in energy-producing/transit countries precede headline-driven energy and gold moves; GDELT is a slow aggregator so use as confirmation/regime, not trigger.

Features: event count by CAMEO root in a country basket, Goldstein-scale mean, burst z-score

Target: CL and GC intraday range expansion within 6 hours

Falsify-if: Burst z-score does not predict range expansion vs shuffled-country placebo

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: B+

## W75A-E25 — GDELT Date-Added vs Source-Publish Latency

Primary source: GDELT 2.0 Events/GKG 15-minute files (https://www.gdeltproject.org/data.html)

Mechanism: Fields that stamp when GDELT added a record versus when the article was published separate crawl delay from event time (field names UNVERIFIED this session). Measuring this distribution defines the legal embargo for GDELT features.

Features: added_time - publish_time distribution per source domain tier

Target: Conservative published_time per GDELT row

Falsify-if: Latency tail makes GDELT unusable below 1h for all domain tiers

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: A-

## W75A-E26 — Mention-Velocity Saturation Fade

Primary source: GDELT 2.0 Events/GKG 15-minute files (https://www.gdeltproject.org/data.html)

Mechanism: Story mention counts follow a saturating curve; the second derivative (velocity decline) marks when news is fully priced, giving a fade/exit state for headline trades.

Features: mentions per 15m, logistic fit, inflection time, source-count growth

Target: Post-inflection return drift sign

Falsify-if: No difference in post-inflection vs pre-inflection drift

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: B+

## W75A-E27 — Non-English First-Mention Lead

Primary source: GDELT 2.0 Events/GKG 15-minute files (https://www.gdeltproject.org/data.html) (65 translated languages, verified)

Mechanism: Stories may appear first in local-language outlets (Gulf, Asia) before English wires; GDELT translation lets first-mention time be taken as min across languages.

Features: min first-mention time by language group, lead over first English mention

Target: Lead distribution and return in the lead window for energy/FX

Falsify-if: Lead median is below GDELT cadence so unusable

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: B

## W75A-E28 — Theme-Volume Attention Regime vs VIX

Primary source: GDELT 2.0 Events/GKG 15-minute files (https://www.gdeltproject.org/data.html)

Mechanism: Aggregate economy-theme article volume is an attention measure orthogonal to implied vol; divergence (high attention, low VIX) flags complacent regime.

Features: theme volume z-score minus VIX z-score, rank

Target: Next-day realized vol surprise vs VIX

Falsify-if: Divergence adds nothing to a HAR-RV + VIX model

Horizon: DAILY

Availability: PUBLIC_NEAR_REALTIME

Priority: B

## W75A-E29 — Story Cluster Novelty Score

Primary source: GDELT 2.0 Events/GKG 15-minute files (https://www.gdeltproject.org/data.html) GKG plus own SimHash/MinHash clusters

Mechanism: Raw counts conflate syndication with new information; clustering by near-duplicate text and counting unique stories isolates novelty. Genuinely new clusters move markets more than re-syndications.

Features: cluster id, cluster age, unique-publisher count, novelty = 1/(1+cluster_age)

Target: Return response per new cluster vs old cluster

Falsify-if: Response equals for new and old clusters

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: A

## W75A-E30 — Syndication Inflation Placebo

Primary source: GDELT 2.0 Events/GKG 15-minute files (https://www.gdeltproject.org/data.html)

Mechanism: Placebo: replace unique-cluster counts with raw mention counts; if edge persists equally, the signal is volume/attention only.

Features: raw vs unique count difference, syndicate-network share

Target: Edge ratio unique/raw

Falsify-if: Unique-cluster count edge not above raw-count edge

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: B

## W75A-E31 — De-Duplicated Event Clock for Headline Gating

Primary source: GDELT 2.0 Events/GKG 15-minute files (https://www.gdeltproject.org/data.html) and wire feeds

Mechanism: A single event generates many timestamps; defining event time as the earliest cluster member across feeds avoids repeated triggers and double counting for gating.

Features: cluster first_seen across feeds, merge window parameter w, merge precision/recall on labeled sample

Target: Event-level (not article-level) risk gate

Falsify-if: Gate precision/recall not above article-level gate

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: A-

## W75A-E32 — Live Earnings-Call Incremental Tone

Primary source: Quartr transcript/event endpoints (connector read_transcript, list_events; doc https://quartr.com) (read_transcript supports fromTimestamp and incremental reads of live transcripts; tool schema verified)

Mechanism: Calls last ~an hour; tone of the first minutes and Q&A arrives while the stock trades. Incremental windows allow tone-to-return tests at 5-minute granularity without waiting for the final transcript.

Features: per-paragraph tone score, cumulative prepared-remarks tone, guidance-token counts, lastTimestamp lag

Target: Return from call start+10m to call end

Falsify-if: Cumulative tone adds nothing over 8-K/press-release surprise

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: A

## W75A-E33 — Q&A-Section Tone Delta

Primary source: Quartr transcript/event endpoints (connector read_transcript, list_events; doc https://quartr.com) read_transcript section='qna' (verified parameter)

Mechanism: Prepared remarks are scripted; Q&A is less so. Tone delta (Q&A minus prepared) reveals unscripted management stress.

Features: qna tone minus prepared tone, hedge-word rate, analyst follow-up count

Target: Post-call drift and next-day implied vol change

Falsify-if: Delta has no information after controlling prepared tone

Horizon: DAILY

Availability: LICENSED_REALTIME

Priority: A-

## W75A-E34 — Analyst Question Hostility and Guidance Probing

Primary source: Quartr transcript/event endpoints (connector read_transcript, list_events; doc https://quartr.com)

Mechanism: Repeated analyst questions on one topic (margins, demand) signal consensus worry before estimate revisions.

Features: topic repetition count, question length, negative-framing lexicon

Target: Estimate revision direction over next 5 days

Falsify-if: No relation with revision direction

Horizon: WEEKLY

Availability: LICENSED_REALTIME

Priority: B

## W75A-E35 — Call Start Slippage and Overrun

Primary source: Quartr transcript/event endpoints (connector read_transcript, list_events; doc https://quartr.com) list_events/get_event

Mechanism: Delayed call starts or long overruns may signal complex news; event scheduled-vs-actual time is observable.

Features: actual_start - scheduled_start, duration over trailing-mean

Target: Pre-call volatility and post-call abnormal move

Falsify-if: Slippage unrelated to abnormal move

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: B

## W75A-E36 — Mega-Cap Call Tone Breadth for NQ

Primary source: Quartr transcript/event endpoints (connector read_transcript, list_events; doc https://quartr.com)

Mechanism: A handful of NDX names (weights concentrated) reporting in sequence; aggregated weight-times-tone is an index-level state in earnings season.

Features: sum(weight_i*tone_i), count reported, dispersion

Target: NQ drift next-day vs equal-weight placebo

Falsify-if: Weighted tone not above equal-weighted

Horizon: DAILY

Availability: LICENSED_REALTIME

Priority: B+

## W75A-E37 — CFO-vs-CEO Speaking Share

Primary source: Quartr transcript/event endpoints (connector read_transcript, list_events; doc https://quartr.com)

Mechanism: CFO-dominated Q&A suggests numerical defensiveness; share change vs history is an unscripted-state variable.

Features: speaker share of words, change vs last 4 calls

Target: Next-quarter guidance-cut probability

Falsify-if: No relation

Horizon: SLOW_PRIOR

Availability: LICENSED_REALTIME

Priority: B

## W75A-E38 — Vendor LLM-Sentiment Backfill Lookahead Audit

Primary source: Alpha Vantage NEWS_SENTIMENT / EARNINGS_CALL_TRANSCRIPT (https://www.alphavantage.co/documentation/) (EARNINGS_CALL_TRANSCRIPT described as enriched with LLM-based sentiment signals, since 2010Q1)

Mechanism: LLM-based scores computed today on historical transcripts embed model knowledge of later outcomes; a backtest on them can leak.

Features: score stability across vendor model versions, score vs holdout of known-outcome events

Target: Leakage-adjusted edge

Falsify-if: Edge unchanged after replacing with a point-in-time frozen model

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A-

## W75A-E39 — Transcript Guidance-Change Phrase Detector

Primary source: Quartr transcript/event endpoints (connector read_transcript, list_events; doc https://quartr.com) / FMP earningsTranscript (Ultimate plan required)

Mechanism: Phrases like 'raising/lowering our outlook' are narrow, high-precision tokens for guidance changes available during the call.

Features: phrase match plus numeric extraction, direction, magnitude vs consensus

Target: Return from phrase time to +30m

Falsify-if: Phrase timing adds nothing to press-release guidance

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: A

## W75A-E40 — News-Vendor Publish-vs-Ingest Latency Map

Primary source: Alpha Vantage NEWS_SENTIMENT / EARNINGS_CALL_TRANSCRIPT (https://www.alphavantage.co/documentation/); FMP news (plan-gated); Financial_Datasets get_news; Bigdata.com search

Mechanism: Aggregators timestamp differently (publish time vs ingest time). Mapping per-vendor lag defines the point-in-time clock; connector tests this session hit rate-limit / plan gates (AV premium, FMP plan) which is itself a reliability finding.

Features: time_published vs first_seen by vendor, missing-rate, backfill-rate

Target: Per-vendor embargo parameter

Falsify-if: Vendors show equal lag distributions

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: A

## W75A-E41 — Relevance-Weighted Ticker Sentiment Aggregate

Primary source: Alpha Vantage NEWS_SENTIMENT / EARNINGS_CALL_TRANSCRIPT (https://www.alphavantage.co/documentation/) (ticker_sentiment/relevance fields UNVERIFIED this session)

Mechanism: Weighting article sentiment by relevance rather than counting suppresses incidental mentions.

Features: sum(rel*score)/sum(rel) over rolling 60m, article count floor

Target: Next-hour return for NDX names

Falsify-if: Weighted aggregate not above unweighted

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W75A-E42 — Cross-Vendor Sentiment Disagreement

Primary source: Alpha Vantage NEWS_SENTIMENT / EARNINGS_CALL_TRANSCRIPT (https://www.alphavantage.co/documentation/); Bigdata.com sentiment_tearsheet; Twelve Data company news

Mechanism: When vendors disagree, information is ambiguous; dispersion is an uncertainty gate, mean is the signal.

Features: std of z-scored sentiment across vendors, coverage overlap

Target: Absolute next-hour move predicted by dispersion

Falsify-if: Dispersion does not predict abs move

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W75A-E43 — Macro-Topic Headline Volume Gate

Primary source: Alpha Vantage NEWS_SENTIMENT / EARNINGS_CALL_TRANSCRIPT (https://www.alphavantage.co/documentation/) topics filter (topic list UNVERIFIED)

Mechanism: Topic-filtered article counts on macro/fiscal topics proxy event density before scheduled releases.

Features: topic article count per 30m, z-score

Target: Realized vol over next hour

Falsify-if: No incremental power over calendar

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W75A-E44 — Sentiment Vendor Re-Scoring Vintage Placebo

Primary source: Alpha Vantage NEWS_SENTIMENT / EARNINGS_CALL_TRANSCRIPT (https://www.alphavantage.co/documentation/)

Mechanism: Vendors may re-score history; store raw vintages and test whether re-pulls differ.

Features: hash of scored record across pulls, rescored fraction

Target: Fraction of history that is non-point-in-time

Falsify-if: Re-pulls identical (placebo passes)

Horizon: DAILY

Availability: UNKNOWN_MEASURED

Priority: B+

## W75A-E45 — Press-Release Feed vs Newswire Duplicate Resolution

Primary source: FMP press-releases endpoints (plan-gated; UNVERIFIED) and EDGAR Item 2.02

Mechanism: Same release arrives via multiple routes; the earliest route defines tradeable lag.

Features: route first_seen, route order frequency

Target: Which route to subscribe to

Falsify-if: One route always first by >1s but unreachable on license

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: B

## W75A-E46 — Wikipedia Daily Pageview Attention Shock for NDX Names

Primary source: Wikimedia Analytics pageviews API (https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/reference/page-views.html) (endpoints serve from 2015-07-01, verified)

Mechanism: Retail/institutional attention to company pages rises before and after news; daily series exposes attention shocks independent of price.

Features: log pageviews z-score vs 28-day median, human-agent filter, spike-minus-news-cluster residual

Target: Next-day absolute return/volatility

Falsify-if: Shock residual has no power after news-count control

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B+

## W75A-E47 — Wikipedia Macro-Concept Page Attention (Recession/Inflation)

Primary source: Wikimedia Analytics pageviews API (https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/reference/page-views.html)

Mechanism: Aggregate macro-concept page views track public worry cycles; slow, noisy regime prior.

Features: pageviews of selected macro pages, 7d vs 90d ratio

Target: Subsequent equity index drawdown probability

Falsify-if: No relation after VIX control

Horizon: WEEKLY

Availability: PUBLIC_BATCH

Priority: B

## W75A-E48 — Wikipedia Hourly Dump Intraday Attention (UNVERIFIED cadence)

Primary source: Wikimedia pageviews hourly dumps (https://dumps.wikimedia.org/other/pageviews/): format and latency not stated on page read

Mechanism: If hourly dumps publish with short lag they allow intraday attention features; unverified cadence means measurement is first task.

Features: dump publish lag, per-article hourly views

Target: Usable-latency verdict

Falsify-if: Publication lag exceeds several hours (not intraday)

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: B

## W75A-E49 — Wikipedia Edit-Burst on Company Pages

Primary source: MediaWiki recent-changes API (UNVERIFIED)

Mechanism: Edit bursts follow breaking events; edit-count minus pageview ratio flags insider-knowledge hot topics.

Features: edits per hour, unique editors, revert rate

Target: Event detection lead vs wires

Falsify-if: No lead over wire timestamps

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: B

## W75A-E50 — Google Trends Sampling-Noise Floor

Primary source: Google Trends (https://trends.google.com; official API availability UNVERIFIED, developers.google.com page 404 this session)

Mechanism: Trends returns sampled, normalized (0-100) relative series; repeated draws differ. Estimating draw variance gives a noise floor to test if attention signals exceed noise.

Features: variance across N repeated requests, normalization anchor stability

Target: Minimum detectable attention shock

Falsify-if: Variance too large to detect any shock at target horizon

Horizon: DAILY

Availability: UNKNOWN_MEASURED

Priority: B+

## W75A-E51 — Google Trends Query-Panel Relative Attention (Gold, Rates, Recession)

Primary source: Google Trends

Mechanism: Public interest in 'gold price', 'mortgage rates', 'layoffs' reflects household stress; use as slow prior with fixed-anchor normalization.

Features: multi-query panel normalized to an anchor term, weekly change

Target: Weekly return of GC/ZN

Falsify-if: No effect vs placebo terms

Horizon: WEEKLY

Availability: UNKNOWN_MEASURED

Priority: B

## W75A-E52 — Crypto Social Attention Gate (LunarCrush)

Primary source: LunarCrush API (https://lunarcrush.com/developers/api/endpoints) ; connector tools topic_time_series, cryptocurrencies

Mechanism: Social volume spikes precede high-vol phases in crypto; used as risk-gate not direction.

Features: social volume z-score, AltRank/Galaxy-type composites (definitions UNVERIFIED), sentiment dispersion

Target: BTC/ETH next-4h realized vol

Falsify-if: Social volume not predictive after volume+funding control

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W75A-E53 — Equity Social Attention for NDX Mega-Caps (LunarCrush stocks)

Primary source: LunarCrush API (https://lunarcrush.com/developers/api/endpoints) connector stocks tool

Mechanism: Equity coverage of social metrics lets attention spikes be compared with price/volume.

Features: mention volume z, bull/bear ratio, creator concentration

Target: Next-hour abs return

Falsify-if: No incremental over options volume

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W75A-E54 — Creator-Concentration Manipulation Filter

Primary source: LunarCrush API (https://lunarcrush.com/developers/api/endpoints) connector creator, creator_posts

Mechanism: Attention concentrated in few creators is cheap to manipulate; breadth-adjusted attention improves reliability.

Features: Herfindahl of post counts by creator, new-creator share

Target: Predictive power gap breadth-adjusted vs raw

Falsify-if: No gap

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W75A-E55 — X (Twitter) API Terms Gate

Primary source: X developer terms (https://developer.x.com/en/developer-terms/more-on-restricted-use-cases; HTTP 402 on fetch, UNVERIFIED)

Mechanism: Redistribution/commercial-use terms may bar storing content for modelling. Edge: legal source-status gate before any X-derived feature enters research.

Features: terms checklist: storage, derived metrics, display, rate tier cost

Target: Allowed-feature list

Falsify-if: Terms permit all uses (gate trivial)

Horizon: SLOW_PRIOR

Availability: UNKNOWN_MEASURED

Priority: B

## W75A-E56 — Reddit Mention Velocity Under API Terms

Primary source: Reddit Data API Wiki (https://support.reddithelp.com/hc/en-us/articles/16160319875092-Reddit-Data-API-Wiki; HTTP 403, UNVERIFIED)

Mechanism: Retail-forum ticker mention velocity is a small-cap/meme attention proxy; commercial terms need confirmation first.

Features: mentions per hour, unique authors, comment/score ratio

Target: Next-day abs return for high-retail names

Falsify-if: No effect vs placebo tickers; or terms bar use

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: B

## W75A-E57 — News-vs-Social Attention Divergence

Primary source: GDELT 2.0 Events/GKG 15-minute files (https://www.gdeltproject.org/data.html) + LunarCrush API (https://lunarcrush.com/developers/api/endpoints)

Mechanism: News flow without social echo = institutional-only event; social echo without news = rumor/meme. Divergence classifies event type.

Features: z_news - z_social, lead/lag cross-correlation

Target: Persistence of price move 1h-1d

Falsify-if: Both classes persist equally

Horizon: INTRADAY

Availability: PUBLIC_NEAR_REALTIME

Priority: B+

## W75A-E58 — Headline Latency Tier Ladder (Licensed vs Public)

Primary source: Own measurement: Dow Jones/Reuters/Bloomberg licensed feeds vs public RSS/EDGAR (vendor latency figures UNVERIFIED, none asserted)

Mechanism: Reaction to headlines is front-loaded; edge exists only where our feed tier is within reaction half-life. Ladder measures tiers' timestamps against price reaction onset.

Features: t_feed - t_first_price_move, per tier, per event type

Target: Which event classes tradeable at each tier

Falsify-if: Price reaction onset precedes all feeds we can hold

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: S-

## W75A-E59 — Headline-to-Price Reaction Half-Life by Event Type

Primary source: Own event study using licensed headlines + tick data

Mechanism: Half-life of absorption sets whether public-feed access suffices.

Features: time to 50% of 60s move, by scheduled/unscheduled and by asset

Target: Half-life table

Falsify-if: Half-lives below minimum feed latency for all types

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: A

## W75A-E60 — Public-Feed Catch-Up Decay Gate

Primary source: Own monitoring of public EDGAR/RSS vs paid

Mechanism: As public feeds converge to paid-feed timing, the residual advantage vanishes; the edge needs a decay monitor and automatic retirement.

Features: rolling median lag gap, p-value vs 0

Target: Retire/maintain flag

Falsify-if: Gap stays constant (no decay)

Horizon: SLOW_PRIOR

Availability: UNKNOWN_MEASURED

Priority: B+

## W75A-E61 — Scheduled vs Unscheduled Headline Split

Primary source: Federal Reserve FOMC statement/minutes (https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm); SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation)

Mechanism: Scheduled releases have known clocks; unscheduled have unknown; models fitted pooled mix regimes.

Features: scheduled flag from calendar, hazard of unscheduled headline per hour

Target: Separate response functions

Falsify-if: Pooled model fits equal

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W75A-E62 — Halt Code T1 News-Pending to 8-K Appearance Linkage

Primary source: Nasdaq Trader halt codes (https://www.nasdaqtrader.com/Trader.aspx?id=TradeHaltCodes; referenced in W27V-D03, not re-fetched)

Mechanism: A news-pending halt precedes disclosure; whether an 8-K item appears during/after the halt, and which, conditions resumption direction. LULD mechanics are owned by W27V.

Features: halt code, halt duration, first 8-K item after halt, press-release-in-halt flag

Target: Return from resume to +15m by disclosed item

Falsify-if: Item type does not predict resume direction

Horizon: INTRADAY

Availability: PUBLIC_EVENT_DRIVEN

Priority: A-

## W75A-E63 — Halt-Resume News Content Classifier

Primary source: SEC EDGAR data.sec.gov submissions API (https://www.sec.gov/edgar/sec-api-documentation) with halt feed

Mechanism: Resume prices incorporate content; classifier output at resume predicts continuation vs reversal.

Features: text class (positive/neutral/neg), halted-name NDX weight

Target: Index futures shadow-move at resume

Falsify-if: No relation vs LULD-only halts placebo

Horizon: INTRADAY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B+

## W75A-E64 — Event-Clustering Confidence Gate for Multi-Source Events

Primary source: GDELT + EDGAR + wire feeds

Mechanism: Confidence that independent sources describe the same event (Jaccard on entities within window) reduces false triggers.

Features: entity-set Jaccard, window w, source independence count

Target: Gate precision at fixed recall

Falsify-if: Precision unchanged vs single-source trigger

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: A-

## W75A-E65 — Duplicate-Alert Fatigue Throttle

Primary source: Own event stream

Mechanism: Repeated alerts on the same cluster should decay weight: weight = exp(-k*n_prior); prevents over-trading re-syndicated headlines.

Features: n_prior in cluster, k parameter

Target: Turnover reduction at equal edge

Falsify-if: Throttle lowers edge more than turnover

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: B

## W75A-E66 — Rumor-to-Confirmation Event State Machine

Primary source: Wire headline + EDGAR/press release confirmations

Mechanism: Unconfirmed reports (rumor) vs confirmed (filing) have different reaction/reversal rates; track state UNCONFIRMED->CONFIRMED->DENIED.

Features: state, time to confirmation, denial rate by source tier

Target: Reversal probability after denial

Falsify-if: Reversal rate equal across states

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: A-

## W75A-E67 — Pre-Announcement Silence Tell

Primary source: EDGAR + calendar

Mechanism: Absence of 8-K around expected events (e.g. missing earnings date confirmation) is informative; no-event is not zero.

Features: expected-vs-observed filing, days overdue

Target: Probability of negative surprise

Falsify-if: Overdue flag has no effect

Horizon: DAILY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B

## W75A-E68 — Macro Data Release Text Mirror (Statement Diff Template Generalization)

Primary source: BLS/BEA release text, Treasury refunding statements (W55T owns refunding)

Mechanism: The diff method extends to any templated release (BLS summary, Treasury statement).

Features: template-aligned diff score

Target: Return on release day

Falsify-if: No incremental over numeric surprise

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B

## W75A-E69 — Text and Attention Truth Ladder

Primary source: All W75A sources

Mechanism: Composite gate hierarchy: legal filings > structured vendors > unscripted text > attention aggregates > inferred sentiment.

Features: rung-labelled feature table with embargo per rung

Target: Governance object for every text/attention feature

Falsify-if: A feature is used above its rung without a measured latency tier

Horizon: SLOW_PRIOR

Availability: PUBLIC_EVENT_DRIVEN

Priority: S-

## Final architecture edge — Truth Ladder

Truth Ladder for text and attention state, from physical/legal fact to inference:
1. Primary legal fact: EDGAR accepted filing (accession, Item) and official central-bank page; clock = first_seen_time, never deadline.
2. Vendor-structured facts: parsed item/entity fields, with vintage hash.
3. Unscripted text: live transcript chunks, headlines; point-in-time frozen models only.
4. Aggregated attention: GDELT clusters, pageviews, Trends, social metrics, de-duplicated by event clusters.
5. Inference: sentiment scores, divergence states; promoted only through the intermediate-outcome gate (A source->intermediate outcome, B expectation revision, C return, D execution improvement).
Each rung may only gate or confirm the rung below it; no attention metric may directly size a position before its latency tier is measured.

## Highest-priority W75A tests

1. W75A-E01 8-K Item-Level First-Seen Latency Surface
2. W75A-E16 FOMC Statement Token-Diff Hawkishness Index
3. W75A-E17 Statement-to-Press-Conference Divergence
4. W75A-E32 Live Earnings-Call Incremental Tone
5. W75A-E58 Headline Latency Tier Ladder (Licensed vs Public)
6. W75A-E29 Story Cluster Novelty Score
7. W75A-E40 News-Vendor Publish-vs-Ingest Latency Map
8. W75A-E39 Transcript Guidance-Change Phrase Detector
9. W75A-E52 Crypto Social Attention Gate (LunarCrush)
10. W75A-E64 Event-Clustering Confidence Gate for Multi-Source Events
