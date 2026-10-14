# Wave 84X — Cross-Asset Linkage State

Namespace: **W84X**

Thesis: intraday strategies trade a changing joint distribution. The same ZN move means a hedge in one stock-bond regime and a common shock in another; gold loads on real yields (daily, lagged) but is traded against nominal yields and the dollar intraday; BTC trades through weekends while equity index futures are shut; ETFs and futures differ by clock and arbitrage capacity. The research target is the linkage state (sign, beta, factor share, lead direction, stability) as a risk gate, hedge ratio and confirmation filter, not a directional view.

Boundary: W62C owns CFTC positioning crowding including cross-asset crowd clusters (E29); W70B owns Globex microstructure including cross-instrument OFI lead-lag (E25); W77V owns volatility products; W78E execution quality; W76Q energy and metals clocks; W6N NQ/gold fundamental links; W26/W27 forced flows and constraint states. W84X owns the cross-asset correlation, beta, composite and lead-lag state and ETF-versus-futures dislocation as a regime layer.

All candidates are research hypotheses only. Claude owns later implementation. No profitability is claimed; every threshold is a parameter to be calibrated under the intermediate-outcome promotion gate.

## W84X-E01 — Rate-Beta of Gold on ZN Returns by Stock-Bond Sign Regime

Primary source: Campbell, Pflueger, Viceira NBER w20070 https://nber.org/system/files/working_papers/w20070/w20070.pdf (search-verified: bond-stock beta varies by monetary regime; retitled 2018 'Macroeconomic Drivers of Bond and Equity Risks'); CME ZN/GC tape

Mechanism: Gold responds to the real-rate component of yield moves; the nominal-yield (ZN) beta is unstable because yield changes are dominated by real or breakeven shocks depending on the inflation/monetary regime.

Features: rolling 30-min OLS beta of GC on ZN returns; sign of NQ-ZN rolling corr; split beta by regime.

Target: Conditional GC response to a ZN move.

Falsify-if: Beta is statistically identical across stock-bond sign regimes (Chow test across 3 years).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S

## W84X-E02 — Daily 10y Real Yield Change as Next-Session Gold Prior

Primary source: FRED DFII10 https://fred.stlouisfed.org/series/DFII10 (verified: daily 10y TIPS constant-maturity yield from Fed H.15; page last updated 9 Oct 2026 15:16 CDT with last observation 8 Oct 2026, i.e. one business day lag)

Mechanism: Real yield is the opportunity cost of gold (Erb-Harvey) and is available only after the day with a lag; its prior-day change should be used at t+1 only, never at t.

Features: d DFII10 (t-1) lagged to availability time; GC overnight/RTH returns on day t+1.

Target: Directional prior or vol scaling at the open.

Falsify-if: Lagged real-yield change has no incremental information after prior-day GC return and ZN return.

Horizon: SLOW_PRIOR

Availability: PUBLIC_DELAYED

Priority: B+

## W84X-E03 — Intraday Breakeven-vs-Real Decomposition via ETF Pair

Primary source: US Treasury interest-rate statistics https://home.treasury.gov/policy-issues/financing-the-government/interest-rate-statistics (verified: curve inputs are NY Fed indicative bids at about 15:30 ET); ETF pair TIP vs IEF (tickers are the author's assumption; confirm product docs PP)

Mechanism: Nominal yield change = real + breakeven; ETF pair gives a tradable intraday split not published as an official intraday TIPS curve.

Features: r_TIP - beta*r_IEF residual; rolling beta; residual sign vs GC and NQ.

Target: Which component drives the current ZN move.

Falsify-if: Residual has no explanatory power for GC beyond ZN.

Horizon: INTRADAY

Availability: PUBLIC_REALTIME

Priority: A-

## W84X-E04 — Stock-Bond Correlation Sign as NQ Hedge and Gate

Primary source: Campbell, Pflueger, Viceira NBER w20070 https://nber.org/system/files/working_papers/w20070/w20070.pdf (search-verified: bond-stock beta varies by monetary regime; retitled 2018 'Macroeconomic Drivers of Bond and Equity Risks')

Mechanism: When stock-bond correlation is positive (inflation-led regime), bonds fail as equity hedge and rate shocks hit NQ and ZN together.

Features: rolling 60-min corr(NQ, ZN), 20-day daily corr, sign hysteresis (see E50).

Target: Risk gate / hedge ratio.

Falsify-if: Hedge ratio computed ignoring sign does equal or better in out-of-sample drawdown.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S-

## W84X-E05 — Inflation-Regime Switch Marker

Primary source: Campbell, Pflueger, Viceira NBER w20070 https://nber.org/system/files/working_papers/w20070/w20070.pdf (search-verified: bond-stock beta varies by monetary regime; retitled 2018 'Macroeconomic Drivers of Bond and Equity Risks'); CPI release timing PP (BLS calendar not fetched)

Mechanism: Regime break is typically revealed on inflation prints; storing a discrete regime from release-day cross-asset reaction fingerprints.

Features: release-day sign(corr change), ZN/NQ co-move; regime posterior.

Target: Regime label for E04.

Falsify-if: Label flips are noise (permutation test of flip dates).

Horizon: SLOW_PRIOR

Availability: PUBLIC_SCHEDULED

Priority: B+

## W84X-E06 — FOMC Day Cross-Asset Correlation Spike Window

Primary source: Fed FOMC calendar https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm (verified: 27-28 Oct and 8-9 Dec 2026; 2027 dates listed; minutes three weeks after decision; statement time not on page - 14:00 ET PP)

Mechanism: Decision day collapses cross-asset dimensionality: NQ, ZN, 6E, GC load on one policy factor in the minutes after the statement.

Features: first PC share of 1-min returns [stmt, stmt+30m] vs 60-day baseline; statement timestamp from Fed press release feed (PP).

Target: Factor-share gate for sizing.

Falsify-if: PC1 share on FOMC days does not exceed non-FOMC placebo days.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED + PAID_REALTIME

Priority: A+

## W84X-E07 — FOMC Minutes Release Cross-Asset Fingerprint

Primary source: Fed FOMC calendar https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm (verified: 27-28 Oct and 8-9 Dec 2026; 2027 dates listed; minutes three weeks after decision; statement time not on page - 14:00 ET PP) (minutes 3 weeks after decision, verified)

Mechanism: Minutes are a scheduled text event with smaller surprise; fingerprint tests whether any cross-asset move survives.

Features: Same envelope as E06 at minutes time (time PP).

Target: Response scale.

Falsify-if: Zero response vs placebo.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B

## W84X-E08 — Pre-FOMC Correlation Compression

Primary source: Fed FOMC calendar https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm (verified: 27-28 Oct and 8-9 Dec 2026; 2027 dates listed; minutes three weeks after decision; statement time not on page - 14:00 ET PP)

Mechanism: Positioning ahead of decisions reduces cross-asset co-movement (idiosyncratic quiet) then jumps.

Features: rolling corr matrix mean off-diagonal in the 24h before; jump size after.

Target: Jump forecast.

Falsify-if: No pre-event compression relative to placebo days.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W84X-E09 — Dollar Proxy Beta of NQ and GC (6E-based)

Primary source: ICE US Dollar Index methodology (direct URL returned 404; weights unverified) PROVENANCE_PENDING; CME 6E spec PP

Mechanism: Euro futures proxy for the dollar index when the official index weights are unavailable; dollar-to-asset betas drift by session.

Features: 6E return betas of NQ, GC by session (Asia/London/NY).

Target: Session-specific dollar beta.

Falsify-if: Session betas equal.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W84X-E10 — Trade-Weighted Dollar vs Dollar-Index Divergence (Slow)

Primary source: Fed H.10 https://www.federalreserve.gov/releases/h10/default.htm (verified: bilateral rates and dollar indexes released Mondays 16:15 for prior business week)

Mechanism: Broad trade-weighted dollar differs from the euro-heavy futures index; divergence is a slow prior that is published weekly with a lag so only usable as a state descriptor.

Features: Broad index weekly change minus 6E-weighted proxy change (vintage aligned to Monday 16:15).

Target: Slow prior on gold/EM.

Falsify-if: Divergence carries no information.

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B

## W84X-E11 — Dollar-Yield-Gold Triangle Residual

Primary source: FRED DFII10 https://fred.stlouisfed.org/series/DFII10 (verified: daily 10y TIPS constant-maturity yield from Fed H.15; page last updated 9 Oct 2026 15:16 CDT with last observation 8 Oct 2026, i.e. one business day lag); Fed H.10 https://www.federalreserve.gov/releases/h10/default.htm (verified: bilateral rates and dollar indexes released Mondays 16:15 for prior business week)

Mechanism: GC modeled as function of ZN (rates) and 6E (dollar); residual is the gold-specific component, expected to mean revert unless a gold-specific shock.

Features: rolling regression residual z; half-life; entry only if residual z beyond k and no gold-news flag.

Target: Residual reversion.

Falsify-if: Residual reversion half-life is infinite (no stationarity).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W84X-E12 — Risk-On/Off Composite Definition

Primary source: SEC Rule 17 CFR 270.6c-11 (ETF rule; adopting Release 33-10695) via law-firm summaries (search-verified: daily holdings, prior-day NAV/premium-discount, 30-day median bid-ask, >2% for >7 days disclosure) for ETF components; CME futures for others

Mechanism: A composite of equity (NQ), credit proxy (HYG), carry (6J), cyclicals (HG), safe haven (ZN, GC) and crypto (BTC) gives a single state variable; weights learned by PCA not asserted.

Features: PC1 of z-scored 5-min returns; stability of loadings; PC1 sign.

Target: Regime scalar.

Falsify-if: PC1 explains below baseline under shuffle.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S-

## W84X-E13 — Absorption Ratio of Cross-Asset Returns

Primary source: Kritzman et al. 'Principal Components as a Measure of Systemic Risk' (not fetched) PROVENANCE_PENDING

Mechanism: Share of variance in the first k eigenvectors rises before stress.

Features: eigenvalue share top-2 of rolling 60-min returns across 10 assets.

Target: Systemic-stress prior.

Falsify-if: No relation with next-hour realized vol.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W84X-E14 — Correlation Matrix Eigenvalue Gap Gate

Primary source: Random matrix practice; standard linear algebra (no primary needed)

Mechanism: Large gap between first and second eigenvalue means one macro factor dominates, reducing diversification.

Features: lambda1/lambda2, Marchenko-Pastur threshold.

Target: Position-size multiplier.

Falsify-if: Gate does not improve risk-adjusted sizing out-of-sample.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W84X-E15 — ZN to ES/NQ Lead at Rate-Sensitive Releases

Primary source: Hasbrouck (2003) J. Finance 58(6):2375-2400 'Intraday Price Formation in U.S. Equity Index Markets' (search-verified: most price discovery in E-mini; SPY smaller role; index ETFs weaker) (E-mini dominates equity price discovery); ZN timestamp structure PP

Mechanism: At rate-sensitive prints, ZN reacts first; NQ follows with a measurable delay.

Features: cross-correlation of 100ms returns around t0.

Target: Lag in seconds, tradable only if above latency + cost.

Falsify-if: Lag below costs/latency; no lead.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W84X-E16 — Yen Futures Risk-Off Lead to NQ

Primary source: CME 6J spec https://www.cmegroup.com/markets/fx/g10/japanese-yen.contractSpecs.html (not fetched) PROVENANCE_PENDING

Mechanism: Carry unwinds show first in JPY crosses (positive 6J) before equities during Asia/Europe hours.

Features: 6J 5-min return shock vs NQ next 30m.

Target: NQ drawdown probability.

Falsify-if: 6J shock has no incremental predictive power after VIX proxy.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W84X-E17 — Copper-Gold Ratio Intraday Growth Proxy

Primary source: CME HG/GC specs (HG listed in CME metals menu, verified listing)

Mechanism: Cyclical vs safe-haven metal ratio is a growth/risk gauge; intraday change reveals risk repricing.

Features: ratio z and change over 30 min; lead vs NQ and ZN yields.

Target: Growth-shock direction.

Falsify-if: Ratio has no lead over ZN/NQ.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W84X-E18 — Oil Shock to Breakeven to Gold Multi-Hop Chain

Primary source: CME CL spec (verified), ETF pair as E03

Mechanism: Oil moves breakevens and inflation expectations before real yield responds, then gold.

Features: CL->TIP/IEF residual->GC lagged cross-correlation chain.

Target: Delayed gold response.

Falsify-if: No hop-two lag.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W84X-E19 — Weekend BTC Move as Sunday NQ Gap Predictor

Primary source: CME Bitcoin futures spec https://www.cmegroup.com/markets/cryptocurrencies/bitcoin/bitcoin.contractSpecs.html (verified: Globex 24/7 except Sat 02:00-04:00 CT and Mon-Fri 16:00-16:02 CT; termination 16:00 London last Friday; TAS/BTIC; tick $5=25)

Mechanism: CME BTC futures trade through the weekend (only maintenance gaps) so BTC captures risk sentiment while NQ is shut; Sunday 17:00 CT NQ reopen can gap toward it.

Features: BTC return Fri 16:00 CT to Sun reopen; NQ Sunday gap.

Target: Gap fade/continuation.

Falsify-if: No relation beyond ES/6E weekend ticks.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W84X-E20 — BTC 16:00-16:02 CT Maintenance Gap Cross-Asset Hole

Primary source: CME Bitcoin futures spec https://www.cmegroup.com/markets/cryptocurrencies/bitcoin/bitcoin.contractSpecs.html (verified: Globex 24/7 except Sat 02:00-04:00 CT and Mon-Fri 16:00-16:02 CT; termination 16:00 London last Friday; TAS/BTIC; tick $5=25)

Mechanism: Brief mon-fri maintenance window coincides with equity cash close region; fake gaps in BTC series can contaminate correlation.

Features: mask minutes; correlation recomputed with/without.

Target: Data-quality correction.

Falsify-if: Corr estimates unchanged => remove edge.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W84X-E21 — Monthly BTC Expiry 16:00 London Cross-Asset Noise

Primary source: CME Bitcoin futures spec https://www.cmegroup.com/markets/cryptocurrencies/bitcoin/bitcoin.contractSpecs.html (verified: Globex 24/7 except Sat 02:00-04:00 CT and Mon-Fri 16:00-16:02 CT; termination 16:00 London last Friday; TAS/BTIC; tick $5=25)

Mechanism: Final settlement uses the 16:00 London reference on last Friday; expiry flows may jitter correlations.

Features: expiry-day flag; 15:30-16:30 London returns vs equities.

Target: Noise mask.

Falsify-if: No difference.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W84X-E22 — Spot-BTC ETF vs CME Futures Dislocation

Primary source: CME Bitcoin futures spec https://www.cmegroup.com/markets/cryptocurrencies/bitcoin/bitcoin.contractSpecs.html (verified: Globex 24/7 except Sat 02:00-04:00 CT and Mon-Fri 16:00-16:02 CT; termination 16:00 London last Friday; TAS/BTIC; tick $5=25) + SEC Rule 17 CFR 270.6c-11 (ETF rule; adopting Release 33-10695) via law-firm summaries (search-verified: daily holdings, prior-day NAV/premium-discount, 30-day median bid-ask, >2% for >7 days disclosure)

Mechanism: Spot ETF trades only US cash hours; futures trade nearly 24/7; basis plus ETF premium/discount shows demand pressure at cash open.

Features: ETF price - spot-implied; futures basis; open gap.

Target: Open convergence trade/avoid.

Falsify-if: Dislocation z has no predictive reversion.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W84X-E23 — SPY/QQQ vs ES/NQ Fair-Value Dislocation

Primary source: Hasbrouck (2003) J. Finance 58(6):2375-2400 'Intraday Price Formation in U.S. Equity Index Markets' (search-verified: most price discovery in E-mini; SPY smaller role; index ETFs weaker)

Mechanism: Futures lead price discovery; ETF dislocations vs fair value (carry, dividends) mean revert once arbitrage capacity returns; useful as a state of arbitrage capacity.

Features: fair-value gap in ticks; persistence; volume.

Target: Capacity gate.

Falsify-if: Gap persistence unrelated to capacity proxies.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W84X-E24 — Prior-Day ETF Premium/Discount Disclosure as Slow Prior

Primary source: SEC Rule 17 CFR 270.6c-11 (ETF rule; adopting Release 33-10695) via law-firm summaries (search-verified: daily holdings, prior-day NAV/premium-discount, 30-day median bid-ask, >2% for >7 days disclosure)

Mechanism: Rule requires prior-day NAV/premium-discount disclosure and flags >2% for >7 days; persistent dislocation indicates arbitrage breakdown.

Features: disclosed premium series; days above 2%.

Target: Slow stress prior.

Falsify-if: No relation with next-week vol.

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B

## W84X-E25 — Bond ETF vs Treasury Futures Dislocation

Primary source: SEC Rule 17 CFR 270.6c-11 (ETF rule; adopting Release 33-10695) via law-firm summaries (search-verified: daily holdings, prior-day NAV/premium-discount, 30-day median bid-ask, >2% for >7 days disclosure); ZN/ZB CME spec PP

Mechanism: Bond ETFs repriced through cash market can lag/lead futures in stress; the gap is a funding stress marker.

Features: IEF/TLT price vs ZN/ZB implied; gap z.

Target: Stress gate.

Falsify-if: Gap not related to subsequent vol.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W84X-E26 — High-Yield ETF Lead Over Equity in Stress

Primary source: HYG vs NQ (product docs PP; lead-lag literature PP)

Mechanism: Credit proxy ETFs may adjust before equity futures in credit-driven stress.

Features: lagged cross-corr HYG->NQ.

Target: Early warning.

Falsify-if: No lead.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W84X-E27 — Sector ETF Dependence on S&P ETF Price Discovery

Primary source: Hasbrouck (2003) J. Finance 58(6):2375-2400 'Intraday Price Formation in U.S. Equity Index Markets' (search-verified: most price discovery in E-mini; SPY smaller role; index ETFs weaker) (S&P ETF contributes markedly to sector ETF discovery)

Mechanism: Sector ETFs follow broad ETFs; sector residual signal is stale information, not new.

Features: sector minus beta*ES residual lag.

Target: Stale-quote avoidance.

Falsify-if: No lag.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W84X-E28 — Cash-Close Handoff 16:00 ET Cross-Asset State

Primary source: HA; NQ spec page returned 404 (PP)

Mechanism: Cash equity ends at 16:00 ET while futures continue; cross-asset links shift to after-hours liquidity.

Features: corr before/after 16:00; spread; ZN state.

Target: Gate.

Falsify-if: No state change.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W84X-E29 — Treasury Curve 15:30 Input vs 16:00 Equity Close Timing

Primary source: US Treasury interest-rate statistics https://home.treasury.gov/policy-issues/financing-the-government/interest-rate-statistics (verified: curve inputs are NY Fed indicative bids at about 15:30 ET)

Mechanism: Official daily yields use indicative bids at about 15:30 ET, so the last 30 minutes of rates/equity co-movement is absent from daily data.

Features: yield change after 15:30 (futures-implied) vs equity close-to-open.

Target: Overnight prior correction.

Falsify-if: Post-15:30 move does not improve overnight forecast.

Horizon: DAILY

Availability: PUBLIC_BATCH + PAID_REALTIME

Priority: B+

## W84X-E30 — DFII10 Availability-Lag Guard

Primary source: FRED DFII10 https://fred.stlouisfed.org/series/DFII10 (verified: daily 10y TIPS constant-maturity yield from Fed H.15; page last updated 9 Oct 2026 15:16 CDT with last observation 8 Oct 2026, i.e. one business day lag)

Mechanism: Public series stamped t are visible on t+1 evening; features using t at t cause look-ahead.

Features: availability_time = last_updated; enforce embargo.

Target: Leakage control (methodological edge).

Falsify-if: Series available same-day (then relax guard).

Horizon: DAILY

Availability: PUBLIC_DELAYED

Priority: A

## W84X-E31 — Gold-Dollar Beta Session Switch

Primary source: ICE US Dollar Index methodology (direct URL returned 404; weights unverified) PROVENANCE_PENDING; Fed H.10 https://www.federalreserve.gov/releases/h10/default.htm (verified: bilateral rates and dollar indexes released Mondays 16:15 for prior business week)

Mechanism: Dollar-gold relation differs in Asia/London/NY because participants and benchmark fixes differ.

Features: betas by session; stability.

Target: Session-conditioned parameters.

Falsify-if: Betas equal.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W84X-E32 — Gold-Equity Sign by Drawdown Depth

Primary source: Baur & Lucey (2010) 'Is gold a hedge or a safe haven?' (not fetched) PROVENANCE_PENDING

Mechanism: Gold hedges mild equity declines but can fall in liquidity crunches when everything is sold.

Features: rolling corr(GC,NQ) split by NQ intraday drawdown buckets.

Target: Gold hedge reliability.

Falsify-if: Corr identical across drawdown buckets.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W84X-E33 — Gold-NQ Intraday Beta State Machine (Extends W6N)

Primary source: Existing W6N NQ/Gold file; vault-internal

Mechanism: W6N catalogs NQ-gold physical/fundamental links; this adds a stateful beta classifier (decoupled/hedge/co-liquidation).

Features: 3-state HMM on (corr, beta, vol ratio).

Target: State label.

Falsify-if: HMM states not distinguishable from 1 state (BIC).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W84X-E34 — Oil-Equity Correlation Sign as Shock Identifier

Primary source: CME CL (verified)

Mechanism: Oil up with equities up implies demand shock; oil up with equities down implies supply shock.

Features: sign(corr(CL,NQ)) on 15-min windows; matched to EIA/OPEC event flags.

Target: Shock type label.

Falsify-if: Label does not predict next-hour equity follow-through.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W84X-E35 — MOVE-VIX Joint Stress Ratio

Primary source: ICE BofA MOVE index (licensed; PP)

Mechanism: Rates vol versus equity vol ratio shows whether stress is rates-led.

Features: MOVE/VIX ratio z.

Target: Stress source label.

Falsify-if: Ratio uninformative.

Horizon: DAILY

Availability: LICENSED_REALTIME [PP]

Priority: B

## W84X-E36 — Cross-Asset Correlation Surprise Gate

Primary source: Standard (no primary)

Mechanism: When realized 30-min correlation departs from 60-day baseline, hedges and spread models mis-size.

Features: |C_30m - C_60d| in Frobenius norm; threshold k.

Target: Size multiplier.

Falsify-if: Gate does not reduce drawdown.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W84X-E37 — Event-Type Cross-Asset Fingerprint Library

Primary source: Fed FOMC calendar https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm (verified: 27-28 Oct and 8-9 Dec 2026; 2027 dates listed; minutes three weeks after decision; statement time not on page - 14:00 ET PP); EIA schedules (W76Q-D01)

Mechanism: Each release type leaves a characteristic correlation-matrix change; a library classifies live reactions.

Features: delta-corr matrix per event type; cosine similarity.

Target: Live event classification.

Falsify-if: Fingerprints not stable across years.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED + PAID_REALTIME

Priority: B+

## W84X-E38 — Treasury Auction Tail Cross-Asset Response

Primary source: Treasury auction schedule/results (TreasuryDirect; time PP)

Mechanism: Weak auctions repricing duration, hitting NQ in rate-sensitive regimes.

Features: tail in bp; ZN/NQ response; time PP.

Target: Event gate.

Falsify-if: No response.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED [PP]

Priority: B

## W84X-E39 — Sunday Open Multi-Asset Consensus Gap

Primary source: CME Bitcoin futures spec https://www.cmegroup.com/markets/cryptocurrencies/bitcoin/bitcoin.contractSpecs.html (verified: Globex 24/7 except Sat 02:00-04:00 CT and Mon-Fri 16:00-16:02 CT; termination 16:00 London last Friday; TAS/BTIC; tick $5=25); CME GC/CL specs (verified Sunday opens)

Mechanism: Weekend information priced in BTC, 6J, 6E, GC, CL pre-NQ open; consensus vector predicts NQ gap direction.

Features: weighted weekend returns across five assets; NQ gap.

Target: Gap forecast.

Falsify-if: Consensus no better than BTC alone.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W84X-E40 — Asia Currency Lead to Europe-Open NQ

Primary source: CME 6J/6A (PP)

Mechanism: Asia session FX moves anticipate Europe/US equity open.

Features: FX return 00:00-03:00 ET vs NQ 03:00-09:30.

Target: Drift.

Falsify-if: No relation.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W84X-E41 — Real-Yield Up Gold Up Divergence Flag

Primary source: Erb & Harvey NBER w18706 https://www.nber.org/papers/w18706.pdf (abstract read via search; real-rate correlation figures only from secondary sources, PP); FRED DFII10 https://fred.stlouisfed.org/series/DFII10 (verified: daily 10y TIPS constant-maturity yield from Fed H.15; page last updated 9 Oct 2026 15:16 CDT with last observation 8 Oct 2026, i.e. one business day lag)

Mechanism: A rise in gold with rising real yields conflicts with the standard negative relation; marks fragility or a non-rate driver.

Features: sign(d gold)*sign(d real) over 5d; flag.

Target: Fragility prior.

Falsify-if: Flag does not predict reversal.

Horizon: SLOW_PRIOR

Availability: PUBLIC_DELAYED

Priority: B+

## W84X-E42 — Synchronized Direction Count (Herding Breadth)

Primary source: Standard (no primary)

Mechanism: Count of assets moving same macro-signed direction in 5 minutes is a herding measure.

Features: breadth of signed z>1 across 10 assets.

Target: Regime scalar.

Falsify-if: Breadth not related to vol.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W84X-E43 — Cross-Asset Dispersion Regime

Primary source: Standard

Mechanism: Low cross-sectional dispersion of normalized returns indicates macro-driven tape.

Features: std over assets of z-return per 5 min.

Target: Regime.

Falsify-if: No relation with correlations.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W84X-E44 — Net Lead Direction Stability (Transfer Entropy)

Primary source: Schreiber transfer entropy (not fetched) PROVENANCE_PENDING

Mechanism: Rolling directed information flow between ZN, NQ, GC, 6E indicates who leads now.

Features: rolling TE matrices; net-out minus in.

Target: Lead identity.

Falsify-if: TE directions random relative to shuffled series.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W84X-E45 — Hedge-Ratio Instability CUSUM

Primary source: Standard

Mechanism: Rolling beta of NQ on ZN/6E drifts; CUSUM detects the break.

Features: CUSUM of residuals; ratio change.

Target: Hedge reset trigger.

Falsify-if: CUSUM triggers not followed by changed hedge efficacy.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W84X-E46 — Residual Momentum After Rate and Dollar Factors

Primary source: Standard

Mechanism: NQ residual after removing ZN/6E betas contains idiosyncratic equity flow that persists briefly.

Features: residual cumulative 15m; continuation.

Target: Entry confirmation.

Falsify-if: Residual continuation zero.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W84X-E47 — Overnight Information Partition for NQ

Primary source: CME Bitcoin futures spec https://www.cmegroup.com/markets/cryptocurrencies/bitcoin/bitcoin.contractSpecs.html (verified: Globex 24/7 except Sat 02:00-04:00 CT and Mon-Fri 16:00-16:02 CT; termination 16:00 London last Friday; TAS/BTIC; tick $5=25)

Mechanism: Overnight NQ moves partition into rate, dollar, crypto and unexplained parts; the unexplained part is more likely to mean revert at RTH open.

Features: regress overnight NQ on ZN, 6E, BTC; residual.

Target: Open fade.

Falsify-if: Residual unrelated to open reversal.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W84X-E48 — Event-Clock Collision Map

Primary source: EIA schedule (W76Q-D01), Fed FOMC calendar https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm (verified: 27-28 Oct and 8-9 Dec 2026; 2027 dates listed; minutes three weeks after decision; statement time not on page - 14:00 ET PP)

Mechanism: Overlapping events at the same minute (e.g. EIA 10:30 with other releases) contaminate single-event inference; a map lists collisions.

Features: minute-level event set; collision flag.

Target: Mask.

Falsify-if: No contamination.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W84X-E49 — Tail Co-Exceedance Across NQ, ZN, GC, BTC

Primary source: Standard copula/EVT

Mechanism: Joint tail probability differs from independence; matters for portfolio loss gating.

Features: empirical co-exceedance at 1% tails.

Target: Tail gate.

Falsify-if: Co-exceedance equals independence.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B

## W84X-E50 — Correlation Regime Hysteresis Controller

Primary source: Standard

Mechanism: State flips at fixed thresholds flip-flop; hysteresis with minimum dwell time reduces false switching.

Features: enter/exit thresholds, dwell minutes.

Target: Regime stability.

Falsify-if: Controller gives no fewer false flips.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W84X-E51 — Rates-Dollar-Equity Collision at 08:30 ET Releases

Primary source: Macro release calendars (BLS/BEA; PP)

Mechanism: Major releases at 08:30 ET trigger joint repricing before the cash open; cross-asset beta changes for NQ globex session.

Features: 08:30 windows; matrix.

Target: Pre-open gate.

Falsify-if: No beta change.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED [PP]

Priority: B

## W84X-E52 — Weekly H.10 Monday Vintage Gap

Primary source: Fed H.10 https://www.federalreserve.gov/releases/h10/default.htm (verified: bilateral rates and dollar indexes released Mondays 16:15 for prior business week)

Mechanism: H.10 posts the prior week Monday 16:15, so dollar indexes in daily files are retrospective; intraday models must not rely on them.

Features: vintage check; revision log.

Target: Leakage control.

Falsify-if: Daily files available earlier (then relax).

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B

## W84X-E53 — Gold-ETF vs Dollar Reaction Divergence

Primary source: SEC Rule 17 CFR 270.6c-11 (ETF rule; adopting Release 33-10695) via law-firm summaries (search-verified: daily holdings, prior-day NAV/premium-discount, 30-day median bid-ask, >2% for >7 days disclosure); SSGA GLD (PP)

Mechanism: Dollar shocks that ETF shares absorb at cash hours vs futures during off-hours create timing gaps.

Features: GLD vs GC dollar beta by hour.

Target: Timing gap.

Falsify-if: No gap.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W84X-E54 — Funding Stress Cross-Check via Bond ETF Premium

Primary source: SEC rule (verified via summaries)

Mechanism: Premium/discount spikes in rates ETFs concurrent with dollar strength flag funding stress.

Features: premium z, 6E z, ZN.

Target: Stress state.

Falsify-if: No relation.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W84X-E55 — Cross-Asset Calendar of Holiday Asymmetry

Primary source: CME holiday calendars (expiration calendar tool linked on CL page, verified link)

Mechanism: Holiday closure asymmetry (US closed, London open) leaves gold, FX and rates with isolated liquidity.

Features: holiday flag; spreads; beta.

Target: Gate.

Falsify-if: No difference.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B

## W84X-E56 — Dollar-Gold-NQ Triple Co-Movement Exhaustion

Primary source: Standard

Mechanism: When all three move in a macro-consistent direction past k sigma, a snapback occurs on liquidity exhaustion.

Features: composite z; reversal probability.

Target: Reversal.

Falsify-if: No reversal edge.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## Final architecture edge (Truth Ladder)

Truth Ladder for W84X: L0 primary-source timing objects (H.10, FRED/H.15, Treasury, FOMC, CME specs, SEC ETF rule) -> L1 vintage-safe data with availability timestamps -> L2 rolling correlation/beta states with hysteresis (E50) -> L3 event fingerprints and lead-lag tests with placebo shuffles -> L4 composite regime scalar (E12) driving sizing/gating, never direction -> L5 intermediate-outcome promotion gate. PROVENANCE_PENDING dependencies stay at L1.

## Highest-priority W84X tests

1. W84X-E01 Rate-Beta of Gold on ZN Returns by Stock-Bond Sign Regime
2. W84X-E04 Stock-Bond Correlation Sign as NQ Hedge and Gate
3. W84X-E06 FOMC Day Cross-Asset Correlation Spike Window
4. W84X-E12 Risk-On/Off Composite Definition
5. W84X-E19 Weekend BTC Move as Sunday NQ Gap Predictor
6. W84X-E23 SPY/QQQ vs ES/NQ Fair-Value Dislocation
7. W84X-E39 Sunday Open Multi-Asset Consensus Gap
8. W84X-E11 Dollar-Yield-Gold Triangle Residual
9. W84X-E30 DFII10 Availability-Lag Guard
10. W84X-E50 Correlation Regime Hysteresis Controller
