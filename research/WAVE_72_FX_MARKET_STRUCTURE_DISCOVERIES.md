# Wave 72X — FX Market Structure and Fixing/Flow State

Namespace: **W72X**

Thesis: spot FX is a decentralized market whose price discovery is punctuated by scheduled, rule-defined clocks: the WM/Refinitiv 4pm London fix (5-minute window, median, time-sliced capture), 47 further intraday WMR fixes, the Tokyo 9:55 fix, the ECB concertation, the 10:00 New York and 15:00 Tokyo option cuts, CME 14:00 CT settlement and CME FX markers and fixing prices, plus a settlement and funding layer (CLS pay-in timeline, FX swap and cross-currency basis, central-bank swap lines). Order flow referenced to those clocks is predictable in timing and partly in sign, producing documented pre-fix drift and post-fix reversal, month-end amplification, and clock-aligned liquidity states. The target for an intraday multi-asset system is not an FX directional call but (a) clock-aware regime and risk-gate states that stop FX-driven moves from being misread as information in NQ/ES/rates/gold and (b) slow priors on dollar-funding stress that condition intraday behaviour.

Boundary: W62C owns CFTC positioning and crowding (this wave only adds FX-specific nowcast and FX-specific divergence); W78B owns generic execution-cost and DST/roll liquidity mechanics (this wave isolates the fix-specific displacement); W38O owns public swap-data (basis swaps) and W10B owns repo surfaces and basis-trade fragility (this wave adds the FX-swap and cross-currency basis leg); W70B owns Globex MDP 3.0 book microstructure; W26R owns equity rebalance forced flow; W80X (rates and Treasury structure) owns SOFR/repo/Treasury mechanics referenced here.

All candidates are research hypotheses only. Claude owns later implementation.

## W72X-E01 — Multi-Fix Clock-Proximity State Vector

Primary source: W72X-D01, D03, D04, D05 (WMR 4pm London + hourly intraday fixes; ECB concertation ~14:10 CET; CME 14:00 CT settlement; CME markers 16:00 NY/London, 15:00 Tokyo; CME FX fixing 10:00 NY)

Mechanism: Scheduled benchmark clocks concentrate order flow at known instants; the state that matters for an intraday multi-asset system is time-to-next-fix and time-since-last-fix per fix family, not a single 4pm flag.

Features: For each fix family f: tau_to(f), tau_since(f) in minutes, DST-resolved from IANA zones (Asia/Tokyo, Europe/Frankfurt, Europe/London, America/New_York, America/Chicago); one-hot of 'inside pre-fix ramp', 'inside fix window', 'post-fix reversal zone' with window lengths as calibration parameters.

Target: Realized FX 1-min vol and 6E/6J spread width as function of the vector; secondary: NQ/ES 1-min realized vol conditional on FX fix proximity.

Falsify-if: Falsify if a model using only generic hour-of-day dummies explains FX realized-vol variance as well as the fix-proximity vector (out-of-sample R2 difference <= 0 under purged walk-forward); negative control: placebo fix clocks shifted by +37 minutes.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: S

## W72X-E02 — DST-Mismatch Fix Displacement Window

Primary source: W72X-D01 (4pm London fix) + IANA tz database; US vs UK/EU DST transition calendars (UK clocks change last Sunday of Oct 2026 = 25 Oct; US first Sunday of Nov 2026 = 1 Nov; dates are calendar rules, verify in tzdb)

Mechanism: In weeks when UK/EU and US DST differ, the 4pm London fix lands at 12:00 ET instead of 11:00 ET, and the ECB concertation shifts from ~08:10 ET to ~09:10 ET. Any model trained on fixed-ET hours misaligns FX-driven flow with the NQ/ES session clock.

Features: mismatch_flag (0/1), fix_ET_hour, fix-to-NQ-bar offset; compare NQ 1-min volume/vol at 11:00-11:05 ET vs 12:00-12:05 ET inside vs outside mismatch weeks.

Target: Whether the hourly volume/vol bump attributable to the London fix moves with London time (not ET) across the mismatch; adjacent mechanism W78B-E51 (DST liquidity timing) is generic, this edge isolates the fix-specific displacement.

Falsify-if: Falsify if the NQ/ES volume-vol bump stays at the same ET minute across mismatch and non-mismatch weeks (difference-in-differences coefficient CI includes 0 over >=8 mismatch weeks); negative control: Tokyo 9:55 JST (no DST) bump.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: A+

## W72X-E03 — Unconditional W-Shaped Dollar Drift Into Fixes

Primary source: W72X-D15 (Krohn, Mueller, Whelan, Bank of Canada SWP 2021-48: USD appreciation into Tokyo 9:55, ECB and London fixes, depreciation after; JPY the exception)

Mechanism: Net dollar demand at fixes combined with dealer inventory limits produces systematic pre-fix USD appreciation and post-fix reversal in G10 against USD; the exploitable object after costs is conditional, not unconditional.

Features: dollar_basket_ret over [-60m,-5m] and [+5m,+60m] around each fix; per-currency signed contributions; excluding JPY as a separate branch.

Target: Sign and magnitude of pre-fix and post-fix basket returns, per fix, post-2019 sample, net of 6E/6J/6B/6A/6C futures cost ledger.

Falsify-if: Falsify if the pre-fix USD drift is not significantly positive post-2020 at 5% after HAC errors, or disappears when costs from W78B-E40 ledger are subtracted; negative control: random same-length windows not touching a fix.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W72X-E04 — Conditional Window-to-Window Reversal Coefficient

Primary source: W72X-D15 (panel regression: return in one window predicts opposite-signed return in the next window, strengthened after controlling contemporaneous order flow)

Mechanism: Inventory-risk models imply that the sign of the pre-fix return predicts the post-fix return with a negative coefficient; the coefficient may be time-varying with dealer risk capacity.

Features: beta_t = coefficient of ret(fix, +5..+60m) on ret(fix, -60..-5m) estimated rolling; interact with realized-vol percentile and month-end flag.

Target: Post-fix return sign predicted by pre-fix return sign (hit rate, magnitude) per fix.

Falsify-if: Falsify if the rolling beta is positive or indistinguishable from 0 over two consecutive 12-month blocks, or its sign flips on pure time-shift placebo clocks.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W72X-E05 — Post-2015 London Pre/Post-Fix Reversal Under the 5-Minute Window

Primary source: W72X-D14 (Evans, J. Banking & Finance 87, 2018: significant negative pre/post-fix price-change correlation across currencies, largest at month-end; sample used a one-minute fix window) + W72X-D01 (WMR now uses a 5-minute calculation window)

Mechanism: The Evans sample reflects a one-minute fix window; the benchmark was later moved to a 5-minute window with time-sliced capture and median, which reduces the payoff to concentrated window trading and may have attenuated or relocated the reversal.

Features: corr(ret[-30m,-5m], ret[+5m,+30m]) by calendar year; structural break test at the benchmark window change (exact date PROVENANCE_PENDING; use FX Global Code era 2015 as a prior bracket).

Target: Whether reversal strength before vs after the window change differs.

Falsify-if: Falsify if the correlation is statistically unchanged across the break and remains as negative as in the Evans sample at month-end (then the window change did not matter); or if it vanishes entirely post-break (then the edge is retired as SLOW_PRIOR only).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W72X-E06 — Month-End Fix Amplification Flag

Primary source: W72X-D14 (Evans: atypically large pre-fix price changes concentrated on last trading day of month) + W72X-D17 (Melvin and Prins 2015: month-end hedging identified through the fix)

Mechanism: Portfolio hedging and index-rebalance orders concentrate at the month-end 4pm fix, so both pre-fix volatility and post-fix reversal are larger on the last business day.

Features: is_last_bday, is_last_2_bdays, MTD cross-border equity return differential; fix-window vol ratio vs 20-day median.

Target: Pre-fix absolute 5-min move and post-fix reversal probability on month-end vs intra-month days.

Falsify-if: Falsify if month-end days show no higher incidence of top-5% absolute pre-fix moves than matched intra-month days over >=36 months; negative control: first business day (not a hedging date).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W72X-E07 — Equity-MTD Hedge-Pressure Predictor for the Month-End Fix

Primary source: W72X-D17 (Melvin and Prins, J. Financial Markets 22, 2015: month equity gains predict currency depreciation before end-of-month fix; full text restricted, abstract-level only)

Mechanism: Foreign holders of US equities hedge currency exposure; after a month of strong US equity gains, hedge notional rises and USD selling into the month-end fix follows. Sign depends on holder base and hedge ratio, so sign is estimated, not assumed.

Features: NQ and ES month-to-date return (from prior month last close to fix-minus-1h), also local-equity MTD for EUR/JPY/GBP blocs; ratio of MTD return to its 12m std.

Target: USD basket return in the last 3 hours before the month-end 4pm fix; secondary: post-fix drift.

Falsify-if: Falsify if the predictive coefficient has unstable sign across half-year blocks, or if replacing MTD return with a random-walk placebo of equal variance performs equally.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A+

## W72X-E08 — Fix-Window Edge Calibration (Centering Unverified)

Primary source: W72X-D01 (WMR 5-minute calculation window; exact centering relative to 16:00 not confirmed from the primary factsheet; third-party text conflicts) 

Mechanism: Strategy rules that avoid or target the fix need the true window edges. The LSEG factsheet confirms a 5-minute window and time-sliced median but not the offsets, so the edges must be estimated from the vol-spike shape and then replaced by the methodology document.

Features: Per-second absolute return and traded volume profile 15:50-16:10 London; estimate start/end by change-point detection; compare with candidate [-2.5,+2.5] and [-5,0] minutes.

Target: Estimated window offset with CI.

Falsify-if: Falsify if the profile shows no change-point consistent with any fixed 5-minute interval (then window membership is not usable as a rule parameter).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W72X-E09 — Hourly-Fix Placebo Ladder

Primary source: W72X-D01, D02 (WMR Intraday Spot rates: up to 47 additional fix times, produced on the hour in the LSEG availability table)

Mechanism: If the 4pm vol bump is a hedging-flow artifact, other hourly WMR fixes should show smaller bumps in proportion to flow; if it is a generic top-of-hour effect, all hours look similar.

Features: Vol bump ratio at each hourly fix vs the same minute of a non-fix reference (e.g. :20 past); rank vs flow importance.

Target: Dose-response of vol bump against fix importance.

Falsify-if: Falsify if bump ratios at 4pm are statistically equal to those at neighbouring non-benchmark top-of-hour times (then the fix has no incremental effect and the clock gate is retired).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W72X-E10 — Fix-Window Liquidity Paradox Execution Ledger

Primary source: W72X-D14 (Evans: EBS volume and depth rise sharply during fix window while spreads narrow; ratio of in-window to outside average spread 0.238-0.413 for the pairs shown, 2007-2013 EBS samples)

Mechanism: The fix window is cheap to cross in spread terms but price-biased by queued fix orders; a ledger that reports spread and adverse drift separately avoids both over-avoiding and over-trading it.

Features: Spread_in_window / spread_outside; signed impact over [t, t+5m] for marketable orders inside vs outside; both normalised by 1-min sigma.

Target: Cost per unit sigma split into spread, impact, post-fix reversal.

Falsify-if: Falsify if post-2015 fix-window spread is not narrower than baseline or if signed impact inside the window is indistinguishable from outside.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W72X-E11 — Pre-Fix Ramp Length Estimator

Primary source: W72X-D16 (Ito and Yamada, J. Int. Economics 109, 2017: Tokyo hedge trades reported by one market participant to start ~30 minutes before the fix; anecdote, not measured) + W72X-D14

Mechanism: Pre-hedging begins before the fix and produces a gradual price drift into it; the ramp length is a parameter to estimate per fix, not a fixed 30 minutes.

Features: Cumulative signed return from t_fix-L to t_fix for L in {5,10,15,30,45,60}; monotone fit of drift vs L.

Target: L* that maximises predicted post-fix reversal per unit risk, per fix and regime.

Falsify-if: Falsify if the drift curve is flat in L (no ramp) or L* is not stable across 6-month blocks.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W72X-E12 — Tokyo 9:55 JST Spike-and-Revert Signature in USD/JPY

Primary source: W72X-D16 (Ito and Yamada: concentrated trades at 9:55 JST, price spikes more frequent than London, reversal after the fix; Tokyo fixes are bank-specific rates) + W72X-D06 (CME eFIX lists WMR Tokyo 09:55)

Mechanism: Importers' predictable USD buying settled at bank fixes creates a transient USD/JPY spike that reverses; 00:55 UTC falls in the NQ overnight session, so the spike can contaminate USD/JPY-led NQ overnight signals.

Features: USDJPY 10-second return at 00:55 UTC vs 00:45; spike size in bp; reversal over next 5 min; NQ 1-min return correlation with the spike.

Target: Probability and size of reversal after spike; whether NQ moves coincident with the spike mean-revert too.

Falsify-if: Falsify if post-2015 spike frequency at 00:55 UTC is not above neighbouring minutes, or NQ co-moves with USDJPY at 00:55 no more than at placebo minutes.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W72X-E13 — Gotobi Settlement-Day Bias in the Tokyo Fix

Primary source: W72X-D16 (Ito and Yamada: order imbalance toward buying foreign currency is larger on days when payments are due; exact date set in the extracted text is truncated, so the gotobi set 5/10/15/20/25/month-end is a hypothesis, PROVENANCE_PENDING)

Mechanism: Japanese importers settle on customary dates, raising USD demand at the 9:55 fix on those dates; the bias is calendar-predictable and therefore testable at zero data cost.

Features: gotobi_flag (5th,10th,15th,20th,25th and last business day, rolling to prior business day on non-business days; set to be confirmed), USDJPY return [00:25,00:55] UTC and [00:55,01:25] UTC.

Target: Pre-fix USDJPY drift on gotobi vs non-gotobi.

Falsify-if: Falsify if the gotobi pre-fix drift is not larger than non-gotobi with CI excluding 0 over >=5 years; negative control: arbitrary 'pseudo-gotobi' days (3rd, 8th, ...).

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W72X-E14 — Tokyo 15:00 Option Cut and Marker Clock for JPY Crosses

Primary source: W72X-D04 (CME FX Marker at 3:00 pm Tokyo) + W72X-D21 (secondary: 3pm Tokyo FX option expiry convention; primary DTCC/OTC convention not verified)

Mechanism: A second Asia benchmark (15:00 Tokyo = 06:00 UTC) concentrates USD/JPY and cross hedging before London opens; relevant as a pre-London liquidity state for NQ overnight.

Features: Distance of USDJPY to large strikes (if public expiry lists used) at 06:00 UTC; return and vol around 15:00 Tokyo vs placebo hour.

Target: USDJPY vol and reversal around 15:00 Tokyo.

Falsify-if: Falsify if realized vol and signed reversal around 15:00 Tokyo equal those at placebo times of day after matching on event calendars.

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: B

## W72X-E15 — ECB Concertation Window Reversal in EUR Crosses

Primary source: W72X-D03 (ECB: daily concertation procedure among central banks normally around 14:10 CET; rates published ~16:00 CET) + W72X-D14 (Evans includes the ECB fix among scheduled-event windows)

Mechanism: The ECB reference rate is a point-in-time snapshot; order flow referencing it clusters near the snapshot, but publication at 16:00 CET is after the event, so only the snapshot time is usable as a decision-time clock.

Features: EURUSD/EURGBP/EURJPY return and spread in [13:55,14:25] CET; pre/post-snapshot correlation; DST-aware (CET vs CEST).

Target: Reversal after 14:10 CET snapshot; effect on Bund/ES 1-min vol at the same time.

Falsify-if: Falsify if the vol and reversal at 14:10 CET equal placebo times; if the ECB moves the concertation time (check ECB page version each quarter), the clock must be re-versioned.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W72X-E16 — ECB Publication-Time Leak Guard

Primary source: W72X-D03 (ECB reference rates: snapshot ~14:10 CET, publication ~16:00 CET, downloads CSV/XML/SDMX)

Mechanism: Using the published ECB reference rate as a feature at 14:15 CET leaks ~1h45m of future information; the guard enforces published_time as availability.

Features: feature_available_time = max(published_time, ingest_time); unit test comparing backtest availability vs publish timestamps in the ECB CSV.

Target: Leak test pass/fail for any feature derived from ECB reference rates.

Falsify-if: Falsify the guard only if the ECB changes publication to real time; any strategy using the daily rate before publication fails the leak audit.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: A-

## W72X-E17 — BTIC Volume Share as Fix-Flow Proxy

Primary source: W72X-D06 (CME FX product guide: EURUSD BTIC references next WMR 4pm London; Euro FX spec: BTIC trading close 3:40-4:30 pm London / 9:40-10:30 am CT)

Mechanism: Basis-trade-at-index-close futures let participants trade futures at the next WMR fix; high BTIC share of total 6E volume signals large fix-referenced orders about to be worked.

Features: BTIC volume / (outright 6E volume) over trailing 1-3 days; BTIC OI change; BTIC trade-time distribution relative to 15:40 London.

Target: Fix-window absolute move and post-fix reversal on days with high BTIC share.

Falsify-if: Falsify if BTIC share has zero incremental power over month-end and vol controls; data per-trade BTIC timing requires CME licensed data (LICENSED/PAID), EOD volume is public.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W72X-E18 — Month-End BTIC+ (6EP) Hedge-Pressure Gauge

Primary source: W72X-D06 (CME FX BTIC+ references month-end WMR 4pm London, rule chapter 261B, product code 6EP)

Mechanism: 6EP isolates month-end fix-referenced hedging, so its open interest and volume are a cleaner gauge than outright volume for the month-end amplification effect.

Features: 6EP volume and OI in last 5 business days, net change; ratio to 6EB.

Target: Month-end fix absolute pre-fix move and sign of USD pressure.

Falsify-if: Falsify if 6EP activity does not rank-correlate with realised month-end fix volatility over >=24 months; sparse liquidity may make the series too thin (then retire).

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B

## W72X-E19 — BTIC Halt-Window Post-Fix Liquidity Thinning

Primary source: W72X-D06 (Euro FX spec: BTIC close 3:40 pm to 4:30 pm London on Globex)

Mechanism: The BTIC market pauses just before and after the fix; whether outright 6E depth thins during the same period measures how much fix-time liquidity lives in BTIC rather than outright.

Features: 6E top-5 depth and spread 15:30-16:45 London on BTIC-active days; ratio to outside-window depth.

Target: Execution cost for 6E (and 6J) during 15:40-16:30 London.

Falsify-if: Falsify if 6E depth and spread in the BTIC-close window are equal to matched non-fix windows.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W72X-E20 — CME Marker vs Daily Settlement Divergence

Primary source: W72X-D04 (CME markers at 16:00 NY, 16:00 London, 15:00 Tokyo using the same base methodology; daily settlement at 14:00 CT)

Mechanism: Markers and the 14:00 CT settlement use the same VWAP-or-mid method at different times, so the marker-settlement drift isolates intraday price change between valuation clocks, and the difference between marker error vs spot gives a tier-quality diagnostic.

Features: marker_NY(16:00) - settle(14:00 CT) minus spot change over the same interval; absolute value z-scored.

Target: Valuation noise indicator for futures-vs-spot reconciliation; stress flag when |diff| exceeds calibrated threshold.

Falsify-if: Falsify if the divergence is fully explained by spot change (R2 > 0.99) with no residual information.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B

## W72X-E21 — CME Marker Tier Occupancy as 4pm Futures-Liquidity Flag

Primary source: W72X-D04 (marker tiers: Tier 1 three or more trades in the 30-second window; Tier 2 bid/ask mid; Tier 3 external vendor rates)

Mechanism: Tier fall-through reveals that the nearby futures traded fewer than three prints in the 30s window; a tier-2/3 outcome at 16:00 London in 6E would mark an unusually thin fix-time futures market. Whether CME publishes the tier used per marker is not verified.

Features: tier_used(marker) if published; else proxy trades in last 30s from MDP trade summary.

Target: Fix-time liquidity quality indicator.

Falsify-if: Falsify if tier information is not published or recoverable (PROVENANCE_PENDING for the publication path) or if tier-2/3 events carry no vol/spread information.

Horizon: DAILY

Availability: UNKNOWN_MEASURED

Priority: B

## W72X-E22 — CME 14:00 CT FX Settlement-Window Pressure vs Equity Index Clock

Primary source: W72X-D04, D06 (CME daily settlement at 14:00 CT for major G7 FX futures; Euro FX spec lists Settlement time 14:00 CT)

Mechanism: FX futures settle at 15:00 ET, while NQ/ES rebalancing flow builds into the 16:00 ET cash close; FX settlement-window order flow can coincide with the late-session equity flow.

Features: 6E/6J 1-min signed volume in [13:55,14:05] CT; NQ 1-min return in same window and the following 30 min.

Target: Whether FX futures settlement-window imbalance leads NQ returns in the 15:00-15:30 ET window.

Falsify-if: Falsify if cross-correlation of FX settlement-window imbalance with NQ is not different from placebo windows (13:30 CT) after day-of-week and macro-event controls.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W72X-E23 — 10:00 New York Option-Cut Pinning Distance

Primary source: W72X-D05 (CME: FX options on futures expire 10:00 a.m. New York time since 9 June 2019, aligned to OTC convention; European-style, auto-exercised vs fixing price) + W72X-D21 (secondary FX expiry lists)

Mechanism: Large OTC/listed strikes near spot can pin price until 10:00 ET and release afterward; 10:00 ET is also a US equity-open macro-release slot, so release and data collide.

Features: dist = |spot - K| / sigma_1h for the largest known strike (CME option OI by strike is available; OTC strike lists are secondary and PROVENANCE_PENDING); minutes to cut; post-cut vol ratio.

Target: Pre-cut realised vol suppression and post-cut vol expansion in EURUSD/USDJPY; effect on NQ 10:00-10:15 ET.

Falsify-if: Falsify if realised vol does not drop when dist is small and does not rise post-cut vs matched days without large nearby strikes; negative control: strikes far away.

Horizon: INTRADAY

Availability: PUBLIC_BATCH

Priority: A

## W72X-E24 — 10:00 ET Option-Cut by Macro-Release Collision

Primary source: W72X-D05 (10:00 a.m. New York options expiry) + exact data release times to be taken from agency calendars (BLS/Census/ISM/Conference Board release times are UNVERIFIED here and must be sourced per series)

Mechanism: When option-cut and 10:00 ET releases coincide, FX pinning breaks at the same moment as information arrives, so FX-implied NQ cross-asset reaction is mis-attributed; separating these cases cleans FX-to-NQ transmission estimates.

Features: collision_flag = 1 if a tier-1 release lands within +/-1 minute of 10:00 ET; FX 1-min vol, NQ 1-min vol with and without collision.

Target: Cross-asset reaction attribution error.

Falsify-if: Falsify if reaction functions estimated with and without collision flags are statistically identical.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W72X-E25 — CME FX Fixing Tier-Fallthrough State at 10:00 ET

Primary source: W72X-D05 (CME FX fixing 60-second interval 9:59:00-9:59:59 ET; Tier 1 VWAP if 20+ contracts, else Tier 2 mid, else Tier 3 synthetic from vendor spot and forward points)

Mechanism: The fixing price drives auto-exercise of expiring FX options; a tier fall-through in a thin contract means the settlement reference was formed from mid or synthetic data, raising reference-price uncertainty that can show up as later-day re-pricing.

Features: contracts traded in the 60-second window per product; tier_used; |fixing - spot mid at 10:00:00|.

Target: Reference-price error and subsequent move on expiry days.

Falsify-if: Falsify if |fixing - spot| shows no tier dependence; fixing prints are public (channel 320 MDType W) but historical tier flag is not verified.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B

## W72X-E26 — CLS Pay-In Window Clock as Europe-Morning USD Liquidity State

Primary source: W72X-D07 (CLS operational timeline: settlement 07:00-09:00 CET, early-closing currencies funding completion target 10:00 CET, late-closing 12:00 CET; revised pay-in schedule 06:30 CET; deck Feb 2022)

Mechanism: CLS pay-ins draw large currency balances in a fixed European morning window; if intraday USD/EUR funding supply is tight, FX swap and short-end rates should show clock-aligned stress that spills into rate futures.

Features: Minutes since 07:00 CET; high-gross-settlement-day flag (using CLS monthly volume surprise); SOFR/ESTR futures 1-min vol in 07:00-12:00 CET.

Target: Co-movement of short-rate futures vol with CLS pay-in window on heavy days.

Falsify-if: Falsify if vol in the pay-in window is not above clock-matched windows on heavy-settlement days, or the CLS schedule changes (re-version). Intraday CLS data is not public, so this is a clock hypothesis only.

Horizon: INTRADAY

Availability: PUBLIC_WEB_ONLY

Priority: B

## W72X-E27 — CLS Weekend Closure and Sunday Reopen Gap Clock

Primary source: W72X-D07 (CLS operates 5.5 days per week, closing 02:00 CET Saturday and reopening 22:00 CET Sunday)

Mechanism: Settlement infrastructure is dark over the weekend; Sunday-evening FX and the Globex Sunday open occur around CLS reopening, aligning pre-funding and gap-resolution behaviour.

Features: minutes since CLS reopening (22:00 CET Sunday); FX gap vs Friday close; NQ Sunday-open gap sign agreement with FX gap.

Target: Predicted continuation vs fill of Sunday gaps conditional on FX gap and CLS clock.

Falsify-if: Falsify if gap-fill statistics are independent of the CLS clock after conditioning on weekend news; adjacent execution mechanics are in W78B-E40.

Horizon: INTRADAY

Availability: PUBLIC_WEB_ONLY

Priority: B

## W72X-E28 — CLS Monthly Volume Surprise as FX Liquidity Slow Prior

Primary source: W72X-D08 (CLS monthly FX trading activity reports; e.g. average daily submitted volume USD 2.83T in June 2026, USD 2.96T in March 2026 per CLS listing)

Mechanism: Persistent changes in settled volume reflect dealer and investor activity; monthly surprise vs seasonal expectation conditions FX realized-vol and depth for the next weeks.

Features: z_t = (log ADV_t - seasonal mean)/std; lag of publication (reports appear weeks after month end; exact lag measured).

Target: Next-month FX realized vol, spreads, and cross-asset correlations (NQ vs USD).

Falsify-if: Falsify if z_t has no information beyond lagged realised vol and VIX at monthly horizon; release lag must be measured (UNKNOWN_MEASURED).

Horizon: SLOW_PRIOR

Availability: PUBLIC_DELAYED

Priority: B

## W72X-E29 — CLS Intraday Spot Volume Product Lead (Licensed)

Primary source: W72X-D08 (CLS data suite lists intraday FX spot volume product; The Hedge Fund Journal describes executed intraday spot trades for 18 currencies and 33 pairs; CLS terms/pricing PROVENANCE_PENDING)

Mechanism: If a licensed near-real-time spot volume feed exists with sub-hourly granularity, volume surprise could lead vol; availability, latency, and rights are unverified.

Features: bucketed volume surprise vs same-time-of-day median; lag to publication.

Target: Next-30-minute FX realised vol and NQ/FX correlation.

Falsify-if: Falsify as unusable if the feed is not available at our latency or rights; otherwise falsify if surprise has no predictive power over contemporaneous futures volume.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: B

## W72X-E30 — US T+1 Securities Settlement FX Pre-Funding Compression

Primary source: W72X-D07 (CLS 9 April 2024 note: IPIS deadline stays 00:00 CET, trades can be submitted until 06:30 CET; ~1% of CLS ADV is T+1 USD trades involving funds; 40-50% of that could settle outside CLS)

Mechanism: US T+1 compresses the window to buy USD for US equity purchases; large NQ/ES-linked inflow days may raise FX demand in the Asian/European morning following.

Features: NQ/ES prior-day signed notional (proxy: volume x return), next-morning USD basket move (00:00-08:00 UTC), controlling for rates.

Target: USD pressure in the Asia/Europe morning after high US equity-flow days.

Falsify-if: Falsify if the coefficient is zero before vs after May 2024 (difference-in-differences) or placebo with non-US equity index.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B

## W72X-E31 — CLS-to-BIS Coverage Ratio Drift

Primary source: W72X-D08, D11 (CLS settlement volume vs BIS turnover; Hasbrouck-Levich NBER WP 23206 found CLS settled volume at 37.2% of BIS spot turnover in April 2013)

Mechanism: The ratio of CLS-settled volume to BIS-reported turnover tracks how much trading nets internally or settles bilaterally; a rising off-CLS share implies more internalization and potentially thinner lit price discovery.

Features: ratio_t = CLS ADV_t / BIS turnover (triennial, interpolated) per pair; trend and break detection.

Target: Slow prior on lit-market fragility and cross-venue dispersion.

Falsify-if: Falsify if ratio trends do not predict EBS/CME spread behaviour; ratio mismatch of definitions (net-net vs gross) should be harmonised first.

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B

## W72X-E32 — Last-Look Reject-Rate Adverse-Selection State

Primary source: W72X-D09 (GFXC last look paper: LPs should disclose price-check method and window length; GFXC Principle 17)

Mechanism: On venues with last look, reject rate rises when mid moves in the LP's favour inside the hold window; a rising own reject rate marks short-term adverse-selection pressure and is observable in our own order records.

Features: reject_rate_rolling(5m), reject conditional on post-request mid move, reject asymmetry by side.

Target: Next-5-minute FX realised vol and markout; gate for FX spot execution via last-look LPs.

Falsify-if: Falsify if reject rate carries no information beyond contemporaneous realised vol; applies only if the system routes FX via LPs with last look (futures-only routing makes this null).

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: B+

## W72X-E33 — Hold-Time Asymmetry Audit

Primary source: W72X-D09 (GFXC paper: hold times and asymmetric hold times discussed; Principle 17 expects fair, disclosed last look)

Mechanism: If accept responses and reject responses take different time, the LP may be using hold time asymmetrically; the audit compares latency distributions of accepts and rejects on our own flow.

Features: Latency_accept, latency_reject distributions; KS and quantile gaps; vs disclosed max/min window.

Target: Pass/fail test of asymmetric hold behaviour per LP; routing penalty.

Falsify-if: Falsify if accept and reject latency distributions are statistically indistinguishable (KS p>0.1 on >=1000 trades each).

Horizon: WEEKLY

Availability: UNKNOWN_MEASURED

Priority: B

## W72X-E34 — Price-Tolerance Asymmetry Audit

Primary source: W72X-D09 (GFXC paper: symmetric price check applies same tolerance both directions; asymmetric check applies different; Disclosures Cover Sheet 3-ll)

Mechanism: A claimed symmetric check should reject equally often on adverse and favourable mid moves; asymmetric rejection is detectable from outcomes.

Features: P(reject | favourable move to us) vs P(reject | adverse move) at matched move magnitudes in pips.

Target: Asymmetry index per LP; slippage-adjusted LP ranking.

Falsify-if: Falsify if the asymmetry index CI includes 0 across LPs, or if disclosure says symmetric and measured is symmetric.

Horizon: WEEKLY

Availability: UNKNOWN_MEASURED

Priority: B+

## W72X-E35 — Last-Look vs Firm-CLOB Quote Divergence at News

Primary source: W72X-D09, D10, D20 (EBS Market is described as a firm central limit order book; LSEG states no last-look in Spot Matching; LP streaming quotes may use last look)

Mechanism: At news, LP last-look quotes can widen or reject while firm CLOB books show executable depth; the gap between executable depth in the firm book and indicative LP quote is a measure of latent adverse selection.

Features: EBS top-of-book depth and spread vs LP quote spread/reject rate in the minute after tier-1 releases.

Target: Choice of venue for FX execution and a news-regime flag for NQ/FX cross hedges.

Falsify-if: Falsify if LP quote spreads and reject rates track EBS spreads one-for-one at news (no divergence).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W72X-E36 — Last-Look Disclosure Drift Prior

Primary source: W72X-D09 (GFXC: LPs should disclose max/min last-look window, price-check symmetry, cover-and-deal; individual LP disclosure numbers not fetched)

Mechanism: LP disclosures are slow-moving but changeable; tracking disclosure changes provides a versioned prior for routing decisions.

Features: diff of disclosure cover sheet fields across versions; hash and date.

Target: Slow prior on LP quality.

Falsify-if: Falsify if disclosed window length does not match measured hold time (then disclosure carries no information).

Horizon: SLOW_PRIOR

Availability: PUBLIC_WEB_ONLY

Priority: B

## W72X-E37 — EBS Microstructure Regime-Break Gate (Quarter-Pip, MQL, Faster Data)

Primary source: W72X-D10 (CME 17 June 2024: faster market data, lower MQLs and granular price increments rolled out Q1 2024 starting with AUD/USD and EUR/USD; EUR/USD top-of-book average 0.63 pips, 30% reduction; over 20% of EUR/USD volume on quarter or three-quarter pip increments)

Mechanism: Structural changes in the primary spot market change tick size, quote life and adverse selection, breaking stationarity of any EUR/USD spot microstructure estimate trained across Q1 2024.

Features: break_date per pair (staggered: AUD/USD, EUR/USD first); version stamp per feature; pre/post-regime separate calibration.

Target: Stability of spread, impact, and depth-based features across the break.

Falsify-if: Falsify if feature distributions pre/post break are statistically identical (then pooling is safe); gates stay otherwise. Exact MQL values by date are PROVENANCE_PENDING.

Horizon: SLOW_PRIOR

Availability: PAID_REALTIME

Priority: A-

## W72X-E38 — EBS Top-of-Book Post-Event Spread Normalization Half-Life

Primary source: W72X-D10 (CME: EUR/USD median spreads 17% lower over U.S. CPI release than in prior month, measured 5 minutes post release, April vs March 2024)

Mechanism: Spread normalization speed after tier-1 releases measures liquidity provider re-entry; a slow half-life in EUR/USD should coincide with thin NQ depth recovery.

Features: tau_half = time for EUR/USD top-of-book spread to return halfway to pre-event median; same for NQ spread/depth.

Target: Whether EUR/USD tau_half predicts NQ tau_half and the follow-through of the first 5-minute move.

Falsify-if: Falsify if EUR/USD tau_half has no incremental power for NQ depth recovery after controlling for VIX and event surprise.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W72X-E39 — Quarter-Pip Share and Price-Point Occupancy Tick-Grid Feature

Primary source: W72X-D10 (CME: ~90% of price points traded vs ~60% before one-fourth pip increments; over 20% of EUR/USD volume on quarter/three-quarter increments; price discretion inside the spread)

Mechanism: The proportion of volume at fractional increments measures how much trading happens inside the old tick grid, a proxy for hidden/discretionary interest and competition for queue priority.

Features: frac_pip_vol_share, price-point occupancy per 5-min bucket.

Target: Spread and impact prediction for EUR/USD short-horizon orders.

Falsify-if: Falsify if fractional share has no predictive power for next-bucket spread or realised markouts.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W72X-E40 — Depth-Within-2.5-Pips Inventory Gate

Primary source: W72X-D10 (CME: +22% order volume available down to 2.5 pips depth in EUR/USD book after the changes)

Mechanism: Resting inventory within a fixed pip band is a direct resilience measure; a drop signals liquidity withdrawal before price gaps.

Features: depth_2.5 normalised by its 20-day time-of-day median; first difference; interaction with scheduled-event proximity.

Target: Probability of >=3 sigma 1-minute EUR/USD move in the next 5 minutes.

Falsify-if: Falsify if depth_2.5 has no marginal predictive power over spread alone.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W72X-E41 — FX Link Futures-vs-Spot Spread Deviation From Carry

Primary source: W72X-D19 (CME FX Link: CLOB for spreads between OTC spot and FX futures; FX Swap Rate Monitor implied rate differential from FX Link swap points)

Mechanism: FX Link price equals the futures-minus-spot spread; carry parity says it should equal forward points to the IMM date. Deviation measures funding and balance-sheet friction.

Features: dev = FX_Link_mid - (spot x (r_usd - r_eur) x tau); use SOFR/ESTR curves; z-scored by time to expiry.

Target: Funding-stress state; leading indicator for USD funding spikes around quarter-end and for 6E basis-related execution costs.

Falsify-if: Falsify if dev is fully explained by SOFR-ESTR differentials with R2 > 0.98.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W72X-E42 — FX Spot+ Launch Event Study

Primary source: W72X-D19 (CME describes FX Spot+ as an all-to-all spot CLOB in Chicago using implication technology and FX Link; launch status/date UNVERIFIED)

Mechanism: If launched, spot-in-futures-terms liquidity changes who shows liquidity and how spot and futures link, possibly lowering futures-spot dispersions.

Features: pre/post spread and dispersion of EBS vs futures-implied spot.

Target: Structural-break gate for FX microstructure.

Falsify-if: Retire the edge if product is not launched or no measurable change appears; source status PROVENANCE_PENDING.

Horizon: SLOW_PRIOR

Availability: PUBLIC_WEB_ONLY

Priority: B

## W72X-E43 — IMM Roll-Week 6E Liquidity Crossover

Primary source: W72X-D06 (Euro FX spec: quarterly Mar/Jun/Sep/Dec contracts plus serials; trading terminates 9:16 a.m. CT two business days before the third Wednesday; physical delivery)

Mechanism: Liquidity migrates from front to next quarterly contract in a predictable window before expiry; adverse selection and roll costs spike if the system sits in the wrong contract.

Features: front/second share of volume, spread, depth by day-to-expiry; migration day estimate.

Target: Optimal roll day and cost per roll for 6E/6J/6B.

Falsify-if: Falsify if migration day varies more than +/-2 days with no calendar predictor; adjacent mechanics for ES/NQ in W78B-E44.

Horizon: WEEKLY

Availability: PUBLIC_SCHEDULED

Priority: B

## W72X-E44 — 6E Expiry-Day Pre-9:16 CT Volatility Cluster

Primary source: W72X-D06 (6E last trade 9:16 a.m. CT; final settlement increment 0.00005)

Mechanism: Physically delivered contracts show closing-out and delivery-intent flow in the expiring contract's last minutes; the 9:16 CT cut falls shortly before US equity open and macro slots.

Features: Expiring-contract volume, spread, and 1-second returns 9:00-9:16 CT; relation to remaining OI.

Target: Execution-quality cost multiplier for 6E at expiry.

Falsify-if: Falsify if expiry-day last-15-min vol in expiring contract is not above matched non-expiry days.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W72X-E45 — FX-Swap-Implied Rate Differential vs OIS Gap Around Central-Bank Events

Primary source: W72X-D19 (CME FX Swap Rate Monitor: implied rate differential from mid-market FX swap points) + OIS/SOFR sources in W80X

Mechanism: At FOMC/ECB, futures-implied USD funding cost via FX swap should move with OIS; a widening gap between FX-swap-implied and OIS-implied differentials signals balance-sheet scarcity.

Features: gap_t = implied_diff_FXswap - implied_diff_OIS; change over [-10m,+30m] around event.

Target: Funding-stress flag and NQ drawdown risk after FOMC.

Falsify-if: Falsify if gap changes carry no information beyond OIS moves or if gap is mostly noise at intraday frequency.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W72X-E46 — Quarter-End Cross-Currency Basis Spike Window

Primary source: W72X-D12 (BIS Quarterly Review Sep 2016: since 2014 basis exhibits quarter-end spikes along with repo rates; linked to regulatory reporting dates)

Mechanism: Banks window-dress balance sheets at reporting dates, reducing arbitrage capacity; basis and repo spike together, which affects funding-sensitive trades and index futures microstructure near quarter-end.

Features: days_to_quarter_end, quarter-end flag, 1w/1m basis (licensed) or CME FX Link deviation proxy; repo spreads (see W80X).

Target: Cross-asset vol conditioning in the last 3 days of each quarter.

Falsify-if: Falsify if spikes have disappeared post-2022 (regulatory change) or have no ES/NQ liquidity relevance.

Horizon: SLOW_PRIOR

Availability: PAID_REALTIME

Priority: A-

## W72X-E47 — Year-End Turn Tenor Kink

Primary source: W72X-D12 (BIS: quarter-end spikes; year-end bigger per Risk.net, paywalled, secondary; PROVENANCE_PENDING for magnitudes)

Mechanism: FX-swap pricing across tenors shows a kink where the tenor crosses year-end; the kink size is a stress gauge and can precede equity liquidity thinning in late December.

Features: kink = swap_pts(tenor spanning YE) - interpolated; timing of onset (days before).

Target: Late-December index-futures liquidity and gap risk.

Falsify-if: Falsify if kink size shows no relation to NQ/ES late-December spreads or realised vol.

Horizon: SLOW_PRIOR

Availability: PAID_REALTIME

Priority: B

## W72X-E48 — Basis-Repo Co-Spike Joint State

Primary source: W72X-D12 (BIS: basis and repo rates spike together at quarter-end) + W80X repo sources

Mechanism: Cross-currency basis and USD repo share a common balance-sheet constraint; joint spike distinguishes balance-sheet scarcity from isolated FX hedging demand.

Features: z(basis_1m) and z(SOFR-IORB or GC-SOFR); joint exceedance; lead-lag.

Target: ES/NQ closing auction vol and basis when joint spike occurs.

Falsify-if: Falsify if the joint-spike state adds nothing beyond either series alone for NQ close imbalance outcomes; extends W10B-E07/E09 repo surfaces with FX leg.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A-

## W72X-E49 — JPY Basis Hedging-Demand Prior

Primary source: W72X-D12 (BIS 2016: widening basis raised BIS-reporting banks' claims on the Japanese official sector; hedging demand plus limited arbitrage capacity)

Mechanism: A wide JPY/USD basis means hedged USD assets cost more for Japanese investors, shifting flows into unhedged USD assets and increasing USD/JPY sensitivity to risk.

Features: JPY 3m basis level and change; USDJPY vs NQ rolling correlation conditional on basis tercile.

Target: NQ-USDJPY correlation regime.

Falsify-if: Falsify if correlation regimes are independent of basis terciles after controlling for rate differentials.

Horizon: SLOW_PRIOR

Availability: PAID_REALTIME

Priority: B

## W72X-E50 — Fed Swap-Line Take-Up Binary Stress State

Primary source: W72X-D18 (Fed standing swap lines with ECB, BoJ, BoE, BoC, SNB at OIS+25 bp per the 15 March 2020 coordinated action; weekly usage line in H.4.1 not verified)

Mechanism: Nonzero and rising swap-line usage indicates offshore USD scarcity; as a binary regime it conditions all dollar-sensitive intraday signals.

Features: swap_line_outstanding (H.4.1 central bank liquidity swaps), delta week over week; flag when above threshold.

Target: Regime gate for NQ/FX/gold correlation structure.

Falsify-if: Falsify if outstanding amounts are zero for >95% of sample so the flag is non-informative, or when nonzero but with no cross-asset effect. H.4.1 line item PROVENANCE_PENDING.

Horizon: WEEKLY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W72X-E51 — Turnover-Weighted Dollar Basket vs DXY Divergence

Primary source: W72X-D11 (BIS Triennial April 2025: USD one side of 89.2% of trades; EUR 28.9%, JPY 16.8%, GBP 10.2%, CNY 8.5%, CHF 6.4%; preliminary Sept 2025 release)

Mechanism: A trade-weighted proxy built from turnover shares differs from fixed-weight indexes; when the two diverge, the standard dollar index mis-measures FX risk relevant to cross-asset flows.

Features: basket_turnover = sum_w share_i x ret_i vs DXY ret (weights from the DXY methodology, which must be separately verified); rolling difference.

Target: NQ beta to dollar by basket; selecting the better proxy.

Falsify-if: Falsify if NQ beta to either basket is indistinguishable (difference in R2 < 0.01 OOS).

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B

## W72X-E52 — TFF Tuesday-to-Friday Stale-Gap Nowcast for FX Futures

Primary source: W72X-D13 (CFTC COT released 3:30 p.m. ET usually Friday with data from the prior Tuesday; PRE API dataset gpe5-46if TFF Futures Only with dealer/asset_mgr/lev_money fields)

Mechanism: Positions are three days old at publication; the price path between Tuesday close and Friday release carries information on how positions likely changed, enabling a nowcast that is the actionable object for Monday trading.

Features: lev_money_net(Tue) + beta x return(Tue->Fri) in currency; regression on subsequent weekly change; extends W62C-E04 with FX-specific nowcast.

Target: Next-week change in leveraged-fund net positions and the following week's currency return.

Falsify-if: Falsify if nowcast error variance equals the naive last-observation variance; negative control: using non-FX contracts.

Horizon: WEEKLY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W72X-E53 — Leveraged-vs-Asset-Manager FX Divergence as Risk-Sentiment Prior

Primary source: W72X-D13 (TFF categories: Dealer, Asset Manager, Leveraged Money, Other Reportables, Non-Reportables) ; adjacent W62C-E01/E02 are cross-asset; this edge is FX-specific

Mechanism: Opposite-signed net positions of asset managers and leveraged funds in JPY/CHF/EUR futures reflect carry vs hedging vs trend; divergence amplitude conditions USD/JPY response to US yields and NQ drawdowns.

Features: div_t = z(lev_net) - z(am_net) per currency; percentile; interaction with JPY.

Target: Probability of USD/JPY down-gaps conditional on NQ drawdown days.

Falsify-if: Falsify if div_t has no incremental explanatory power for USD/JPY or NQ conditional beta beyond W62C-E01 crowding.

Horizon: WEEKLY

Availability: PUBLIC_SCHEDULED

Priority: B

## W72X-E54 — FX Futures OI Share vs BIS Spot Share

Primary source: W72X-D11, D13 (BIS turnover shares; CFTC open interest by currency)

Mechanism: A futures participation ratio (FX futures OI relative to BIS turnover by currency) indicates how much of a currency's positioning is visible in COT; low ratio means COT is a weak proxy for that currency.

Features: ratio_i = futures_OI_i / BIS_turnover_i; rank; COT-signal reliability weights.

Target: Weights for combining COT currency signals.

Falsify-if: Falsify if ratio-weighted COT composite is no better than equal-weighted OOS.

Horizon: SLOW_PRIOR

Availability: PUBLIC_DELAYED

Priority: B

## W72X-E55 — COT Release Clock and Holiday-Delay Leak Guard

Primary source: W72X-D13 (CFTC: releases 3:30 p.m. ET, usually Friday, prior-Tuesday data; 2026 schedule marks delayed releases, e.g. 22 Jun, 6 Jul, 16 and 30 Nov, 28 Dec)

Mechanism: A backtest that assumes Friday availability on holiday-delayed weeks leaks 1-3 days; the guard reads the posted calendar for published_time.

Features: published_time from CFTC release schedule; unit test of feature availability.

Target: Pass/fail leak check for all COT-based features.

Falsify-if: Falsify only if CFTC changes the release convention; any strategy using Friday dates in delayed weeks fails.

Horizon: WEEKLY

Availability: PUBLIC_SCHEDULED

Priority: A-

## W72X-E56 — Fix-Window FX-to-NQ Contagion Placebo Test

Primary source: W72X-D01, D15 (dollar demand waves at fixes) 

Mechanism: If dollar demand at fixes were a pure FX-microstructure artifact, NQ should not respond; if it reflects broader balance-sheet and hedging flow, NQ and rates co-move. This is a placebo-controlled cross-asset test.

Features: NQ 1-min return and volume in fix windows vs placebo windows of equal length; USD basket pre-fix drift as regressor.

Target: Cross-asset coupling at fixes.

Falsify-if: Falsify if NQ coupling in fix windows equals coupling in placebo windows (CI includes 0); such a null is a successful outcome that prevents unneeded fix gating of NQ.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W72X-E57 — USD/JPY Asia-Fix to NQ Overnight Lead Filter

Primary source: W72X-D16 (Ito and Yamada: Tokyo fix spike reverses) + W72X-D15

Mechanism: NQ overnight moves that coincide with the 00:55 UTC USD/JPY spike should be treated as lower-quality entries because the FX driver mean-reverts; moves in NQ not associated with the spike are unaffected.

Features: NQ 5-min return sign at 00:55 UTC, USDJPY spike size, reversal; entry-quality score.

Target: Entry-confirmation filter for overnight NQ trades.

Falsify-if: Falsify if NQ entries taken during spike windows have equal 30-minute expectancy to others after fees and costs under the intermediate-outcome promotion gate.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W72X-E58 — Fix-Referenced Order Cancellation Signature (WMR Window Edge Cancel Burst)

Primary source: W72X-D01, D14 (WMR time-sliced capture and median; Evans: dealers' pre-fix trading and fix windows)

Mechanism: Time-sliced capture creates edge effects at slice boundaries; cancellation and re-quote bursts at slice edges are detectable in EBS/CME books and indicate window participants.

Features: Cancel-to-trade ratio per second around the fix; autocorrelation at slice period (unknown; estimated).

Target: Slice period estimate and burst intensity.

Falsify-if: Falsify if per-second cancel counts show no periodicity around the fix beyond baseline.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: B

## W72X-E59 — FX Global Code Principle 17 Version Gate

Primary source: W72X-D09 (GFXC: December 2017 revision of Principle 17 on information from the client's trade request during last look; 2021 last look guidance; Code three-year review kept text)

Mechanism: Rule versions change LP behaviour (e.g. cover and deal trading in the window); versioning historic FX execution data by Code version avoids pooling across regimes.

Features: version_id per date (2017-12-19 revision, 2021 guidance); reject-rate and markout distributions by version.

Target: Stability of LP markouts across code versions.

Falsify-if: Falsify if markout and reject distributions show no break across version dates.

Horizon: SLOW_PRIOR

Availability: PUBLIC_WEB_ONLY

Priority: B

## W72X-E60 — Month-End Rebalance Clock Fusion (FX Fix x Equity MOC)

Primary source: W72X-D14, D17 + equity rebalance mechanics owned by W26R

Mechanism: Month-end creates two flow waves: the 16:00 London FX fix (11:00/12:00 ET) and US equity-close rebalances; whether the first predicts the second sign is the fused object.

Features: FX month-end pre-fix USD move sign; MOC imbalance proxy; NQ last-30-min return; adjacency W26R.

Target: NQ last-30-min direction on month-end days given FX fix pressure.

Falsify-if: Falsify if the FX state adds no explanatory power beyond known rebalance-flow predictors in W26R.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W72X-E61 — Fix-Window Participation Concentration Using CME FX Futures vs EBS

Primary source: W72X-D06, D10 (CME FX futures liquidity rivals large ECNs per CME; EBS primary market)

Mechanism: Share of fix-window volume in futures vs EBS spot indicates where fix hedging is routed; a shift toward futures raises the usefulness of 6E/6J futures prints as fix-flow proxies.

Features: 6E 1s volume / (EBS volume if licensed); ratio over the fix window.

Target: Which venue leads price discovery at the fix.

Falsify-if: Falsify if futures leads in fewer than 40% of windows and lead-lag is unstable.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: B

## Final architecture edge (Truth Ladder)

The Truth Ladder for W72X: (1) rule or methodology fact from the benchmark administrator, exchange or regulator, versioned with effective date; (2) verified clock state (DST-resolved fix, settlement and option-cut instants, with published_time vs event_time separated); (3) intermediate microstructure outcomes (pre-fix drift sign, reversal coefficient, spread and depth half-life, reject/hold-time statistics); (4) execution-quality outcomes net of the W78B cost ledger; (5) only then any return-linked claim. A candidate may act only as a risk gate, entry filter or execution parameter until stage 4 evidence exists, and every FX-conditional rule must beat a placebo-clock control before it touches NQ/ES/rates/gold decisions.

## Highest-priority W72X tests

1. W72X-E01 Multi-Fix Clock-Proximity State Vector
2. W72X-E02 DST-Mismatch Fix Displacement Window
3. W72X-E04 Conditional Window-to-Window Reversal Coefficient
4. W72X-E07 Equity-MTD Hedge-Pressure Predictor for the Month-End Fix
5. W72X-E12 Tokyo 9:55 JST Spike-and-Revert Signature in USD/JPY
6. W72X-E23 10:00 New York Option-Cut Pinning Distance
7. W72X-E38 EBS Top-of-Book Post-Event Spread Normalization Half-Life
8. W72X-E41 FX Link Futures-vs-Spot Spread Deviation From Carry
9. W72X-E48 Basis-Repo Co-Spike Joint State
10. W72X-E57 USD/JPY Asia-Fix to NQ Overnight Lead Filter
