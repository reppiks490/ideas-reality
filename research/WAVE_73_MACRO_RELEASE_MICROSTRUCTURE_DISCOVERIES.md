# Wave 73E — Scheduled Macro Release Microstructure

Namespace: **W73E**

Thesis: scheduled macro releases and central-bank decisions are the most predictable liquidity and volatility shocks in an intraday multi-asset system. Release clocks are public in advance (BLS, BEA, Census, FOMC, ECB, BoE, BoJ calendars), the lock-up channel was closed in 2020, and the first public instant is a web posting. The edge is not predicting direction from the headline; it is modelling the clock, the surprise construction, the liquidity withdrawal and recovery, the volatility half-life, and cross-asset transmission as regime, risk-gate, execution-quality and entry-confirmation state.

Boundary: W75A owns FOMC text analysis (W75A-E16 token-diff, E17 statement-to-press-conference divergence, E18 minutes revealed-preference gap, E19 FOMC calendar-anchored intraday gate); W73E uses only price, clock, liquidity and surprise features and extends E19 with a price-based phase decomposition. W70B owns Globex book mechanics, W77 volatility products, W78B execution-quality ledgers, W55 Treasury financing events, W62 positioning. Where W73E overlaps, the increment is stated in the edge.

All candidates are research hypotheses only. Claude owns later implementation.

## W73E-E01 — Release-Clock Proximity Risk Gate

Primary source: BLS release calendar https://www.bls.gov/schedule/news_release/ (all times ET, 8:30 releases listed); BEA schedule https://www.bea.gov/news/schedule; Census economic indicators calendar

Mechanism: Scheduled tier-1 releases create a known-time volatility and liquidity-withdrawal event. A risk gate keyed to the calendar clock needs no model of the surprise itself.

Features: tau_next = seconds to next tier-1 release; tau_prev = seconds since last; tier weight w_k from E02; gate_state in {CLEAR, PRE_RELEASE, RELEASE_WINDOW, DECAY}. Parameters: pre-window length P, window length W (calibrate).

Target: Realized 1-min variance and quoted-spread multiple of NQ/ES/ZN/GC/6E in [-P,+W] relative to matched baseline.

Falsify-if: Gate does not reduce 95th-percentile slippage vs a no-gate baseline in out-of-sample, or placebo clocks (same weekday, same minute, no release) show the same variance lift.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: S

## W73E-E02 — Release Tier Impact Matrix (Slow Prior)

Primary source: Same calendars as E01 plus own futures tick archive (CME data; see W70B for book fields)

Mechanism: Release importance is asset-specific and drifts with the policy regime; a rolling matrix of absolute first-5-minute move per release type per asset converts a calendar into weights.

Features: M[k,a] = median |r_{0..+5m}| of asset a for release k over trailing N occurrences, scaled by trailing non-event 5-min median; rank stability across windows.

Target: Forecast of next-occurrence |r| (rank correlation) and of gate width.

Falsify-if: Spearman rank correlation of M between consecutive N-occurrence windows is not above a shuffled-label null, or M-weighted gate does no better than equal weights.

Horizon: SLOW_PRIOR

Availability: PUBLIC_SCHEDULED

Priority: A+

## W73E-E03 — Same-Timestamp Release Collision Count

Primary source: BLS calendar (Oct 2026 shows 8:30 CPI and Real Earnings same day); BEA schedule (Oct 29 2026 lists GDP advance and personal income and outlays on same date); Census calendar

Mechanism: Releases sharing a timestamp or day split attribution of the first move and can produce component whipsaw; independent additive effects are not guaranteed.

Features: n_same_ts, n_same_day_8:30, joint tier-weight sum; interaction term between the two largest surprise z-scores.

Target: |r_{0..+5m}| and whipsaw count (sign flips of 1-second returns in first 120s).

Falsify-if: Interaction coefficient is not distinguishable from zero under purged walk-forward, i.e. additive model fits equally well.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: A

## W73E-E04 — Schedule-Integrity and Shutdown Regime Flag

Primary source: BLS CPI shutdown impact page https://www.bls.gov/cpi/additional-resources/2025-federal-government-shutdown-impact-cpi.htm (reported via search snippet: October 2025 CPI not published, September CPI slipped from Oct 15 to Oct 24, October Employment Situation not released); BLS calendar states it is updated as needed, usually at least a week before release

Mechanism: A calendar is not a promise. Lapse-in-appropriations or rescheduling states remove or move scheduled events, so a model that assumes an event may take stale risk-off or risk-on positions.

Features: calendar_age_days of the entry, reschedule_count in last 90 days, appropriations-lapse flag (from Congress/OMB notices; source separate), last_published_vs_expected lag.

Target: Event-occurrence indicator and realized variance on the originally scheduled date.

Falsify-if: Variance lift on a cancelled or moved date persists at the original time (market still expects data), i.e. regime flag adds no information over the live calendar.

Horizon: SLOW_PRIOR

Availability: PUBLIC_EVENT_DRIVEN

Priority: A+

## W73E-E05 — Calendar Vintage Snapshot Integrity

Primary source: BLS iCal feed named on the BLS schedule page; BEA schedule offers ICS and JSON formats per the page; Census calendar

Mechanism: Backtests that read today's calendar leak reschedules. Snapshotting daily creates a point-in-time calendar and reveals how often announced dates change.

Features: vintage_hash, dates_changed_since_prior_snapshot, lead time of change.

Target: Fraction of historical events whose date in the T-7d snapshot differs from realized date.

Falsify-if: Zero changes observed over a full year (flag is dead weight) or feature leakage test finds gate performance identical with current-calendar and snapshot-calendar.

Horizon: SLOW_PRIOR

Availability: PUBLIC_SCHEDULED

Priority: B+

## W73E-E06 — Post-Lockup Public Dissemination Latency Race

Primary source: Federal Register notice 2020-11297 https://www.govinfo.gov/content/pkg/FR-2020-05-27/html/2020-11297.htm (DOL media lock-up permanently discontinued effective June 3, 2020; BEA and Census also end embargoed lock-ups; data available to public at 8:30 AM ET)

Mechanism: Since 2020 the first public instant is a web posting; the market reacts through first parsers. Latency from official time to our parsed value versus first futures tick is a measurable structural quantity, not directional alpha.

Features: delta_parse = t_parsed - 08:30:00.000 ET; delta_tick = t_first_ES_move_gt_k_ticks - 08:30:00.000 ET; distribution by release and source (HTML, PDF, API).

Target: Fraction of releases where our parsed value arrives before the first ES/ZN displacement beyond k ticks.

Falsify-if: Parsed value arrives after the first displacement in more than a stated fraction of releases (then value is confirmation-only, not entry).

Horizon: INTRADAY

Availability: PUBLIC_REALTIME

Priority: A+

## W73E-E07 — Lockup-Removal Pre-Release Informed Flow Regime Break

Primary source: Bernile, Hu, Tang, Can information be locked up? Journal of Financial Economics 2016, 121(3), 496-520 (abstract verified via search; reports no informed trading before NFP, PPI, GDP during lockups, but informed E-mini trading before FOMC); Federal Register 2020-11297

Mechanism: If informed pre-release trading existed around lockups, ending lockups in 2020 should change its footprint. A natural experiment for slow prior on whether pre-release signed flow is informative.

Features: Signed E-mini order flow in [-5m,0] before 8:30 release interacted with post-2020 dummy; surprise sign.

Target: Corr(signed pre-flow, surprise z) pre vs post June 3 2020.

Falsify-if: Post-2020 correlation exceeds zero by a margin that survives multiple-testing control, which would contradict the no-informed-trading reading; or equals pre-2020, making the lockup irrelevant.

Horizon: SLOW_PRIOR

Availability: RETROSPECTIVE_ONLY

Priority: B+

## W73E-E08 — Pre-Release Depth Withdrawal Execution Gate

Primary source: CME MDP 3.0 top-of-book depth (see W70B); release calendars E01

Mechanism: Liquidity providers pull quotes before known events to avoid adverse selection; observable depth thinning is a live state for execution quality.

Features: depth_ratio = (bid+ask size at touch, 10s before release) / (median same minute-of-day size, trailing non-event days); spread_ratio.

Target: Slippage of a marketable 1-lot in [0,+5s] and fill quality of passive entries.

Falsify-if: depth_ratio fails to predict first-5s slippage better than clock-time alone.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W73E-E09 — Embargo-Lift Spread and Depth Recovery Curve

Primary source: Balduzzi, Elton, Green, JFQA 36(4) 2001 (abstract verified: price adjustment generally within one minute; bid-ask spreads widen at announcement and revert in 5-15 minutes in Treasury interdealer data)

Mechanism: After the release, spreads normalize on a characteristic timescale that bounds the earliest non-penalized passive entry. The timescale is asset and tier specific and must be re-estimated on futures data.

Features: t_spread_half = time for spread to fall to halfway between peak and baseline; t_depth_80 = time to 80 percent of baseline depth.

Target: Passive entry fill rate and adverse selection by entry delay d after release.

Falsify-if: Entry delay d* from the curve does not improve net P&L per fill vs. immediate or fixed 15-minute delay on held-out events.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W73E-E10 — Post-Release Volatility Half-Life by Tier

Primary source: Andersen and Bollerslev, Journal of Finance 53(1) 1998 (announcements and intraday patterns explain much intraday volatility; abstract verified); own 1-second futures data

Mechanism: Volatility after a release decays with approximate exponential or power-law form. Fitted half-life converts the state DECAY into a numeric time-in-state for position sizing.

Features: fit sigma_t = base + A*exp(-t/h) (or power law) per event; h as function of surprise |z|, tier, time-of-day.

Target: Out-of-sample residual of predicted 1-min variance for t in [+2m,+60m].

Falsify-if: Power-law fit beats exponential on every tier (then h undefined) or h does not scale with |z|.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: S

## W73E-E11 — Consensus Surprise Z-Score Standardization

Primary source: Balduzzi-Elton-Green 2001 and Andersen-Bollerslev-Diebold-Vega, American Economic Review 93(1) 2003 (abstract verified: announcement surprises produce conditional mean jumps in FX); consensus from licensed vendor (Bloomberg, Reuters, Econoday, FactSet) - PROVENANCE_PENDING for exact feed

Mechanism: Raw surprise (actual minus consensus) is not comparable across releases; scaling by historical surprise standard deviation puts them on one scale.

Features: z = (A - C) / sigma_k, sigma_k = trailing std of (A - C) for release k, excluding current event.

Target: Signed first-minute return per asset.

Falsify-if: Slope of r on z is not distinguishable from zero for the headline series of NFP and CPI under walk-forward.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: S-

## W73E-E12 — Consensus Timestamp Vintage Pairing

Primary source: RESEARCH_PROTOCOL.md section 3 (vintage-first); vendor consensus snapshots PROVENANCE_PENDING

Mechanism: Consensus changes up to the release; the value used must be the last snapshot with published_time less than decision_time. Using the final post-hoc consensus leaks nothing but using a revised actual leaks.

Features: consensus_snapshot_time, actual_first_print_value (never revised value), age_of_consensus_minutes.

Target: Backtest P&L under first-print vs revised-actual.

Falsify-if: P&L difference between first-print and revised-actual is not distinguishable from zero (then vintage care is unnecessary for that series).

Horizon: SLOW_PRIOR

Availability: LICENSED_REALTIME

Priority: A

## W73E-E13 — CPI Headline-Core Component Split Surprise

Primary source: BLS calendar lists CPI and Real Earnings as 8:30 ET releases; component consensus from vendor PROVENANCE_PENDING

Mechanism: Rate-sensitive assets key on the component that moves the expected policy path, usually core, so headline surprise can mislead when core diverges.

Features: z_head, z_core, z_diff = z_head - z_core; rate-reaction sign agreement indicator.

Target: Signed 2-minute return in ZN/ZT versus z_core and z_head in a joint regression.

Falsify-if: z_head subsumes z_core in the joint regression (coefficient of z_core insignificant) over a rolling sample.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: A+

## W73E-E14 — Payroll Triple Surprise (Jobs, Wages, Unemployment)

Primary source: BLS Employment Situation 8:30 ET (Oct 2 2026 listed for September data)

Mechanism: NFP bundles three headline numbers; the market reaction depends on which dominates the policy-relevant signal, and it varies by regime.

Features: z_jobs, z_wage, z_unemp, composite c = argmax-weighted by rolling beta estimated on prior N events.

Target: First-minute ZN and ES returns; whipsaw count; 5m vs 1m sign agreement.

Falsify-if: Rolling-beta weighted composite does not out-forecast the headline jobs z-score alone.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: A

## W73E-E15 — Good-News-Bad-News Equity Sign Regime

Primary source: Andersen-Bollerslev-Diebold-Vega 2003 (documents state dependence of news effects; verified at abstract level) and Fed policy state from FOMC calendar https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm

Mechanism: Equity reaction to growth surprises can be positive or negative depending on whether the market is focused on growth or discount rate. The sign is a regime state.

Features: regime s = sign of trailing 60-day correlation between daily ES return and daily ZN return (or 10y yield change); interact with z.

Target: Sign of ES response in [0,+5m] to growth surprise z.

Falsify-if: Interaction coefficient on s is not significant, or sign map flips unpredictably out-of-sample.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: S

## W73E-E16 — Bad-News Asymmetry Multiplier

Primary source: Andersen-Bollerslev-Diebold-Vega 2003 (abstract verified: bad news has greater impact than good news in FX)

Mechanism: If asymmetry persists in index futures, downside surprises deserve a higher reaction weight and wider stops than upside surprises of the same magnitude.

Features: asym = beta(z<0) / beta(z>0) for each asset, estimated on rolling events; define bad news relative to the asset's risk-off direction.

Target: Ratio of absolute first-5-minute move for |z|>k by sign.

Falsify-if: asym confidence interval includes 1 in out-of-sample.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: B+

## W73E-E17 — Consensus Dispersion Uncertainty Scaler

Primary source: Vendor survey min/max/std (Bloomberg, Reuters) PROVENANCE_PENDING; no feed verified

Mechanism: Wide forecaster disagreement signals higher ex-ante uncertainty; the reaction per unit surprise or the unconditional move size may rise.

Features: disp = (high - low) / sigma_k or stdev of survey; interaction with |z|.

Target: |r_{0..+5m}| and realized variance post-release.

Falsify-if: disp adds no predictive power over |z| and tier alone.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: B+

## W73E-E18 — Prior-Month Revision Surprise Factor

Primary source: BLS Employment Situation (revisions to prior two months are published with each release; confirm in release text - PROVENANCE_PENDING); BEA GDP second and third estimates https://www.bea.gov/news/schedule

Mechanism: Revisions carry separate information and may be absorbed with delay because headline dominates attention.

Features: rev_net = revision to prior two months sum; z_rev scaled.

Target: Return in [+1m,+15m] versus [0,+1m], and 1-day drift.

Falsify-if: Revision z explains no incremental return after controlling for headline z.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: B+

## W73E-E19 — GDP Vintage Staircase Placebo

Primary source: BEA schedule: Q3 2026 advance Oct 29, second Nov 25, third Dec 23 (verified on page)

Mechanism: Advance estimate is the first information; second and third are revisions. Reaction should concentrate in the advance estimate; second and third estimates act as negative controls.

Features: estimate_type; z_adv, z_rev2, z_rev3.

Target: |r_{0..+5m}| at 8:30 for each type.

Falsify-if: Second or third estimate triggers a comparable move to advance (rejecting information-timing story).

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B

## W73E-E20 — Market-Implied Expectation versus Survey Consensus Gap

Primary source: CME fed funds and Treasury futures (feed PROVENANCE_PENDING for fields); pre-release 30 minute price drift

Mechanism: Futures drift before a release may already embed information the survey lacks, so surprise relative to market expectation differs from surprise relative to survey.

Features: drift_pre = r_{-30m..-1s} in ZT/ZN; implied_z = drift_pre / (beta_k * sigma_k); gap = z - implied_z.

Target: Post-release return vs gap versus vs z alone.

Falsify-if: gap has no incremental explanatory power over z.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W73E-E21 — Bond-Market Pre-Release Uncertainty Resolution

Primary source: Hu, Pan, Wang, Zhu, Premium for heightened uncertainty, Journal of Financial Economics 145(3) 2022, NBER w25817 (abstract verified; related finding that bond market resolves uncertainty earlier than equity per search summary)

Mechanism: If uncertainty resolves earlier in bonds than equities, pre-release ZN/ZT behavior should lead ES positioning into the event.

Features: ZN realized vol and drift in [-24h,0] relative to ES; lead-lag.

Target: ES pre-event return conditional on ZN pre-event vol state.

Falsify-if: No lead-lag; ZN state has no incremental information on ES pre-event returns.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W73E-E22 — Consensus Staleness Elapsed-Shock Index

Primary source: Survey collection dates (vendor) PROVENANCE_PENDING; crude oil, rates, FX moves from own tape

Mechanism: Surveys are frozen days before; shocks between collection and release change the true expectation and distort measured surprise.

Features: stale = abs(return of 2y yield / oil / DXY since survey close) normalized; corrected z = (A - (C + beta*shock)) / sigma_k.

Target: Out-of-sample R^2 of first-minute response.

Falsify-if: Staleness-adjusted z does not beat raw z.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W73E-E23 — First-Print Overreaction Reversal Ratio

Primary source: Own 1-second data around 8:30 releases; ABDV 2003 and Balduzzi-Elton-Green 2001 for timing of adjustment

Mechanism: If the initial move overshoots, the sign of return in [+1m,+15m] opposes [0,+1m] for large |z| and wide spreads. Sign ambiguity: continuation is equally plausible and must be tested two-sided.

Features: R = r_{+1m..+15m} / r_{0..+1m}; conditioning on |z|, spread_ratio, depth_ratio.

Target: Mean R by conditioning bucket.

Falsify-if: R not significantly different from zero in either direction after cost.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S

## W73E-E24 — Bond-First Equity-Second Lead-Lag

Primary source: Balduzzi-Elton-Green 2001 (one-minute adjustment in Treasuries); own ZN and ES ticks

Mechanism: A rate-sensitive release moves ZN first and ES follows by seconds to minutes in some regimes; the lag profile is exploitable only if above latency and cost.

Features: Cross-correlation of 1s returns ZN vs ES in [0,+120s]; peak lag tau*; sign by regime from E15.

Target: ES return in [tau*, +5m] conditional on ZN impulse in [0,tau*].

Falsify-if: Peak lag below measured round-trip latency, or no incremental ES predictability after cost.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S

## W73E-E25 — Gold and Dollar Real-Yield Transmission State

Primary source: Own GC, 6E ticks and ZT/ZN; Federal Reserve statement and BLS data clocks

Mechanism: Gold responds to real-yield and dollar surprises; transmission strength is state dependent.

Features: beta_GC_on_ZN, beta_6E_on_ZN trailing; z-scored; realized in [0,+10m].

Target: GC response magnitude and sign given ZN impulse.

Falsify-if: Trailing beta no better than constant beta out-of-sample.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W73E-E26 — Crypto Beta Switch at Macro Releases

Primary source: BTC perp/spot tape (venue PROVENANCE_PENDING), NQ ticks

Mechanism: Crypto trades 24/7 so it absorbs release shocks without a halt; its beta to NQ around releases may differ from baseline.

Features: beta_BTC_NQ in [0,+5m] versus [-60m,-5m]; sign of BTC reaction when ZN impulse large.

Target: Out-of-sample ability of beta_event to forecast BTC move given NQ impulse.

Falsify-if: Event beta equals baseline beta (no regime).

Horizon: INTRADAY

Availability: PUBLIC_REALTIME

Priority: B+

## W73E-E27 — Component Whipsaw Count in First Two Minutes

Primary source: Release documents publish headline and components simultaneously (BLS 8:30 ET); own 1-second data

Mechanism: When headline and components disagree, price may jump then reverse as the market parses; whipsaw count measures this ambiguity and signals an unreliable first move.

Features: wsc = number of sign changes of 5-second returns in [0,+120s]; sign agreement between z_head and z_core.

Target: Reversal ratio R from E23 and 5-minute follow-through.

Falsify-if: wsc does not predict R or follow-through.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W73E-E28 — Event-Time Clock Alignment (Seconds-Since-Release)

Primary source: Own tape; release timestamps from calendar E05

Mechanism: Aligning to event time instead of wall time prevents smearing of the microstructure response by clock jitter and parse delay.

Features: event_time = t - T_release; normalizing volume by cumulative volume clock; align on exchange timestamps.

Target: Cross-event stability of average responses.

Falsify-if: Wall-clock alignment gives equal or lower between-event signal-to-noise.

Horizon: SLOW_PRIOR

Availability: PAID_REALTIME

Priority: B

## W73E-E29 — Depth Recovery Time to 80 Percent

Primary source: Own book data (see W70B); release clocks

Mechanism: Time until depth returns to 80 percent of baseline defines when liquidity-taking is cheap again.

Features: t_depth_80 per release; function of |z|, tier, time-of-day.

Target: Fill slippage as function of time after release.

Falsify-if: t_depth_80 does not vary with |z|; fixed delay equals adaptive.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W73E-E30 — Large-Surprise Drift Continuation Window

Primary source: Own tape; consensus z (E11)

Mechanism: After spread normalization, large surprises may continue to drift 5-60 minutes as slower participants adjust; opposite sign possible via mean reversion.

Features: drift = r_{+15m..+60m}; condition on |z| > k and spread normalized by t_spread_half.

Target: Mean drift by bucket, two-sided.

Falsify-if: No statistically distinguishable drift after cost and multiple-testing control.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: A-

## W73E-E31 — FOMC Three-Phase Intraday Clock

Primary source: Federal Reserve statement page https://www.federalreserve.gov/newsevents/pressreleases/monetary20250917a.htm (verified: statement for release at 2:00 p.m. EDT); press-conference start time UNVERIFIED (commonly 2:30 p.m. ET) PROVENANCE_PENDING; FOMC calendar https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm

Mechanism: FOMC day has distinct phases: pre-statement, statement digestion, press conference; variance and liquidity differ by phase. Extends W75A-E19 (FOMC Calendar-Anchored Intraday Gate) by adding a price-based phase decomposition.

Features: Phase variance shares V_pre, V_stmt, V_press; phase-specific spread ratios.

Target: Variance partition of FOMC-day range across phases.

Falsify-if: Phase shares equal those of ordinary days at the same times.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: S

## W73E-E32 — Statement-to-Press-Conference Price Reversal

Primary source: Fed statement 2:00 p.m. EDT (verified); press conference time PROVENANCE_PENDING; boundary: W75A-E17 owns text divergence, this edge uses only price

Mechanism: Statement reaction is often repriced when the Chair speaks. Price-only version: sign of the 2:00-2:05 return versus 2:30-3:30 return, conditioned on SEP meeting.

Features: R_fomc = r_{press_window} / r_{stmt_window}; SEP flag from calendar.

Target: Mean R by SEP and by dissent flags (flag source separate).

Falsify-if: R not different from zero and not different between SEP and non-SEP meetings.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S

## W73E-E33 — SEP Meeting Amplification Flag

Primary source: FOMC calendars page (2026: March, June, September, December meetings have SEP; verified)

Mechanism: Meetings with projections have additional information (dot plot and projections) and may produce larger or longer reactions.

Features: sep_flag; abs 2:00-2:30 return; half-life h from E10.

Target: Effect of sep_flag on variance and h.

Falsify-if: No difference after controlling for surprise size.

Horizon: SLOW_PRIOR

Availability: PUBLIC_SCHEDULED

Priority: A

## W73E-E34 — FOMC Blackout Window Quietness and Exit

Primary source: Federal Reserve FOMC external communications policy (participants and staff PDFs found at https://www.federalreserve.gov/monetarypolicy/files/FOMC_ExtCommunicationParticipants.pdf; blackout begins 12:00 a.m. ET second Saturday before meeting and ends 11:59 p.m. ET day after meeting per search summary - verify exact text); St. Louis Fed blackout page https://www.stlouisfed.org/about-us/resources/blackout-periods

Mechanism: During blackout, policymaker commentary headlines are mostly absent, so a Fed-speaker risk gate can be disabled and rates variance should lack speaker shocks.

Features: blackout_flag; days_since_blackout_exit; count of speeches the next days.

Target: Rates (ZN/ZT) non-event variance inside vs outside blackout, controlling for data releases.

Falsify-if: Variance inside blackout is not lower after controlling for releases.

Horizon: SLOW_PRIOR

Availability: PUBLIC_SCHEDULED

Priority: A

## W73E-E35 — Post-Blackout Speaker Density Burst

Primary source: Fed calendar of events and speeches page PROVENANCE_PENDING (URL not fetched); blackout dates as above

Mechanism: After the blackout ends, speakers cluster; expected shocks per day increase.

Features: speaker_count_next_48h weighted by voter status (voter list source: FOMC membership page PROVENANCE_PENDING).

Target: ZN and ES 15-minute variance around speeches.

Falsify-if: Speaker density does not predict variance beyond calendar day effects.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W73E-E36 — FOMC Minutes Release Timing State

Primary source: FOMC calendars: 2026 minutes Feb 18, Apr 8, May 20, Jul 8, Aug 19, Oct 7 (verified); release time of day UNVERIFIED (historically 2:00 p.m. ET) PROVENANCE_PENDING; boundary: W75A-E18 owns text content

Mechanism: Minutes arrive three weeks after decision at a known date; reaction magnitude relative to pre-decision uncertainty is a timing-only feature independent of text.

Features: minutes_flag; days-since-decision; ex-ante rate vol percentile.

Target: |r_{0..+15m}| ZN, ES at minutes versus matched control days.

Falsify-if: Minutes-day variance not higher than matched controls.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W73E-E37 — Pre-FOMC Drift Conditional Revival Test

Primary source: Lucca and Moench, Journal of Finance 70(1) 2015 (NY Fed SR512 https://www.newyorkfed.org/medialibrary/media/research/staff_reports/sr512.pdf; abstract verified); Kurov, Wolfe, Gilbert, Finance Research Letters 40, 2021 (drift essentially disappeared after 2015); Hu et al. 2022 uncertainty explanation

Mechanism: Drift linked to uncertainty premium; if uncertainty returns (high VIX or dispersion), the drift may reappear conditionally. Unconditional drift is already falsified per Kurov et al.

Features: ES return from T_decision - 24h to -2m; VIX or MOVE percentile (W77 for vol products); meeting flag.

Target: Conditional mean of pre-FOMC ES return by uncertainty tercile.

Falsify-if: Conditional mean is zero in the high-uncertainty tercile post-2015.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A-

## W73E-E38 — Pre-FOMC Signed-Flow Footprint

Primary source: Bernile, Hu, Tang JFE 2016 (abstract verified: trading consistent with informed activity in E-mini before FOMC announcements); own E-mini trade data

Mechanism: A footprint of informed signed order flow immediately before 2:00 p.m. is testable on modern data but ethical limits apply: no inference about identities.

Features: signed volume imbalance in [-30m,-1m] for ES; surprise sign from E39.

Target: Correlation of pre-flow with policy surprise sign.

Falsify-if: Correlation indistinguishable from zero after 2015 sample.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W73E-E39 — Futures-Implied Policy Surprise Around Statement

Primary source: CME fed funds / SOFR futures tick data (PROVENANCE_PENDING for contract specs and licensing); Fed statement time 2:00 p.m. EDT (verified)

Mechanism: Policy surprise is the change in near-term rate futures around the statement. It is the market-based analogue of consensus surprise and does not rely on surveys.

Features: ps = change in front implied rate over [13:55,14:05]; second factor: change in 2y-implied rate.

Target: ES, ZN, GC, 6E returns over [14:00,14:30].

Falsify-if: Rate-futures surprise adds no explanatory power over simple ZT return.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W73E-E40 — Day-Before Range Compression Positioning

Primary source: FOMC calendars (two-day meetings, e.g. Oct 27-28 2026); own daily/intraday ranges

Mechanism: Day one of a two-day meeting should be quiet; compressed ranges followed by large events may reflect positioning and sets up a vol-breakout prior.

Features: range_ratio = day1 range / 20-day median; day1 volume ratio.

Target: Next-day (decision day) range and 2:00-4:00 variance.

Falsify-if: Compression does not predict decision-day range.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W73E-E41 — Two-Day Meeting Day-One Placebo

Primary source: FOMC calendars (2026-2027 meeting dates verified)

Mechanism: Day one has no policy announcement; an event model that finds large day-one effects is mis-specified. Day one is the natural negative control.

Features: placebo_flag; same-clock windows 14:00-14:30 on day one.

Target: Estimated 'FOMC effect' on day one.

Falsify-if: Estimated effect on day one is as large as on announcement day.

Horizon: SLOW_PRIOR

Availability: PUBLIC_SCHEDULED

Priority: B+

## W73E-E42 — Scheduled Fed Speaker Weighted Exposure

Primary source: Fed event calendar PROVENANCE_PENDING; FOMC voter roster PROVENANCE_PENDING

Mechanism: Speakers differ in influence (Chair, Vice Chair, NY Fed president, voters). Exposure over the next two hours is a forward risk state.

Features: exposure_2h = sum of weights of scheduled speakers in next 120 minutes.

Target: ZN 15-minute realized variance.

Falsify-if: Weights uniform give equal fit; exposure adds nothing beyond calendar day.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W73E-E43 — ECB Decision Overlap With US Morning

Primary source: ECB meeting calendar https://www.ecb.europa.eu/press/calendars/mgcgc/html/index.en.html (2026: 28-29 Oct with press conference 29 Oct; 17 Dec; times of announcement not stated on page; commonly 14:15 and 14:45 CET) PROVENANCE_PENDING for times

Mechanism: ECB decisions fall in US pre-market (about 8:15 and 8:45 ET), interfering with 8:30 US releases and ES liquidity; an overlap flag identifies compound event windows.

Features: overlap flag if ECB decision within +/-60m of a US tier-1 release; timezone conversion with DST handled via IANA tz.

Target: |r| and spread in ES, 6E, ZN.

Falsify-if: Overlap windows do not show variance above sum of single-event windows.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: A

## W73E-E44 — Central-Bank Cluster Week Density

Primary source: FOMC 27-28 Oct 2026; ECB 28-29 Oct 2026 (press conference Oct 29); BoJ 29-30 Oct 2026 with Outlook Report Oct 30; BEA GDP advance and PCE Oct 29; BLS ECI Oct 30; BoE 5 Nov 2026 (all from fetched official pages)

Mechanism: Clustered events within 72 hours compress several shocks into one regime; cross-central-bank interactions (e.g., USDJPY) can magnify moves.

Features: n_cb_events_in_72h; n_tier1_releases_in_72h; cluster_flag.

Target: Weekly range and 3-day realized variance.

Falsify-if: Cluster-week variance not above sum of component weeks.

Horizon: WEEKLY

Availability: PUBLIC_SCHEDULED

Priority: A+

## W73E-E45 — BoJ Outlook Report Meeting Flag

Primary source: BoJ schedule https://www.boj.or.jp/en/mopo/mpmsche_minu/index.htm (2026 outlook reports Jan 23, Apr 28, Jul 31, Oct 30; summary of opinions and minutes lags; verified)

Mechanism: Outlook-report meetings carry forecasts and are more informative; JPY crosses and Asia-hours NQ may react more.

Features: outlook_flag; days to minutes release.

Target: 6J realized variance in Tokyo session and NQ overnight.

Falsify-if: No difference between outlook and non-outlook meetings.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W73E-E46 — BoJ Summary-of-Opinions and Minutes Placebo Events

Primary source: BoJ page: Summary of Opinions ~10 days post meeting and minutes weeks later, released at 8:50 (JST per page; verified)

Mechanism: Minutes and summaries are lagged information; reaction should be small; use as placebo to calibrate event-window detection.

Features: event type in {SUMMARY, MINUTES}; JST to ET conversion with DST.

Target: |r| 6J and NQ in [0,+15m].

Falsify-if: Reaction comparable to a policy decision day (invalidating placebo).

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B

## W73E-E47 — BoJ Unscheduled Time-of-Day Uncertainty in Thin Overnight Globex

Primary source: BoJ meeting date pairs verified; announcement time of day UNVERIFIED (PROVENANCE_PENDING)

Mechanism: If decision timing within the meeting day is irregular, the response lands in thin overnight US index futures; the risk is wide spreads.

Features: meeting_day flag; Globex depth percentile in Asia hours.

Target: NQ slippage during Tokyo-session meeting day.

Falsify-if: Slippage same as ordinary Asia-hour days.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W73E-E48 — BoE MPC MPR-Meeting Versus Non-MPR

Primary source: BoE MPC dates https://www.bankofengland.co.uk/monetary-policy/upcoming-mpc-dates (2026: Feb 5, Apr 30, Jul 30, Nov 5 with MPR; others without; minutes published with announcement; time of day not stated on page - PROVENANCE_PENDING)

Mechanism: MPR meetings add forecasts; sterling and gilts react more; spillover to US rates in the same morning.

Features: mpr_flag; 6B and ZN reaction around announcement.

Target: Return and variance in 6B, ZN.

Falsify-if: MPR flag effect absent.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W73E-E49 — Foreign Central Bank Surprise Spillover to ZN and ES

Primary source: ECB/BoE/BoJ calendars above; OIS curves for surprise (PROVENANCE_PENDING licensed)

Mechanism: A foreign-policy surprise moves global yields; US duration may absorb part of it.

Features: fcb_surprise = change in front-end OIS around decision; beta_ZN trailing.

Target: ZN and ES returns in [0,+30m].

Falsify-if: beta indistinguishable from zero.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: B+

## W73E-E50 — Daylight Saving Misalignment Window

Primary source: Standard DST rules for US (second Sunday of March to first Sunday of November) and EU (last Sunday of March to last Sunday of October); verify against IANA tz database PROVENANCE_PENDING

Mechanism: For roughly two to three weeks per year the ET-CET offset is five hours instead of six, shifting the overlap of ECB announcements with US releases.

Features: tz_offset_ET_CET; computed event overlap with E01.

Target: Event overlap and variance in affected weeks.

Falsify-if: No overlap difference found in affected weeks.

Horizon: SLOW_PRIOR

Availability: PUBLIC_SCHEDULED

Priority: B

## W73E-E51 — Holiday-Thinned Release Days

Primary source: BLS and BEA calendars (releases scheduled near US holidays); CME holiday calendar PROVENANCE_PENDING

Mechanism: Release on or around thin-liquidity sessions amplifies price impact per unit surprise.

Features: holiday_adjacent flag; volume ratio.

Target: Impact per unit z.

Falsify-if: Impact per unit z identical on holiday-adjacent days.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W73E-E52 — Day-of-Month Macro Heat Slow Prior

Primary source: BLS, BEA, Census calendars aggregated

Mechanism: The count of tier-1 releases per day of month and week is a slow prior for daily range and for preparing risk budgets.

Features: heat_d = sum of tier weights on date d.

Target: Daily true range of NQ/ES.

Falsify-if: heat_d has no cross-sectional association with daily range after day-of-week control.

Horizon: SLOW_PRIOR

Availability: PUBLIC_SCHEDULED

Priority: B+

## W73E-E53 — NFP-Week Positioning Cycle

Primary source: BLS Employment Situation calendar; own daily data

Mechanism: Range compression Tuesday to Thursday before a Friday payroll may be followed by expansion; the cycle is a rule-based prior for entry sizing.

Features: range_t / range_{t-1}, volume, option-implied move (PENDING).

Target: Friday 8:30 first-30m range.

Falsify-if: Compression has no relation to Friday expansion.

Horizon: WEEKLY

Availability: PUBLIC_SCHEDULED

Priority: B

## W73E-E54 — 8:30 Shock to 9:30 Cash-Open Gap Resolution

Primary source: BLS/BEA/Census 8:30 ET calendars and cash equity open 9:30 ET; boundary: W70B owns book mechanics

Mechanism: Overnight futures reprice at 8:30; the cash open at 9:30 introduces constituents and auctions that may partially retrace or confirm the move.

Features: r_{8:30..9:29}, r_{9:30..10:00}; open imbalance (W81E-E13).

Target: r_{9:30..10:00} sign vs r_{8:30..9:29}.

Falsify-if: Sign independence of the two windows.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W73E-E55 — Hawkes Branching Ratio After Release

Primary source: Own trade/quote tape

Mechanism: Self-excitation of trading intensity after releases summarizes how reflexive the aftermath is; a high branching ratio flags unstable liquidity.

Features: n_hat from Hawkes fit on order arrivals in [0,+15m].

Target: Next 15-minute realized variance.

Falsify-if: n_hat does not improve variance forecasts over simple volume.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W73E-E56 — Cross-Asset Sign Agreement Index

Primary source: Own multi-asset tape

Mechanism: If ES, ZN, GC, 6E, BTC first-minute signs agree with the surprise-implied sign, the shock is clean; disagreement signals mixed information.

Features: agree = fraction of assets with sign consistent with z mapping; weight by impact.

Target: Continuation vs reversal at +15m.

Falsify-if: agree provides no incremental information over |z|.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W73E-E57 — Macro Release State Vector (Truth Ladder)

Primary source: Composite of E01-E56

Mechanism: A conditioning layer: clock, tier, collision, surprise z, spread/depth ratios, half-life state, cross-asset agreement. Not a standalone signal.

Features: vector with parameters calibrated; versioned calendar.

Target: Gate quality: fewer tail slippage events.

Falsify-if: Gated system no better out-of-sample than ungated after cost.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: S

## Final architecture edge (Truth Ladder)

Truth Ladder: (1) verified public clock from point-in-time calendar snapshot; (2) liquidity state measured on the tape (depth, spread, half-life); (3) surprise z with first-print vintage; (4) cross-asset sign agreement; (5) intermediate outcome gate accuracy; (6) only then P&L. A higher rung may not be used to excuse a failed lower rung. The Macro Release State Vector is a conditioning layer.

## Highest-priority W73E tests

1. W73E-E10 Post-Release Volatility Half-Life by Tier
2. W73E-E23 First-Print Overreaction Reversal Ratio
3. W73E-E24 Bond-First Equity-Second Lead-Lag
4. W73E-E31 FOMC Three-Phase Intraday Clock
5. W73E-E32 Statement-to-Press-Conference Price Reversal
6. W73E-E15 Good-News-Bad-News Equity Sign Regime
7. W73E-E08 Pre-Release Depth Withdrawal Execution Gate
8. W73E-E09 Embargo-Lift Spread and Depth Recovery Curve
9. W73E-E44 Central-Bank Cluster Week Density
10. W73E-E39 Futures-Implied Policy Surprise Around Statement
