# Wave 76Q — Energy and Metals Intraday Structure

Namespace: **W76Q**

Thesis: energy and metals have unusually rigid public timing infrastructure: EIA releases at fixed minutes (10:30 ET Wed/Thu with holiday exceptions), exchange settlement is a short volume-weighted window (CL 14:28-14:30 ET, GC 13:29-13:30 ET, Brent 19:28-19:30 London), LBMA benchmark auctions at 10:30/15:00 (gold) and 12:00 (silver) London, and OPEC+ often decides on Sundays before the Globex reopen. The research target is the clock-conditioned state (window, DST alignment, expiry, roll) rather than directional views.

Boundary: W49P owns COMEX/LME inventory and delivery supply states, W56G owns global bullion physical flow, W62C owns CFTC positioning, W70B owns Globex microstructure generically, W77V owns volatility products, W78E execution quality, W83G weather. W76Q owns intraday timing, settlement-window, roll, spread-construction and benchmark-clock mechanics for energy and metals; where it touches an owned mechanic it cites the ID and states the increment.

All candidates are research hypotheses only. Claude owns later implementation. No profitability is claimed; every threshold is a parameter to be calibrated under the intermediate-outcome promotion gate.

## W76Q-E01 — WPSR 10:30 Release Reaction Envelope

Primary source: EIA WPSR schedule https://www.eia.gov/petroleum/supply/weekly/schedule.php (verified: Wed 10:30 ET standard; holiday weeks Thu 12:00 ET); CL spec for Globex hours

Mechanism: A single scheduled public release moves CL/RB/HO within seconds; the envelope (peak abs return, time-to-peak, reversal ratio) is a stable shape per release type but the sign depends on the surprise, not the release.

Features: r[t0-60s,t0+k] for k in {5,30,120,600}s; peak abs; reversal ratio = r[t0+600s]/peak; spread widening factor vs trailing-hour median.

Target: Sized abs response and reversal probability (not sign).

Falsify-if: Envelope parameters are indistinguishable from random same-time Tuesday/Thursday placebo windows (permutation p>0.1 over >=150 Wednesdays).

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED (timestamp) + PAID_REALTIME (CME tape)

Priority: S

## W76Q-E02 — Holiday-Shifted WPSR Release Regime

Primary source: EIA WPSR schedule https://www.eia.gov/petroleum/supply/weekly/schedule.php (verified: Wed 10:30 ET standard; holiday weeks Thu 12:00 ET) (table: Thu 12:00 ET alt-releases e.g. 15 Oct 2026 and 12 Nov 2026 per page; Christmas Mon 17:00; New Year Thu 11:00)

Mechanism: Shifted releases land in different liquidity states (Thursday noon overlaps NG storage week context, midday US lull; Monday 17:00 lands at/after cash close and just after Globex break).

Features: release_slot in {WED_1030, THU_1200, THU_1100, MON_1700}; slot-specific envelope from E01; slot sample counts.

Target: Slot-conditional response scale and fade rate.

Falsify-if: Slot-conditional envelope shrinks to pooled Wednesday envelope (hierarchical-model posterior mass on slot effect ~0).

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: A

## W76Q-E03 — EIA Schedule-Change Detector

Primary source: EIA WNGSR schedule https://ir.eia.gov/ngs/schedule.html (verified: Thu 10:30 ET standard; holiday exceptions listed); WPSR schedule page. The NG page marks entries '(Updated)' (e.g. 8 Jan 2025 National Day of Mourning, 29 Dec 2025), proving the schedule can change after publication.

Mechanism: Strategies assuming 10:30 on the standard weekday will mis-time risk gates when EIA amends the calendar; a scraped, versioned schedule with hash diff removes the failure.

Features: daily scrape hash of both schedule pages; diff event; days-to-next-nonstandard-release; Updated-flag count.

Target: Binary: expected_release_time is stale (gate flag).

Falsify-if: Over 12 months no amended entry occurs and hash never changes (then keep only as a monitor, downgrade to B).

Horizon: DAILY

Availability: PUBLIC_WEB_ONLY

Priority: A

## W76Q-E04 — Cushing-Stock Surprise to M1-M2 Spread Response

Primary source: EIA WPSR schedule https://www.eia.gov/petroleum/supply/weekly/schedule.php (verified: Wed 10:30 ET standard; holiday weeks Thu 12:00 ET); CL spec (verified: physical delivery F.O.B. at Cushing, Oklahoma pipelines/storage)

Mechanism: CL deliverable at Cushing, so a Cushing-specific inventory surprise should load on the front calendar spread more than on the flat price; flat-price move is contaminated by crude-wide and macro effects.

Features: z-surprise vs seasonal-AR expectation (own construction; analyst consensus is PP) for Cushing stocks; dSpread(M1-M2) over [t0, t0+10m] minus beta*dFlat.

Target: Spread-minus-flat residual sign and size.

Falsify-if: Residual spread response is not monotone in Cushing surprise decile (Spearman p>0.1, 3-year sample) or equals response to total-crude surprise.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED + PAID_REALTIME

Priority: A+

## W76Q-E05 — Headline-vs-Component Divergence at WPSR

Primary source: EIA WPSR schedule https://www.eia.gov/petroleum/supply/weekly/schedule.php (verified: Wed 10:30 ET standard; holiday weeks Thu 12:00 ET)

Mechanism: When crude stocks and product stocks (gasoline, distillate) surprise in opposite directions, the first print is driven by whichever the algos parse first; later components are priced in minutes.

Features: sign agreement index of crude, gasoline, distillate surprises; divergence flag; CL return t0+5s vs t0+120s.

Target: Probability that first-5s direction reverses by +10 min.

Falsify-if: Reversal rate in divergence cases equals agreement cases within sampling error.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: A

## W76Q-E06 — Refinery Utilization Surprise to Crack Spread Lead

Primary source: EIA WPSR schedule https://www.eia.gov/petroleum/supply/weekly/schedule.php (verified: Wed 10:30 ET standard; holiday weeks Thu 12:00 ET); EIA-800 refinery survey (forms listed via https://eia.gov/petroleum/supply/weekly/pdf/sources.pdf, search-verified)

Mechanism: Refinery runs transmit simultaneously to crude demand and product supply; the 3-2-1 crack (2 RB + 1 HO vs 3 CL) may move before CL outright.

Features: utilization change surprise; crack = (2*RB*42+HO*42-3*CL)/3 with unit care; lead-lag of crack vs CL within [t0,t0+300s].

Target: Which leg leads; crack residual drift.

Falsify-if: No lead of crack over CL in 1-second cross-correlation at t0+[0,300]s, placebo Tue/Thu.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED + PAID_REALTIME

Priority: B+

## W76Q-E07 — Blended-Estimate Series Revision-Risk Fade

Primary source: EIA WPSR schedule https://www.eia.gov/petroleum/supply/weekly/schedule.php (verified: Wed 10:30 ET standard; holiday weeks Thu 12:00 ET); sources.pdf notes certain series (Other Oils Stocks, Total Product Supplied) blend weekly survey data with the latest Petroleum Supply Monthly (search-verified)

Mechanism: Series partly derived from monthly data are mechanically revision-prone, so large first-print surprises in them carry less durable information than surveyed series (crude stocks).

Features: surprise in 'product supplied' vs surprise in surveyed stocks; ratio of absolute weekly-to-monthly revision (collector must store vintages).

Target: Fade ratio of response to derived-series surprises.

Falsify-if: Derived-series response persistence equals surveyed-series persistence (difference in 60-min cumulative return not significant).

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W76Q-E08 — Import-Export Weekly Noise to Brent-WTI Matched Spread

Primary source: EIA WPSR schedule https://www.eia.gov/petroleum/supply/weekly/schedule.php (verified: Wed 10:30 ET standard; holiday weeks Thu 12:00 ET); EIA-804 weekly imports report (search-verified). Exports are model estimates [PP].

Mechanism: Exports/imports surprises signal arbitrage openness between WTI and Brent; matched-month spread (see E26) should respond more than outright.

Features: net-import surprise; dS(WTI M - Brent M) over 10 min.

Target: Matched-spread change sign.

Falsify-if: No spread response beyond outright common factor (partial correlation ~0).

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B

## W76Q-E09 — Release-to-Settlement Drift (10:30 to 14:28 ET)

Primary source: EIA WPSR schedule https://www.eia.gov/petroleum/supply/weekly/schedule.php (verified: Wed 10:30 ET standard; holiday weeks Thu 12:00 ET) + CME CL contract specs https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html (verified) + CME CL settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil (verified: 14:28:00-14:30:00 ET VWAP window)

Mechanism: Information from the 10:30 release continues to be absorbed until the 14:28 ET VWAP window which defines the daily settle; the settle then embeds the drift.

Features: r[t0+10m, 14:27:59] sign relative to r[t0, t0+10m]; continuation vs reversal by surprise decile.

Target: Continuation probability of the first 10-minute move into settle.

Falsify-if: Conditional continuation probability <= unconditional 3h continuation after random 10:30 on non-release days.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: A

## W76Q-E10 — Post-Release Liquidity Refill Half-Life in CL

Primary source: EIA WPSR schedule https://www.eia.gov/petroleum/supply/weekly/schedule.php (verified: Wed 10:30 ET standard; holiday weeks Thu 12:00 ET); CL spec

Mechanism: After the print, depth refills with a decay; entries for any CL strategy during the unrefilled interval pay inflated costs. Measuring the half-life converts the release into an execution gate.

Features: top-of-book and 5-level depth ratio to trailing-hour median; time until ratio >=0.8; spread in ticks (tick 0.01 verified).

Target: Execution-gate duration per release.

Falsify-if: Gate duration is constant across surprise sizes (no dose-response) and unrelated to realized slippage.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W76Q-E11 — Wednesday 10:30 Release x NQ Co-move Window

Primary source: EIA WPSR schedule https://www.eia.gov/petroleum/supply/weekly/schedule.php (verified: Wed 10:30 ET standard; holiday weeks Thu 12:00 ET); NQ via existing vault market data

Mechanism: Oil-surprise to equity-index transmission works via inflation expectations and energy-sector weights; sign is regime-dependent (demand vs supply shock), so only a conditional model is allowed.

Features: oil 10-min return and NQ 10-min return, sign of 60-day rolling corr, VIX regime.

Target: NQ residual drift after controlling for ES/ZN reaction.

Falsify-if: Conditional NQ response is zero after controlling for ZN and 6E returns (nested F-test).

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED + PAID_REALTIME

Priority: B

## W76Q-E12 — Thursday NG Storage Surprise vs 5-Year-Average Deviation

Primary source: EIA WNGSR schedule https://ir.eia.gov/ngs/schedule.html (verified: Thu 10:30 ET standard; holiday exceptions listed) (storage released Thu 10:30 ET)

Mechanism: NG storage change relative to the 5-year average and to a weather-implied expectation (own HDD/CDD model; consensus PP) drives the first-minute move; the deviation of the cumulative inventory from the 5-year mean conditions the sign persistence.

Features: weekly net change minus 5yr avg change; cumulative surplus/deficit percentile; NG return [t0,t0+5m].

Target: First-move persistence vs fade.

Falsify-if: Cumulative surplus percentile adds no explanatory power to weekly surprise (likelihood-ratio test).

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: A+

## W76Q-E13 — WNGSR Holiday-Shift Regime

Primary source: EIA WNGSR schedule https://ir.eia.gov/ngs/schedule.html (verified: Thu 10:30 ET standard; holiday exceptions listed) (Wed 12:00 ET Juneteenth/Thanksgiving/Christmas weeks; Fri 10:30 ET Veterans Day weeks)

Mechanism: Shifted storage releases land in different liquidity and weekly-expiry contexts; Wednesday noon collides with the WPSR digestion window of the same week.

Features: slot types WED_1200, FRI_1030, MON_1200; same-day WPSR indicator.

Target: Slot-specific NG response scale.

Falsify-if: Slot effect not distinguishable from standard Thursday (n small; report as underpowered, never promote on n<30).

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B

## W76Q-E14 — NG Storage Regional Composition Surprise

Primary source: EIA WNGSR schedule https://ir.eia.gov/ngs/schedule.html (verified: Thu 10:30 ET standard; holiday exceptions listed); regional (East/Midwest/South Central/Mountain/Pacific, salt) table structure [PP: confirm current table layout in report]

Mechanism: Regional split (e.g. salt vs non-salt South Central) reveals production vs weather vs power-burn drivers with different price persistence than the headline.

Features: regional surprise vector vs same-week 5yr avg; principal component of regional deviations.

Target: Response persistence class.

Falsify-if: Regional components add no out-of-sample R2 to headline-only model.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B

## W76Q-E15 — NG Expiry Day Colliding With Thursday Storage Release

Primary source: CME NG contract specs https://www.cmegroup.com/markets/energy/natural-gas/natural-gas.contractSpecs.html (verified: termination 3rd last business day of month prior; TAS to 14:30 ET) + EIA WNGSR schedule https://ir.eia.gov/ngs/schedule.html (verified: Thu 10:30 ET standard; holiday exceptions listed)

Mechanism: NG terminates on the 3rd last business day of the month prior to the contract month; when that day is a Thursday the expiring contract absorbs the 10:30 storage shock with thin expiry liquidity.

Features: calendar indicator expiry==Thursday; expiry-contract volume share; spread of M1 vs M2.

Target: Expiring-contract overshoot vs M2.

Falsify-if: Overshoot of M1 relative to M2 on collision days equals non-collision Thursdays.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W76Q-E16 — CL Settlement Window Pin (14:28-14:30 ET)

Primary source: CME CL contract specs https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html (verified) + CME CL settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil (verified: 14:28:00-14:30:00 ET VWAP window)

Mechanism: Front month settles to the VWAP of Globex trades in the 2-minute window; participants with settlement-referenced exposure (TAS, TAM, swaps) concentrate flow there, so price may be pulled toward expected VWAP and released after.

Features: distance of price at 14:27:59 to final settle in ticks; window volume share of day; post-14:30 reversal 5/15 min.

Target: Reversal probability and size after window; distance-to-settle forecast.

Falsify-if: Mean absolute distance-to-settle in the window equals that for random 2-minute windows normalised by volatility (placebo 11:28, 13:28).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S

## W76Q-E17 — CL TAS Flow Pre-Settlement Imbalance

Primary source: CME CL contract specs https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html (verified) + CME CL settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil (verified: 14:28:00-14:30:00 ET VWAP window) (TAS: Rule 524.A; zero or +/-10 ticks; TAS runs to 13:30 CT)

Mechanism: Trading-at-settlement trades are priced off the unknown settle; one-sided TAS accumulation before the window forces offsetting Globex flow in the window.

Features: signed TAS volume (CLT instrument) 13:00-14:28 ET; window VWAP minus 14:27:59 mid. TAS feed fields UNVERIFIED [PP].

Target: Window VWAP displacement direction.

Falsify-if: No correlation between signed TAS flow and window displacement beyond ordinary order flow (partial R2~0).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W76Q-E18 — CL Back-Month Settlement Tier Staleness

Primary source: CME CL contract specs https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html (verified) + CME CL settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil (verified: 14:28:00-14:30:00 ET VWAP window) (Tier1 spread VWAP weighted by months separating legs; Tier2 implied bid/ask; Tier3 net change of previous month)

Mechanism: Back months without spread trades settle by implication (Tier2/3), so published settles are smoothed relative to real market; next-day open can revert toward market.

Features: tier flag per month (inferred by comparing settle to spread-implied); settlement residual; next-open reversion.

Target: Settle-to-open reversion in thin back months.

Falsify-if: Open-minus-settle in Tier3-inferred months is no larger than in Tier1 months.

Horizon: DAILY

Availability: PAID_REALTIME + PUBLIC_BATCH

Priority: B+

## W76Q-E19 — Post-Settle Reopen Gap in CL and GC

Primary source: CME CL contract specs https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html (verified) + CME CL settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil (verified: 14:28:00-14:30:00 ET VWAP window); CME GC contract specs https://www.cmegroup.com/markets/metals/precious/gold.contractSpecs.html (verified) + CME Gold settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/Gold (verified: 13:29-13:30 ET outright, 13:15-13:30 ET spreads) (Globex break 16:00-17:00 CT for CL; 17:00-18:00 ET for GC, verified)

Mechanism: Prices at the 60-minute break boundary reflect thin trade; the settle-to-reopen gap statistic may mean-revert through the Asia session.

Features: gap = open(reopen)-settle normalised by ATR; Asia 3-hour return after.

Target: Gap mean-reversion probability by gap size.

Falsify-if: Gap-fade expectancy not different from zero after cost across 3 years (block bootstrap).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W76Q-E20 — GC 13:29-13:30 ET Window Pin and Reversion

Primary source: CME GC contract specs https://www.cmegroup.com/markets/metals/precious/gold.contractSpecs.html (verified) + CME Gold settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/Gold (verified: 13:29-13:30 ET outright, 13:15-13:30 ET spreads)

Mechanism: Gold front-month settles to the 1-minute VWAP; the very short window makes settlement more sensitive to a single large print than CL.

Features: settle minus 13:28:59 mid; window trade count; max single print share; 13:30+15 min reversal.

Target: Reversal after the window.

Falsify-if: Reversal size equals placebo 1-minute windows.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W76Q-E21 — GC Spread Settlement Threshold State (25 Contracts)

Primary source: CME GC contract specs https://www.cmegroup.com/markets/metals/precious/gold.contractSpecs.html (verified) + CME Gold settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/Gold (verified: 13:29-13:30 ET outright, 13:15-13:30 ET spreads) (Tier1 requires accumulated calendar-spread trades >=25 contracts in 13:15-13:30 ET; Tier2 implied; Tier3 net change; Tier4 block emails)

Mechanism: When spread volume falls under 25, back months settle by fallback tiers; roll-week curves are therefore synthetic in settle data.

Features: spread volume in window per pair; tier proxy; settle-implied spread vs last traded.

Target: Settle-curve artefact flag.

Falsify-if: Settle-implied spreads match last-traded spreads within a tick regardless of volume.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W76Q-E22 — Gold vs Silver Settlement-Clock Stagger

Primary source: CME GC contract specs https://www.cmegroup.com/markets/metals/precious/gold.contractSpecs.html (verified) + CME Gold settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/Gold (verified: 13:29-13:30 ET outright, 13:15-13:30 ET spreads); CME SI contract specs https://www.cmegroup.com/markets/metals/precious/silver.contractSpecs.html (verified: TAS to 12:25 CT, termination 12:25 CT third-last business day) (silver TAS ends 12:25 CT, i.e. 13:25 ET; silver settlement window itself UNVERIFIED [PP])

Mechanism: If silver settles ~5 minutes before gold, the settled gold/silver ratio mixes two clock times and manufactures a spurious ratio move between 13:25-13:30.

Features: GC/SI ratio at each metal's own settle vs at synchronous 13:30 mid.

Target: Ratio artefact size.

Falsify-if: Settled and synchronous ratio differ by <1 tick-equivalent.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B

## W76Q-E23 — Settlement-Window Execution Gate

Primary source: CME CL contract specs https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html (verified) + CME CL settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil (verified: 14:28:00-14:30:00 ET VWAP window); CME GC contract specs https://www.cmegroup.com/markets/metals/precious/gold.contractSpecs.html (verified) + CME Gold settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/Gold (verified: 13:29-13:30 ET outright, 13:15-13:30 ET spreads)

Mechanism: Entries inside settlement windows inherit VWAP-linked flow and altered liquidity; an exclusion mask is a pure execution-quality control.

Features: in_window flags CL 14:28-14:30, GC 13:29-13:30 / 13:15-13:30 (spreads); slippage in window vs adjacent windows.

Target: Slippage uplift.

Falsify-if: Slippage uplift not significant (then drop gate).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W76Q-E24 — Brent 19:28 London vs WTI 14:28 ET DST Misalignment

Primary source: ICE Brent Crude futures https://www.ice.com/products/219/Brent-Crude-Futures (verified: last day = last business day of 2nd month preceding; EFP delivery with cash-settle option vs ICE Brent Index) + ICE Brent/WTI spread spec https://www.ice.com/products/1242/Brent-WTI-Futures-Spread (settlement window 19:28-19:30 London = 14:28-14:30 EST; surfaced via search, page not fully read; PP for exact wording)

Mechanism: ICE spec states the Brent window as 19:28-19:30 London (= 14:28-14:30 EST); UK and US shift clocks on different dates, so for roughly two to three weeks a year the two settles are sampled one hour apart, and settle-derived Brent-WTI spreads inherit an hour of drift.

Features: tz-database computed offset between 19:30 London and 14:30 New York; spread z-score of settle-spread vs synchronous-mid spread in misaligned weeks.

Target: Settle-spread artefact; reversion next day.

Falsify-if: Settle-spread minus synchronous spread has equal variance in aligned and misaligned weeks (Levene).

Horizon: DAILY

Availability: PUBLIC_SCHEDULED (tz rules, verify via IANA tzdata)

Priority: S-

## W76Q-E25 — Brent Expiry Cash-Settle vs Index Convergence Day

Primary source: ICE Brent Crude futures https://www.ice.com/products/219/Brent-Crude-Futures (verified: last day = last business day of 2nd month preceding; EFP delivery with cash-settle option vs ICE Brent Index) + ICE Brent/WTI spread spec https://www.ice.com/products/1242/Brent-WTI-Futures-Spread (settlement window 19:28-19:30 London = 14:28-14:30 EST; surfaced via search, page not fully read; PP for exact wording)

Mechanism: Brent futures expire on the last business day of the second month preceding delivery and can cash-settle vs the ICE Brent Index; the final-day window concentrates convergence flows.

Features: calendar expiry flag; last-day volume share; futures minus index (if licensed; index data PP).

Target: Expiry-day volatility and close dislocation.

Falsify-if: Expiry-day absolute return normalised by vol not above non-expiry days.

Horizon: INTRADAY

Availability: LICENSED_REALTIME [PP for index]

Priority: B+

## W76Q-E26 — Matched-Delivery-Month Brent-WTI Spread Construction

Primary source: ICE Brent Crude futures https://www.ice.com/products/219/Brent-Crude-Futures (verified: last day = last business day of 2nd month preceding; EFP delivery with cash-settle option vs ICE Brent Index) + ICE Brent/WTI spread spec https://www.ice.com/products/1242/Brent-WTI-Futures-Spread (settlement window 19:28-19:30 London = 14:28-14:30 EST; surfaced via search, page not fully read; PP for exact wording) + CME CL contract specs https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html (verified) + CME CL settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil (verified: 14:28:00-14:30:00 ET VWAP window)

Mechanism: Brent Mar expires last business day of Jan; CL Mar terminates 3 business days before 25 Feb (about 20-22 Feb). Between those dates the Brent front is April while CL front is March, so naive front-front spreads are mismatched by a month.

Features: delivery-month map; matched spread S_m = CL_m - BRENT_m; mismatch indicator.

Target: Cleaner spread series for pair logic.

Falsify-if: Matched spread does not have lower first-difference noise than front-front spread.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: A

## W76Q-E27 — Front-Front Spread Discontinuity Window

Primary source: ICE Brent Crude futures https://www.ice.com/products/219/Brent-Crude-Futures (verified: last day = last business day of 2nd month preceding; EFP delivery with cash-settle option vs ICE Brent Index) + ICE Brent/WTI spread spec https://www.ice.com/products/1242/Brent-WTI-Futures-Spread (settlement window 19:28-19:30 London = 14:28-14:30 EST; surfaced via search, page not fully read; PP for exact wording) + CME CL contract specs https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html (verified) + CME CL settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil (verified: 14:28:00-14:30:00 ET VWAP window)

Mechanism: The window between Brent expiry and CL expiry produces a structural jump in naive front-front spread; any model using it learns the calendar, not the economics.

Features: jump size at Brent roll date; days in window per cycle.

Target: Mask period for spread-dependent models.

Falsify-if: No discontinuity in naive spread at Brent roll date (jump insignificant).

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W76Q-E28 — Matched Brent-WTI Spread Intraday Half-Life

Primary source: ICE Brent Crude futures https://www.ice.com/products/219/Brent-Crude-Futures (verified: last day = last business day of 2nd month preceding; EFP delivery with cash-settle option vs ICE Brent Index) + ICE Brent/WTI spread spec https://www.ice.com/products/1242/Brent-WTI-Futures-Spread (settlement window 19:28-19:30 London = 14:28-14:30 EST; surfaced via search, page not fully read; PP for exact wording) + CME CL contract specs https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html (verified) + CME CL settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil (verified: 14:28:00-14:30:00 ET VWAP window)

Mechanism: Spread deviations from a rolling intraday mean should decay at a half-life limited by cross-exchange latency; half-life is state dependent (DST alignment, EIA minutes).

Features: OU half-life on 1-min matched spread; session-specific.

Target: Reversion probability by z-bucket.

Falsify-if: Half-life stable across states and indistinguishable from a random walk (ADF p>0.1).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W76Q-E29 — CL Last-Trade-Day Calendar Hazard

Primary source: CME CL contract specs https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html (verified) + CME CL settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil (verified: 14:28:00-14:30:00 ET VWAP window) (3 business days before the 25th, or 4 if the 25th is not a business day)

Mechanism: Expiry-day trading in the deliverable contract is thinner and settlement-sensitive; roll calendars computed with a fixed 'x days before' rule misplace expiry by holidays.

Features: exact calendar function with NYMEX holiday table; expiry-day volume, spread to M2.

Target: Expiry-day exclusion mask / vol scale.

Falsify-if: Expiry-day realized vol/volume not different from adjacent days.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W76Q-E30 — CL Volume Crossover Roll Detector

Primary source: CME CL contract specs https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html (verified) + CME CL settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil (verified: 14:28:00-14:30:00 ET VWAP window)

Mechanism: The dominant contract changes when M2 volume exceeds M1; trading the wrong contract inflates costs and basis noise.

Features: daily and 5-min volume ratio M2/M1; crossover day offset vs expiry.

Target: Roll-day estimate usable intraday.

Falsify-if: Crossover day does not predict spread depth migration.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W76Q-E31 — NG Expiry-Day Hazard (3rd Last Business Day)

Primary source: CME NG contract specs https://www.cmegroup.com/markets/energy/natural-gas/natural-gas.contractSpecs.html (verified: termination 3rd last business day of month prior; TAS to 14:30 ET)

Mechanism: NG expiry rule differs from CL; expiry volume and single-print risk in the final day.

Features: exact calendar; expiry volume; M1-M2 spread dispersion.

Target: Exclusion mask / size scale.

Falsify-if: No elevated dispersion on expiry days.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: B

## W76Q-E32 — GC Delivery-Month Roll Migration (Extends W49P-E10)

Primary source: CME GC contract specs https://www.cmegroup.com/markets/metals/precious/gold.contractSpecs.html (verified) + CME Gold settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/Gold (verified: 13:29-13:30 ET outright, 13:15-13:30 ET spreads) (delivery any business day of delivery month; listed 26 consecutive months + Jun/Dec). First-notice-day rule date UNVERIFIED [PP]. Extends W49P-E10.

Mechanism: W49P-E10 treats first-notice compression as a delivery-supply state; this edge is the executable intraday roll-timing signal: open-interest and volume migration rate per hour between active months.

Features: 5-min volume share of M2/(M1+M2) around roll; dOI by day.

Target: Optimal switch-over time for continuous front.

Falsify-if: Switch timing by volume crossover shows no execution-cost advantage vs fixed calendar roll.

Horizon: INTRADAY

Availability: PAID_REALTIME + PUBLIC_BATCH

Priority: A-

## W76Q-E33 — GC/SI Expiry-Day Thin-Tape Mask

Primary source: CME GC contract specs https://www.cmegroup.com/markets/metals/precious/gold.contractSpecs.html (verified) + CME Gold settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/Gold (verified: 13:29-13:30 ET outright, 13:15-13:30 ET spreads) (terminates 12:30 CT 3rd last business day); CME SI contract specs https://www.cmegroup.com/markets/metals/precious/silver.contractSpecs.html (verified: TAS to 12:25 CT, termination 12:25 CT third-last business day)

Mechanism: Spot-month trades terminate mid-session; expiring contracts leave residual thin trade at the tail.

Features: expiry flag; spread of expiring vs next; trade count.

Target: Exclusion mask.

Falsify-if: No microstructure difference.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B

## W76Q-E34 — Daily Weekly-Option Expiry Pinning in CL and GC

Primary source: CME GC contract specs https://www.cmegroup.com/markets/metals/precious/gold.contractSpecs.html (verified) + CME Gold settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/Gold (verified: 13:29-13:30 ET outright, 13:15-13:30 ET spreads) lists weekly options Mon-Fri; CL page banner lists Monday and Wednesday WTI weeklies (verified); expiry times and strike grids PP

Mechanism: Daily expiries create strike-specific hedging near expiry; price pin probability rises with open interest concentration (CME Open Interest Profile Tool, verified present).

Features: OI by strike at expiry day; distance to max-OI strike in ATR; pin hit rate by hour.

Target: Pin attraction toward max-OI strike.

Falsify-if: Distance to max-OI strike at expiry equals distance to random strike of equal rank.

Horizon: INTRADAY

Availability: PAID_REALTIME + PUBLIC_BATCH

Priority: A-

## W76Q-E35 — Option-Expiry x Settlement-Window Collision

Primary source: CME GC contract specs https://www.cmegroup.com/markets/metals/precious/gold.contractSpecs.html (verified) + CME Gold settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/Gold (verified: 13:29-13:30 ET outright, 13:15-13:30 ET spreads); CME CL contract specs https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html (verified) + CME CL settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil (verified: 14:28:00-14:30:00 ET VWAP window)

Mechanism: When options expire from the settlement price, the settlement window becomes also the option hedge unwind window.

Features: indicator expiry day with window; window volume spike vs ordinary day.

Target: Window pin amplitude.

Falsify-if: Amplitude identical on expiry vs non-expiry days.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W76Q-E36 — LBMA PM Auction (15:00 London) Window Drift

Primary source: LBMA prices page https://www.lbma.org.uk/prices-and-data/precious-metal-prices (verified: IBA auctions gold 10:30 and 15:00 London, silver 12:00; no weekend/UK bank holiday prices; IBA licence needed for real-time/historical use) + IBA methodology https://www.ice.com/publicdocs/LBMA_Gold_Price_and_LBMA_Silver_Price_Calculation_Methodology.pdf (URL from search; PP until read)

Mechanism: Large physical and ETF-linked flows reference the PM fix; auction price is set when buyer/seller imbalance falls within a tolerance (reported 10,000 oz in secondary search, PP).

Features: GC return [-30m,0], [0,+30m] relative to 15:00 London; DST aware; fix-minus-futures basis (E38).

Target: Drift/reversion around fix.

Falsify-if: Return-to-fix and post-fix returns equal placebo hours.

Horizon: INTRADAY

Availability: LICENSED_REALTIME (fix) + PAID_REALTIME

Priority: A+

## W76Q-E37 — LBMA AM-PM Fix Gap Decomposition

Primary source: LBMA prices page https://www.lbma.org.uk/prices-and-data/precious-metal-prices (verified: IBA auctions gold 10:30 and 15:00 London, silver 12:00; no weekend/UK bank holiday prices; IBA licence needed for real-time/historical use) + IBA methodology https://www.ice.com/publicdocs/LBMA_Gold_Price_and_LBMA_Silver_Price_Calculation_Methodology.pdf (URL from search; PP until read)

Mechanism: The AM (10:30) and PM (15:00) London fixes partition the London day; the AM-PM gap versus the PM-to-next-AM gap measures where gold information arrives.

Features: gap_AM_PM, gap_PM_AM, ratio to 20d mean; relative to NQ/ZN returns.

Target: Session information-share state.

Falsify-if: Ratio carries no information about next-day NY-session direction.

Horizon: DAILY

Availability: LICENSED_REALTIME

Priority: B+

## W76Q-E38 — LBMA Fix vs Futures Basis Dislocation

Primary source: LBMA prices page https://www.lbma.org.uk/prices-and-data/precious-metal-prices (verified: IBA auctions gold 10:30 and 15:00 London, silver 12:00; no weekend/UK bank holiday prices; IBA licence needed for real-time/historical use) + IBA methodology https://www.ice.com/publicdocs/LBMA_Gold_Price_and_LBMA_Silver_Price_Calculation_Methodology.pdf (URL from search; PP until read); CME GC contract specs https://www.cmegroup.com/markets/metals/precious/gold.contractSpecs.html (verified) + CME Gold settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/Gold (verified: 13:29-13:30 ET outright, 13:15-13:30 ET spreads)

Mechanism: Auction price should equal executable spot; futures-implied spot (GC adjusted by carry) minus fix is a dislocation measure at 10:30/15:00.

Features: basis_b = fix - (GC_mid - carry_est); carry estimate parameters PP.

Target: Reversion of |basis| beyond k sigma.

Falsify-if: |basis| z does not predict next 30m GC return.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: B+

## W76Q-E39 — DST-Mismatch Weeks: London Fix vs COMEX Alignment

Primary source: LBMA prices page https://www.lbma.org.uk/prices-and-data/precious-metal-prices (verified: IBA auctions gold 10:30 and 15:00 London, silver 12:00; no weekend/UK bank holiday prices; IBA licence needed for real-time/historical use) + IBA methodology https://www.ice.com/publicdocs/LBMA_Gold_Price_and_LBMA_Silver_Price_Calculation_Methodology.pdf (URL from search; PP until read); GC settlement window 13:29-13:30 ET

Mechanism: London 15:00 equals 10:00 ET when both zones share offset, but in mismatch weeks equals 11:00 ET (or 09:00 ET) shifting the fix relative to US data releases at 08:30/10:00 ET.

Features: tz computed ET time of each fix; collision indicators with US releases.

Target: Fix-vs-release collision calendar.

Falsify-if: Fix-window return variance unaffected by collision.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: S-

## W76Q-E40 — Silver 12:00 London Fix Window

Primary source: LBMA prices page https://www.lbma.org.uk/prices-and-data/precious-metal-prices (verified: IBA auctions gold 10:30 and 15:00 London, silver 12:00; no weekend/UK bank holiday prices; IBA licence needed for real-time/historical use) + IBA methodology https://www.ice.com/publicdocs/LBMA_Gold_Price_and_LBMA_Silver_Price_Calculation_Methodology.pdf (URL from search; PP until read)

Mechanism: Single daily silver auction at 12:00 London falls at ~07:00 ET, before US cash open; thin liquidity amplifies auction prints.

Features: SI return [-15m,+15m]; spread; subsequent NY open reversion.

Target: Post-fix NY-open fade.

Falsify-if: Fade size equals placebo hour.

Horizon: INTRADAY

Availability: LICENSED_REALTIME + PAID_REALTIME

Priority: B+

## W76Q-E41 — PGM 09:45 and 14:00 London Fix Cross-Metal State

Primary source: LBMA prices page https://www.lbma.org.uk/prices-and-data/precious-metal-prices (verified: IBA auctions gold 10:30 and 15:00 London, silver 12:00; no weekend/UK bank holiday prices; IBA licence needed for real-time/historical use) + IBA methodology https://www.ice.com/publicdocs/LBMA_Gold_Price_and_LBMA_Silver_Price_Calculation_Methodology.pdf (URL from search; PP until read) (platinum/palladium 09:45 and 14:00, IBA)

Mechanism: PGM auctions mark industrial risk; their drift relative to gold can lead gold ratio changes.

Features: PL/PA fix returns minus GC returns.

Target: Cross-metal lead sign.

Falsify-if: No lead beyond contemporaneous correlation.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: B

## W76Q-E42 — No-Fix Day Regime

Primary source: LBMA prices page https://www.lbma.org.uk/prices-and-data/precious-metal-prices (verified: IBA auctions gold 10:30 and 15:00 London, silver 12:00; no weekend/UK bank holiday prices; IBA licence needed for real-time/historical use) + IBA methodology https://www.ice.com/publicdocs/LBMA_Gold_Price_and_LBMA_Silver_Price_Calculation_Methodology.pdf (URL from search; PP until read) (no prices on weekends or UK bank holidays)

Mechanism: On US-open/UK-closed days, benchmark-referencing instruments lack a fresh fix and spreads may widen; GLD NAV reference behaviour unverified.

Features: UK holiday calendar x US open; spread and volume.

Target: Liquidity / basis anomaly flag.

Falsify-if: No spread/volume anomaly on UK-holiday US days.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B

## W76Q-E43 — Fix Auction Duration and Rounds as Stress Proxy

Primary source: LBMA prices page https://www.lbma.org.uk/prices-and-data/precious-metal-prices (verified: IBA auctions gold 10:30 and 15:00 London, silver 12:00; no weekend/UK bank holiday prices; IBA licence needed for real-time/historical use) + IBA methodology https://www.ice.com/publicdocs/LBMA_Gold_Price_and_LBMA_Silver_Price_Calculation_Methodology.pdf (URL from search; PP until read) - round-level data publication UNVERIFIED [PP]

Mechanism: More rounds / longer auctions imply imbalance and stress.

Features: rounds_count, duration; if unavailable -> downgrade/kill.

Target: Stress state.

Falsify-if: Data not published or no relation to next-day vol: kill.

Horizon: INTRADAY

Availability: UNKNOWN_MEASURED

Priority: B

## W76Q-E44 — GLD Prior-Day Holdings Change as Intraday Prior

Primary source: SSGA GLD page https://www.ssga.com/us/en/individual/etfs/funds/spdr-gold-trust-gld (search-verified NAV/INAV labels; daily tonnes field PP)

Mechanism: Creation/redemption occurs in baskets of physical gold; net tonnage published next morning is known before the NY session and may condition the day.

Features: tonnes change z; sign; GC open-to-11:00 return.

Target: Directional prior at open.

Falsify-if: No relation after controlling for prior-day GC return.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B+

## W76Q-E45 — GLD NAV-Fix Reference Premium/Discount vs GC

Primary source: SSGA GLD page (search-verified: trust values gold on LBMA Gold Price PM; NAV timing 4pm PP) + prospectus PP

Mechanism: Because NAV references the PM fix while shares trade continuously, intraday premium to fix-implied NAV is the gold-ETF creation pressure indicator.

Features: price/iNAV-1, GC-implied; persistence minutes.

Target: Creation/redemption pressure proxy.

Falsify-if: Premium z does not predict GLD/GC convergence.

Horizon: INTRADAY

Availability: PUBLIC_REALTIME / PAID_REALTIME

Priority: B+

## W76Q-E46 — USO Roll-Window Calendar-Spread Pressure

Primary source: Law-firm alert https://gtlaw.com/nl/insights/2020/5/historic-decline-in-oil-may-trigger-additional-disclosures-by-fcms-and-product-restrictions (search-verified: USO moved to a 10-day roll from May 2020; current schedule PP - read USO prospectus on EDGAR)

Mechanism: A large ETF rolling M1 to M2 over consecutive days pressures the M1-M2 spread in the roll window.

Features: roll-window day index; dSpread vs non-roll windows.

Target: Spread pressure only in roll window.

Falsify-if: No spread differential after calendar controls.

Horizon: INTRADAY

Availability: PUBLIC_BATCH

Priority: B

## W76Q-E47 — Gold Miners vs Gold Open Gap Lead-Lag

Primary source: CME GC contract specs https://www.cmegroup.com/markets/metals/precious/gold.contractSpecs.html (verified) + CME Gold settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/Gold (verified: 13:29-13:30 ET outright, 13:15-13:30 ET spreads) + cash equity ETFs

Mechanism: GDX/GDXJ cannot trade before 09:30 ET while gold trades 23h; the gap at the open encodes unspent gold information plus equity beta.

Features: GC return 18:00-09:30 vs GDX open gap; residual after SPX beta.

Target: Gap-fill vs continuation.

Falsify-if: Gap residual unrelated to first-30-minute GDX return.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W76Q-E48 — Energy Equity Sector vs CL Response Lag at EIA

Primary source: EIA WPSR schedule https://www.eia.gov/petroleum/supply/weekly/schedule.php (verified: Wed 10:30 ET standard; holiday weeks Thu 12:00 ET)

Mechanism: XLE and E&P stocks respond to oil moves with a delay and with equity beta contamination, offering a delayed confirmation entry.

Features: CL 1m return; XLE 1m lag-correlation at t0+[0,300]s.

Target: Confirmation timing.

Falsify-if: No lead-lag at 1-second resolution.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W76Q-E49 — OPEC+ Sunday Meeting Pre-Open Shock

Primary source: OPEC press releases https://www.opec.org/pr-detail/593-1-march-2026.html (search-verified: V8 monthly meetings 4 Jan, 1 Feb, 1 Mar, 5 Apr 2026, all Sundays; later 2026 calendar PP) (all four meetings 2026 dated Sundays; Globex re-opens Sunday 17:00 CT, verified)

Mechanism: Decisions announced Sundays precede the Globex reopening, turning the first minutes after 17:00 CT into the information event with thin liquidity.

Features: first-30-min CL return after reopen; gap vs Friday settle; statement timestamp.

Target: Gap size and fade.

Falsify-if: First-minutes returns on OPEC-Sunday equal returns on ordinary Sunday opens.

Horizon: INTRADAY

Availability: PUBLIC_EVENT_DRIVEN

Priority: S-

## W76Q-E50 — OPEC+ Statement Priced-In Gap Fade

Primary source: OPEC press releases https://www.opec.org/pr-detail/593-1-march-2026.html (search-verified: V8 monthly meetings 4 Jan, 1 Feb, 1 Mar, 5 Apr 2026, all Sundays; later 2026 calendar PP); CME OPEC Watch https://www.cmegroup.com/trading/energy/cme-opec-watch-tool.html (linked on CL page; data access PP)

Mechanism: Option-implied outcome probabilities before the meeting show how much is priced; surprise vs implied probability sizes the gap.

Features: implied probability of decision; realised outcome; gap normalised.

Target: Gap fade vs extend.

Falsify-if: Gap not related to implied-probability surprise.

Horizon: INTRADAY

Availability: PUBLIC_WEB_ONLY [PP]

Priority: B+

## W76Q-E51 — Energy Calendar Staleness Guard

Primary source: OPEC press releases https://www.opec.org/pr-detail/593-1-march-2026.html (search-verified: V8 monthly meetings 4 Jan, 1 Feb, 1 Mar, 5 Apr 2026, all Sundays; later 2026 calendar PP); no verified forward calendar beyond April 2026 (homepage references a 68th JMMC press item dated 4 Oct 2026, unverified)

Mechanism: Meeting dates are announced by press release, not by a machine-readable calendar; a stale assumption causes missed event gates.

Features: last-seen meeting announcement; days since; unknown-date flag.

Target: Event-gate completeness.

Falsify-if: Collector finds a machine-readable schedule (then replace).

Horizon: DAILY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B

## W76Q-E52 — Curve Slope Regime Conditioning of Intraday Reversion

Primary source: CME CL contract specs https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html (verified) + CME CL settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil (verified: 14:28:00-14:30:00 ET VWAP window)

Mechanism: Backwardated vs contango curves change inventory-risk premia and the persistence of shocks.

Features: M1-M12 / M1 percent; sign; intraday reversion half-lives by regime.

Target: Regime-conditioned parameters.

Falsify-if: Parameters identical across regimes.

Horizon: SLOW_PRIOR

Availability: PAID_REALTIME

Priority: B+

## W76Q-E53 — 3-2-1 Crack Divergence Leading CL

Primary source: CME CL contract specs https://www.cmegroup.com/markets/energy/crude-oil/light-sweet-crude.contractSpecs.html (verified) + CME CL settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/NYMEX+Crude+Oil (verified: 14:28:00-14:30:00 ET VWAP window) + RB/HO specs (CME energy products listed on CL page, verified listing)

Mechanism: Product margins move on supply chain news first.

Features: crack z-score vs CL z-score gap; subsequent CL move.

Target: Direction of CL catch-up.

Falsify-if: Crack divergence does not predict CL catch-up.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W76Q-E54 — Micro Gold vs Standard Gold Flow Share

Primary source: CME GC contract specs https://www.cmegroup.com/markets/metals/precious/gold.contractSpecs.html (verified) + CME Gold settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/Gold (verified: 13:29-13:30 ET outright, 13:15-13:30 ET spreads) (MGC listed with GC in CME metals menu, verified)

Mechanism: Micro contract flow share reflects small-account activity; extreme share may flag retail chase.

Features: MGC volume/GC-equivalent volume; extremes; next-hour reversal.

Target: Fade of retail-driven spikes.

Falsify-if: Share carries no information.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W76Q-E55 — CME Dynamic Circuit-Breaker State for CL and GC

Primary source: CME price limits page https://www.cmegroup.com/trading/price-limits.html (fetched; query tool did not return halt rules; rule detail PP)

Mechanism: Dynamic circuit-breaker pauses interrupt price discovery; knowledge of reference and band improves risk gating.

Features: distance to band; pause events; reopen path.

Target: Gate flag.

Falsify-if: No pauses occur in sample => park as monitor.

Horizon: INTRADAY

Availability: PUBLIC_WEB_ONLY [PP]

Priority: B+

## W76Q-E56 — Fix-Hour Volume Clock Seasonality Knots in Gold

Primary source: LBMA prices page https://www.lbma.org.uk/prices-and-data/precious-metal-prices (verified: IBA auctions gold 10:30 and 15:00 London, silver 12:00; no weekend/UK bank holiday prices; IBA licence needed for real-time/historical use) + IBA methodology https://www.ice.com/publicdocs/LBMA_Gold_Price_and_LBMA_Silver_Price_Calculation_Methodology.pdf (URL from search; PP until read); CME GC contract specs https://www.cmegroup.com/markets/metals/precious/gold.contractSpecs.html (verified) + CME Gold settlement procedure https://www.cmegroup.com/confluence/display/EPICSANDBOX/Gold (verified: 13:29-13:30 ET outright, 13:15-13:30 ET spreads)

Mechanism: Volume and vol spike at fix windows, COMEX settlement and US data times; an hourly clock with knot points removes seasonality before signal evaluation.

Features: hour-of-day vol curve with knots at 10:30/15:00 London, 13:30 ET.

Target: Seasonality-adjusted returns.

Falsify-if: Knot-adjusted Sharpe differences vanish.

Horizon: INTRADAY

Availability: LICENSED_REALTIME + PAID_REALTIME

Priority: B+

## Final architecture edge (Truth Ladder)

Truth Ladder for W76Q: L0 calendar and rule objects (EIA schedules with Updated-flag hash, CME specs, ICE specs, tz-computed offsets) -> L1 timestamped event state (release_slot, in_window, expiry flag, DST misalignment) -> L2 conditional envelopes and placebos (same-time non-event windows) -> L3 execution gates (liquidity refill, window mask) -> L4 pair/curve logic with matched delivery months -> L5 intermediate-outcome promotion gate. Any element depending on PROVENANCE_PENDING sources stays at L1 and cannot rise.

## Highest-priority W76Q tests

1. W76Q-E16 CL Settlement Window Pin (14:28-14:30 ET)
2. W76Q-E20 GC 13:29-13:30 ET Window Pin and Reversion
3. W76Q-E24 Brent 19:28 London vs WTI 14:28 ET DST Misalignment
4. W76Q-E36 LBMA PM Auction (15:00 London) Window Drift
5. W76Q-E39 DST-Mismatch Weeks: London Fix vs COMEX Alignment
6. W76Q-E49 OPEC+ Sunday Meeting Pre-Open Shock
7. W76Q-E12 Thursday NG Storage Surprise vs 5-Year-Average Deviation
8. W76Q-E04 Cushing-Stock Surprise to M1-M2 Spread Response
9. W76Q-E01 WPSR 10:30 Release Reaction Envelope
10. W76Q-E26 Matched-Delivery-Month Brent-WTI Spread Construction
