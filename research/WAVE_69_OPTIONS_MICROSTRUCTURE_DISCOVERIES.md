# Wave 69O — Options Microstructure & Dealer-Greeks State

Namespace: **W69O**

Thesis: dealer option hedging changes the market's response function, but dealer positions are unobserved. This wave treats gamma, vanna and charm maps as uncertain inferred states built from OPRA quotes/prints, exchange origin data and OCC open interest, and focuses on (a) quote-driven vs trade-driven sign inference, (b) pitfalls in gamma/vanna/charm estimation, (c) 0DTE and expiry mechanics, (d) strike clustering and pin risk, (e) skew/term-structure dynamics, and (f) index vs single-name flow. The target is a conditional regime state with explicit uncertainty, not a directional call. Verified context: Cboe reports 0DTE at a record 62.4% of SPX volume in Aug 2025 with ~53% estimated retail; Dim-Eraker-Vilkov (SSRN) report no net amplification from 0DTE gamma while Baltussen et al. (JFE 2021) link gamma hedging to last-30-minute momentum, so the sign is genuinely ambiguous.

Boundary: EDGE_ATLAS E02 (0DTE Gamma Phase Field), E03 (MHPA) and E110 own the base concept; this wave extends them with estimation pitfalls, uncertainty gating and microstructure inference. W26R owns SOQ/expiry/OCC exercise-by-exception mechanics (E26-E31); W27V owns halts/LULD; W62C owns CFTC positioning; W77O owns VIX/VX/vol-control mechanics and is cross-referenced here only for joint states.

All candidates are research hypotheses only. Claude owns later implementation. No profitability is claimed; every edge is subject to the intermediate-outcome promotion gate (timing-safe data, purged walk-forward, multiple-testing control, named placebo).

## W69O-E01 — Signed-Volume Confidence Weighting (Quote-Driven Option Trade Sign)

Primary source: OPRA last-sale + NBBO quote messages (OPRA plan output specification; exact spec status PROVENANCE_PENDING)

Mechanism / Features: Option trades are signed by comparing print price to the prevailing NBBO at trade time; Lee-Ready tick tests are unreliable in options because prints can sit inside the spread or follow stale quotes. Feature: s_i = clip((p - mid)/(half_spread), -1, 1) with a quote-age penalty w = exp(-age_ms/tau); signed_vol = sum(w*s*size). Parameters: tau, quote lag offset.

Target: Next 1/5/15-min ES signed-flow imbalance and realized-move sign.

Falsify-if: Falsify if confidence-weighted signed volume has no incremental out-of-sample R2 over naive midpoint sign after quote-lag placebo (shift quotes by random +/-N ms).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W69O-E02 — Complex-Order and Multi-Leg Contamination Filter

Primary source: OPRA/Cboe options trade-condition codes (Cboe Titanium U.S. Options feed spec lists codes such as I Electronic, O Opening, S ISO, K Cabinet; OPRA-native table PROVENANCE_PENDING)

Mechanism / Features: Spread, combo, auction and cabinet prints carry no directional delta; treating each leg as outright flow inflates apparent gamma/delta. Feature: contamination_ratio = notional of non-outright conditions / total notional per strike-minute; compute delta flow only from outright prints, keep a separate spread-leg bucket.

Target: Gamma-flow estimate error vs reconciled next-day open-close.

Falsify-if: Falsify if filtered and unfiltered signed delta give statistically indistinguishable ES predictions after controlling for volume.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E03 — Open-Close Origin Net Customer Flow (Cboe-Only)

Primary source: Cboe Open-Close Volume Summary (end-of-day and 10-minute intraday snapshots via Cboe LiveVol DataShop; origin codes customer / professional customer / broker-dealer / market maker; exact product spec PROVENANCE_PENDING beyond search summary)

Mechanism / Features: Origin-coded open/close volume is the closest public approximation of who initiated positions. Feature: net_customer_open_gamma = sum over strikes of (customer_buy_open - customer_sell_open)*gamma*100*S; dealer proxy = minus customer. Sign limit: customer is not necessarily the end-risk-holder and covers Cboe only.

Target: Sign of next-session ES realized-vol residual versus a flat-sign GEX baseline.

Falsify-if: Falsify if origin-coded gamma does not beat static OI-based GEX at any horizon or if the sign flips unstably across years.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: S-

## W69O-E04 — Customer Size-Bucket Retail/Institution Gamma Split

Primary source: Cboe Open-Close size buckets (<100, 100-199, >199 contracts for customer and professional customer; per Cboe product description, PROVENANCE_PENDING)

Mechanism / Features: Small-lot customer flow (retail-like) and large-lot flow (institutional-like) hedge and decay differently: retail is often long short-dated convexity, institutions often sell premium. Feature: gamma_small, gamma_large, and their signed ratio. Cboe reports roughly 53% of Aug-2025 SPX 0DTE volume as retail (classification method not disclosed).

Target: Conditional intraday autocorrelation sign by bucket-dominance.

Falsify-if: Falsify if bucket-split gamma adds nothing over total customer gamma, or if the split proxies only for time-of-day volume.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: A

## W69O-E05 — Open-Interest Staleness for 0DTE (Flow-Integrated Gamma)

Primary source: OCC daily volume and open interest report (published after close, so same-day OI for 0DTE is effectively zero at the open); Cboe SPXW daily expirations (Cboe press releases 2022-04-13, 2022-09-19)

Mechanism / Features: OI-based GEX maps cannot see positions opened today; 0DTE positions exist only through intraday flow. Feature: G_0dte(t) = sum of signed-volume * gamma(strike, T_remaining) accumulated since the open, rather than OI * gamma. Compare against OI-GEX that includes only 1DTE+.

Target: Improvement of intraday variance forecast after 10:30 ET.

Falsify-if: Falsify if OI-only GEX forecasts intraday variance equally well as flow-integrated 0DTE gamma, i.e. incremental coefficient is zero with HAC errors.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S

## W69O-E06 — Sign-Convention Ensemble Disagreement State

Primary source: Dealer-position conventions in practitioner GEX (calls short / puts long by dealer, all-customer-long, flow-signed) vs Garleanu-Pedersen-Poteshman Demand-Based Option Pricing, RFS 2009 (end users net long index options, esp. OTM puts)

Mechanism / Features: The dealer sign is not observed. Run at least three sign conventions and compute net gamma under each; the disagreement D = max - min across conventions is an uncertainty state. Gate: trade gamma-conditional logic only when conventions agree on sign.

Target: Hit rate of gamma-regime-conditioned strategies split by D tercile.

Falsify-if: Falsify if performance is the same in high-D and low-D terciles (then disagreement is not informative and gating adds only turnover).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W69O-E07 — Gamma Estimate Surface-Model Sensitivity (Sticky Strike vs Sticky Delta)

Primary source: Black-Scholes gamma definition; per-strike IV from OPRA quotes

Mechanism / Features: Gamma computed with flat IV, per-strike IV, or sticky-delta shifted IV differ materially for short-dated wings. Feature: spread of net gamma across three IV treatments, plus gamma-flip strike under each.

Target: Stability of flip level over 5 minutes.

Falsify-if: Falsify if all three treatments produce flip levels within one tick-size bucket nearly always (then complexity is unnecessary).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W69O-E08 — Forward and Carry Error Under 0DTE ATM

Primary source: Put-call parity on SPX/SPXW quotes (implied forward)

Mechanism / Features: A wrong forward shifts moneyness and so the gamma peak. Feature: F_implied(strike) from nearest-ATM call-put pairs; gamma re-centered on F_implied instead of spot.

Target: Peak-gamma location error versus realized pin region.

Falsify-if: Falsify if re-centering does not change peak strike more than a stated tolerance.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W69O-E09 — Time-Remaining Clock and Gamma Singularity Floor

Primary source: Cboe SPXW PM settlement at 15:00 CT / 16:00 ET close (Cboe VIX methodology states 3:00 p.m. for PM-settled weeklys; time convention PROVENANCE_PENDING for SPXW itself)

Mechanism / Features: Gamma scales roughly as 1/sqrt(T); in the last 30 minutes ATM gamma diverges, so small errors in T and IV dominate. Feature: gamma computed with T floored at T_min and capped gamma; share of net gamma from strikes within 0.1 sigma of spot.

Target: Close-window realized variance per unit estimated gamma.

Falsify-if: Falsify if floor/cap choice changes no regime label and no trade conclusion.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E10 — Gamma-Flip Level Uncertainty Band

Primary source: Derived from gamma map | bootstrap over sign conventions and IV treatments

Mechanism / Features: The flip strike is a statistic with a distribution. Feature: flip_lo, flip_hi (10th/90th pct) and band width in expected-move units; if spot lies inside the band the regime label is AMBIGUOUS.

Target: Regime-label precision.

Falsify-if: Falsify if outcomes in AMBIGUOUS are no different from confident states.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W69O-E11 — Spot-to-Dominant-Strike Distance in Sigma Units

Primary source: Derived from intraday ATM IV and strike-level gamma/volume

Mechanism / Features: Pin-like attraction should depend on distance relative to the remaining expected move. Feature: z = (K_dom - S)/(S*IV_atm*sqrt(T_rem)); K_dom = argmax gamma-weighted open interest + flow.

Target: Probability close within 0.1% of K_dom as a function of z.

Falsify-if: Falsify if close-to-strike distance distribution is indistinguishable from randomly chosen round strikes (negative control).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W69O-E12 — Strike-Clustering Concentration Index

Primary source: OCC OI/volume by strike; round-number multiples (25/50/100 index points)

Mechanism / Features: Positions cluster at round strikes; concentration makes the gamma map lumpy and walls sharper. Feature: HHI of gamma notional across strikes and share at multiples of 50/100.

Target: Intraday rejection/penetration events at top strike.

Falsify-if: Falsify if HHI does not predict rejection frequency beyond total gamma.

Horizon: INTRADAY

Availability: PUBLIC_BATCH

Priority: B+

## W69O-E13 — SPXW Cash-Settled Pin Test (Index)

Primary source: Ni, Pearson, Poteshman (2005) 'Stock price clustering on option expiration dates', JFE (stock pinning; index extension untested)

Mechanism / Features: SPX settles in cash with no share delivery, so the single-stock pin channel (delivery/hedge unwind) may not transfer. Test: P(|close - K| < eps) vs uniform baseline on SPXW and SPX expiries, split by estimated net gamma sign.

Target: Excess pin probability.

Falsify-if: Falsify if excess pin probability is zero after round-number baseline; downgrade to non-effect.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A

## W69O-E14 — SPY/QQQ Physical-Settled Early-Exercise Pin Risk

Primary source: OCC Rule 805 exercise-by-exception (current threshold PROVENANCE_PENDING; SEC releases 34-54514 and 34-57163 describe past $0.01 changes for equity options); SPY/QQQ American-style ETF options

Mechanism / Features: ETF options deliver shares and can be exercised early near ex-dividend; after-close exercise decisions create after-hours assignment risk. Feature: ITM-by-0.01 OI near close at strikes within 0.1%; dividend proximity.

Target: Next-open gap beyond futures move.

Falsify-if: Falsify if post-close SPY gap residual unrelated to near-strike OI.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B+

## W69O-E15 — Monthly AM-Settled SPX Expiry Open-Auction Gamma Release

Primary source: Cboe VIX methodology notes standard SPX options settle AM (8:30 CT) and SPXW PM; CME/Cboe SOQ procedures (SOQ spec unverified)

Mechanism / Features: On third Fridays standard SPX monthly expirations settle from opening prints, so their gamma disappears before the cash open while SPXW gamma remains. Feature: share of gamma in AM-settled series, and open-print dispersion.

Target: Opening-30-min realized variance on opex vs matched non-opex Fridays.

Falsify-if: Falsify if matched-day difference is zero after controlling for VIX and overnight gap.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: A

## W69O-E16 — Expiring-Gamma Roll-Off Share

Primary source: OCC OI by expiry; Cboe expiration calendar

Mechanism / Features: Fraction of total gamma notional expiring today and this week is a measure of next-session regime change. Feature: roll_off_today = gamma(exp=today)/gamma(total); roll_off_week.

Target: Next-day RV change vs this share.

Falsify-if: Falsify if share does not predict RV change after VIX level control.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: A

## W69O-E17 — Post-Expiry Gamma Vacuum

Primary source: Derived from OCC OI changes | calendar

Mechanism / Features: After large expiries the dealer book is short of near-dated gamma until new flow arrives; early-session variance can rise. Feature: change in total OI-implied gamma day over day and the first-hour variance ratio.

Target: First-hour RV / trailing average.

Falsify-if: Falsify if post-large-expiry first-hour variance equals matched days.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B+

## W69O-E18 — Charm-Driven Scheduled Delta Drift

Primary source: Black-Scholes charm; Baltussen, Da, Lammers, Martens 'Hedging Demand and Market Intraday Momentum', JFE 142 (2021) 377-403 (gamma hedging demand and last-30-minute momentum)

Mechanism / Features: With no new trades, passage of time alone shifts deltas; charm-implied hedge flow = sum(OI_signed*charm*dt). Sign depends on position sign (ambiguous). Feature: charm_flow(t, t+dt) over the rest of day under each sign convention.

Target: Direction of ES drift in last 60 minutes.

Falsify-if: Falsify if charm_flow has no relationship to late-session drift after removing gamma term.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E19 — Vanna Exposure Under Implied-Vol Moves

Primary source: Black-Scholes vanna; options-implied surface

Mechanism / Features: When IV falls (e.g. after an event), dealer delta changes proportional to vanna, forcing futures hedges; sign depends on long/short. Feature: dDelta = vanna * dIV aggregated; condition on IV change sign and event timing.

Target: ES return during IV-collapse window.

Falsify-if: Falsify if vanna-implied sign has hit rate not above 50% with block bootstrap.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E20 — Event Vol-Crush Window (Scheduled Macro)

Primary source: Macro release calendar (BLS/FOMC calendars) + 0DTE/1DTE IV term structure

Mechanism / Features: Around scheduled releases, 0DTE IV carries event variance; after release IV collapses mechanically. Feature: IV_0dte / IV_1dte kink before event; post-event change in IV.

Target: Realized-move vs implied-move ratio and subsequent drift.

Falsify-if: Falsify if post-event drift is unrelated to the kink magnitude vs non-event placebo days.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W69O-E21 — Implied Overnight/Intraday Variance Split from 0DTE-1DTE Term

Primary source: Same-day (0DTE) and next-day (1DTE) ATM implied variances

Mechanism / Features: Forward implied variance between today's close and tomorrow's close equals IV1^2*T1 - IV0^2*T0. Feature: overnight_implied_var, and its ratio to realized overnight ES move.

Target: Overnight gap magnitude.

Falsify-if: Falsify if implied forward variance forecast does not beat trailing realized overnight variance.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A

## W69O-E22 — Remaining-Vol Budget (Straddle vs Realized-So-Far)

Primary source: ATM straddle price (0DTE) from OPRA quotes

Mechanism / Features: Compare straddle-implied total expected move at open vs realized range so far: budget = E0 - realized_range(t); depletion fraction. Low remaining budget with high realized implies tight afternoon (mean-reversion); inverse implies tail risk repricing.

Target: Remaining-session range.

Falsify-if: Falsify if budget fraction fails to predict remaining range after HAR controls.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W69O-E23 — Intraday Variance Risk Premium (Implied vs Realized, Same Window)

Primary source: 0DTE ATM IV vs 5-min realized variance; Dim, Eraker, Vilkov '0DTEs: Trading, Gamma Risk and Volatility Propagation' (SSRN; reported largest VRP in 0DTE, secondary summary)

Mechanism / Features: Sellers of 0DTE earn premium on average; the premium compresses when realized shocks occur. Feature: IV_0dte^2*T - RV_so_far - forecast_RV_rest.

Target: Next-hour premium sign.

Falsify-if: Falsify if intraday VRP carries no information on future RV direction beyond level of IV.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E24 — 25-Delta Risk Reversal Spot-Skew Beta (0DTE)

Primary source: Options quotes by delta

Mechanism / Features: RR25 = IV_call25 - IV_put25 co-moves with spot; the beta of RR to spot return identifies sticky-delta vs sticky-strike behavior and dealer vega stress. Feature: rolling beta of dRR on dS/S (5-min).

Target: Next-hour sign of spot-vol correlation.

Falsify-if: Falsify if beta instability does not lead realized spot-vol correlation changes.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E25 — Put-Skew Steepening vs Futures Lead-Lag

Primary source: OTM put IV vs ATM IV; ES order flow

Mechanism / Features: Put skew can steepen before cash index declines if hedgers lead. Feature: d(IV_put10 - IV_atm) leading ES return, lag search in seconds to minutes.

Target: ES 1-5 min return.

Falsify-if: Falsify if lead-lag coefficient is zero after bid-ask bounce correction.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E26 — Call-Wing Lottery Demand Regime

Primary source: Cboe 0DTE retail resurgence note (SPX 0DTE 61% share, retail ~53% Aug 2025) and Open-Close small-lot calls

Mechanism / Features: Rising small-lot OTM call buying in 0DTE can invert skew and supply dealers with short upside convexity. Feature: small-lot OTM call share; call-skew inversion.

Target: Upside tail realized moves.

Falsify-if: Falsify if lottery-call share has no relation to upper-tail frequency vs placebo.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: B+

## W69O-E27 — 0DTE Share Regime Prior

Primary source: Cboe Insights 'SPX 0DTE Options Jump to Record 62% Share in August' (verified: 62.4% share, ~2.4M ADV, ~53% retail estimate)

Mechanism / Features: Slow prior: when 0DTE share of SPX volume is high, intraday gamma becomes a larger part of price dynamics, but Dim-Eraker-Vilkov report no net amplification; ambiguous sign. Feature: rolling 20d 0DTE share and its change.

Target: Cross-sectional days in high-share vs low-share months; conditional intraday autocorrelation.

Falsify-if: Falsify if effect on conditional autocorrelation is zero after trend control; keep as prior only.

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B+

## W69O-E28 — Index vs Single-Name Flow Wedge

Primary source: OCC volume by product class; Cboe index vs equity option statistics

Mechanism / Features: Index options hedge with futures; single-name options hedge with stocks and impact NQ via constituent weights. Feature: ratio of index-option gamma to constituent-option gamma weighted by NDX/SPX weights.

Target: NQ vs ES relative variance.

Falsify-if: Falsify if the wedge does not predict NQ-ES spread variability.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B+

## W69O-E29 — Megacap Single-Name Gamma Aggregated into NQ

Primary source: Single-name OPRA quotes for top constituents (index weights from provider)

Mechanism / Features: Sum_i w_i*Gamma_i*S_i^2 in top 10 NDX names, converted to NQ-equivalent delta per 1% move. Earnings dates raise name-specific gamma.

Target: NQ residual after ES.

Falsify-if: Falsify if aggregated megacap gamma adds no information beyond QQQ/NDX gamma.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E30 — SPY/QQQ Option Gamma into Futures Mapping

Primary source: SPY/QQQ OPRA options | ES/NQ beta mapping

Mechanism / Features: ETF option dealers hedge with ETF or futures; need beta-adjusted conversion. Feature: gamma_SPY*(ES notional factor), gamma_QQQ for NQ; sum with SPX gamma.

Target: ES/NQ conditional variance.

Falsify-if: Falsify if adding ETF gamma to index gamma does not improve fit vs index-only (negative control).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E31 — NDX/NDXP vs QQQ Gamma Cross-Check

Primary source: NDX/NDXP options (listing and expiries PROVENANCE_PENDING) vs QQQ

Mechanism / Features: Cross-check two instruments for same exposure; disagreement indicates classification issues.

Target: Same as above.

Falsify-if: Falsify if disagreement is noise.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W69O-E32 — Mechanical Hedge Absorption Ratio (Extends EDGE_ATLAS E03 MHPA)

Primary source: EDGE_ATLAS E03 definition; CME ES order book depth (feed spec PROVENANCE_PENDING)

Mechanism / Features: Increment over E03: use 1% move hedge demand from the gamma ensemble and top-of-book plus replenishment-adjusted depth; ratio R = |dDelta_per_1pct| / depth_5levels.

Target: Move-size conditional on R tercile.

Falsify-if: Falsify if R tercile no better than raw gamma size tercile.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W69O-E33 — Gamma-Sign Conditional Return Autocorrelation

Primary source: Baltussen et al. JFE 2021; estimated net gamma sign

Mechanism / Features: Net short dealer gamma implies pro-cyclical hedging, so 5-min returns positively autocorrelate; long gamma implies negative. Feature: rolling AC1 conditional on sign, with disagreement gate.

Target: 5-min return sign persistence.

Falsify-if: Falsify if AC1 difference by sign is zero on out-of-sample and no better than VIX-level split.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S

## W69O-E34 — Last-30-Minute Momentum Amplification by Gamma Sign

Primary source: Baltussen et al. JFE 2021 (last 30 min returns predicted by rest-of-day return)

Mechanism / Features: Increment: test whether the effect strengthens on estimated net-short-gamma days and weakens on net-long days; day-level interaction.

Target: ES last-30-min return.

Falsify-if: Falsify if interaction coefficient zero.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W69O-E35 — Gamma-Wall Breakout Hazard

Primary source: Strike-level gamma map

Mechanism / Features: Break through a large gamma strike converts attraction to hedge flow. Feature: time-in-band, volume at wall, distance after penetration.

Target: Continuation probability after penetration.

Falsify-if: Falsify if penetration hazard equals random price-level hazard (control with non-wall round numbers).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E36 — Gamma-Weighted Centroid Reversion

Primary source: Gamma map | centroid c = sum(K*|G_K|)/sum(|G_K|)

Mechanism / Features: Distance of spot from centroid decays under long-gamma; opposite under short. Feature: (S - c)/expected move.

Target: Half-life of distance.

Falsify-if: Falsify if half-life independent of gamma sign.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W69O-E37 — Option Quote Revision Intensity as Dealer Stress

Primary source: OPRA quote message counts per strike (OPRA output spec; PROVENANCE_PENDING)

Mechanism / Features: Market makers widen/withdraw before moves; quote revision rate up with spread widening in ATM series. Feature: msgs/sec z-score vs prior 20 days at same time.

Target: Subsequent ES realized variance.

Falsify-if: Falsify if quote-intensity adds nothing beyond ES own volatility and message-rate regime shifts (exchange outages).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W69O-E38 — 0DTE ATM Spread Width Liquidity Gate

Primary source: OPRA NBBO

Mechanism / Features: Width of ATM 0DTE spread relative to premium measures dealer risk appetite. Feature: spread/premium z-score.

Target: ES slippage in next 5 min.

Falsify-if: Falsify if no relationship to execution cost.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E39 — Zero-Bid Wing Exhaustion Count

Primary source: OPRA NBBO; Cboe VIX methodology (excludes strikes after two consecutive zero bids; verified)

Mechanism / Features: Count of OTM strikes with zero bid shrinks in stress as bids appear; or grows when wings are abandoned. Feature: N_zero_bid and VIX-eligible strike count, intraday.

Target: Tail moves in ES.

Falsify-if: Falsify if count does not add beyond VIX and skew.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W69O-E40 — Synthetic-Forward vs ES Basis Flow

Primary source: Put-call parity forward from ATM SPX/SPXW vs ES price adjusted for carry

Mechanism / Features: Synthetic positions in options create transient parity gaps; ES leads or lags. Feature: F_syn - F_ES_fair; z-score.

Target: ES 1-min return.

Falsify-if: Falsify if gap converges without return information (pure noise).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W69O-E41 — Day-Trade Round-Trip Share (Open-Close Reconciliation)

Primary source: Cboe Open-Close open/close flags vs next-day OCC OI

Mechanism / Features: Residual = flow-estimated OI change minus actual; round-trip share indicates how much gamma is transient. Feature: 1 - |OI_delta|/volume per strike.

Target: Persistence of gamma map.

Falsify-if: Falsify if share does not predict map decay.

Horizon: DAILY

Availability: LICENSED_REALTIME

Priority: B+

## W69O-E42 — Overnight Gamma Carry Prior for Next Open

Primary source: OCC OI after close, 1DTE+ book

Mechanism / Features: Positions persisting into the next session set opening gamma regime before 0DTE flow arrives. Feature: carry_gamma at 16:00 mapped to next-day open price.

Target: First-hour RV and AC1.

Falsify-if: Falsify if carry gamma has no effect on first hour after controlling for overnight gap.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: A-

## W69O-E43 — Holiday and Half-Day Option Clock Truncation

Primary source: Cboe holiday calendar / early-close schedule (rule specifics UNVERIFIED)

Mechanism / Features: Early closes shorten T and alter gamma clock; forcing T from default session length is wrong. Feature: schedule-aware T.

Target: Calibration error of expected move.

Falsify-if: Falsify if schedule-aware T leaves expected-move error unchanged.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B

## W69O-E44 — Globex/GTH Overnight Option Activity State

Primary source: Cboe Global Trading Hours for SPX options (existence and hours PROVENANCE_PENDING)

Mechanism / Features: Overnight option volume may reveal pre-open positioning. Feature: GTH volume share and skew change into open.

Target: Opening gap direction.

Falsify-if: Falsify if no relation after ES overnight move control.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W69O-E45 — Earnings-Day Single-Name Event Premium into NQ

Primary source: Earnings calendar; single-name straddle implied move

Mechanism / Features: Megacap event variance contributes to NQ variance by weight^2. Feature: sum(w_i^2*event_var_i).

Target: NQ post-event variance.

Falsify-if: Falsify if not better than dummy for earnings day.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W69O-E46 — Hedge Cadence Inference (Band vs Time-Based)

Primary source: ES tape signed flow after SPX option prints

Mechanism / Features: Dealers may hedge at delta bands or at intervals; autocorrelation of ES signed flow at multiples of interval reveals cadence. Feature: periodogram of ES signed volume after large option prints.

Target: Hedge timing for execution avoidance.

Falsify-if: Falsify if no periodic structure exceeds placebo.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W69O-E47 — Option-to-Futures Lead-Lag Latency Distribution

Primary source: Timestamped OPRA vs CME MDP 3.0 (spec status PROVENANCE_PENDING)

Mechanism / Features: Measure ES response after large option prints; informs execution gating windows. Feature: impulse response of ES mid to signed delta shock in ms.

Target: Optimal pause/aggressiveness windows.

Falsify-if: Falsify if response not distinguishable from random-timed prints.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E48 — Hedge-Flow Convexity (Quadratic Impact)

Primary source: Gamma-implied dDelta = G*dS

Mechanism / Features: Hedge demand scales with move size; large moves create disproportionate flow. Feature: Q = G*(dS)^2 relative to depth.

Target: Tail move frequency conditioned on Q.

Falsify-if: Falsify if tail frequency linear in |dS| only.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E49 — Volga/Vega-Gamma Mixed Hedging Pressure

Primary source: BS vega, vomma

Mechanism / Features: Dealers short wing convexity hold vega that grows as IV rises (vomma), forcing vega hedges. Feature: vomma exposure x dIV^2.

Target: Skew response magnitude.

Falsify-if: Falsify if vomma term adds nothing over delta/gamma.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W69O-E50 — Snapshot Cadence Information Loss

Primary source: Own pipeline ablation

Mechanism / Features: Test 1-sec vs 1-min vs 5-min gamma refresh; measure information decay.

Target: Predictive R2 vs cadence.

Falsify-if: Falsify if 5-min equals 1-sec, in which case save compute.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W69O-E51 — Unconditional Opex Calendar Placebo

Primary source: Calendar permutation

Mechanism / Features: Pseudo-expiry days matched on weekday, VIX, month; compare effects tied to expiry.

Target: Effect difference.

Falsify-if: Required control: falsify if any claimed expiry effect is reproduced on placebo days.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: A

## W69O-E52 — Gamma Regime Persistence Across Days

Primary source: Gamma ensemble history

Mechanism / Features: Autocorrelation of day-level regime label; hysteresis needed to prevent flicker. Feature: regime run lengths.

Target: Optimal smoothing window.

Falsify-if: Falsify if regime labels are white noise.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W69O-E53 — Gamma x VIX-Term-Structure Joint State

Primary source: Gamma ensemble x VIX/VX curve (W77O)

Mechanism / Features: Positive gamma with inverted VX is conflicted; classify joint states.

Target: Conditional variance.

Falsify-if: Falsify if joint state adds no information beyond each alone.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E54 — Gamma x Liquidity-Withdrawal Interaction

Primary source: Gamma ensemble x ES depth

Mechanism / Features: Short gamma with thin depth is the amplification case. Feature: product.

Target: Outsized-move frequency.

Falsify-if: Falsify if interaction is zero.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W69O-E55 — Gamma-Derived Stop-Cluster Map

Primary source: Gamma map walls and prior highs

Mechanism / Features: Where hedging flow flips sign stops cluster. Feature: wall proximity vs round-number stops.

Target: Stop-run frequency.

Falsify-if: Falsify if equal to round-number control.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W69O-E56 — Quantization of Dealer Capacity Using Open Interest Growth

Primary source: OCC OI trend

Mechanism / Features: Rapid OI growth may exceed dealer risk capacity, raising spreads. Feature: OI growth z-score and spread.

Target: Spread widening.

Falsify-if: Falsify if unrelated.

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B

## W69O-E57 — Index-Rebalance x Gamma Collision (links W26R)

Primary source: W26R quarterly events x gamma map

Mechanism / Features: On rebalance days gamma and forced close flows overlap. Feature: gamma state on W26R-E31 collision days.

Target: Close-window move.

Falsify-if: Falsify if rebalance effect is same across gamma states.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A-

## W69O-E58 — Placebo Gamma (Shuffled Strikes) Negative Control

Primary source: Shuffled-strike gamma maps

Mechanism / Features: Required negative control: shuffle strikes within day; any claimed strike-specific effect must vanish.

Target: n/a

Falsify-if: Falsify claims if shuffled maps reproduce results.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W69O-E59 — Dealer Model Cross-Validation with Customer-Flow Surveys (Public Only)

Primary source: Public aggregate statistics only (Cboe OI reports, OCC); no non-public identities

Mechanism / Features: Compare inferred dealer sign with published aggregate customer origin statistics to bound sign error.

Target: Sign accuracy bound.

Falsify-if: Falsify if sign agreement is at chance.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B

## W69O-E60 — Dealer Gamma Truth Ladder

Primary source: All of the above

Mechanism / Features: QUOTES/PRINTS -> CLEAN OUTRIGHT TRADES -> SIGNED FLOW (WITH CONFIDENCE) -> POSITION ESTIMATE (ENSEMBLE) -> GAMMA/VANNA/CHARM MAP + UNCERTAINTY -> HEDGE DEMAND vs FUTURES DEPTH -> REALIZED RESPONSE (REGIME-CONDITIONAL). Rule: higher rungs cannot be promoted without the lower rungs passing their own gates.

Target: Architecture.

Falsify-if: Falsify if lower rungs fail but final signal passes (indicates leakage).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S

## Highest-priority W69O tests

1. W69O-E01 Signed-Volume Confidence Weighting (Quote-Driven Option Trade Sign)
2. W69O-E05 Open-Interest Staleness for 0DTE (Flow-Integrated Gamma)
3. W69O-E06 Sign-Convention Ensemble Disagreement State
4. W69O-E10 Gamma-Flip Level Uncertainty Band
5. W69O-E33 Gamma-Sign Conditional Return Autocorrelation
6. W69O-E34 Last-30-Minute Momentum Amplification by Gamma Sign
7. W69O-E20 Event Vol-Crush Window (Scheduled Macro)
8. W69O-E22 Remaining-Vol Budget (Straddle vs Realized-So-Far)
9. W69O-E32 Mechanical Hedge Absorption Ratio (Extends EDGE_ATLAS E03 MHPA)
10. W69O-E54 Gamma x Liquidity-Withdrawal Interaction
