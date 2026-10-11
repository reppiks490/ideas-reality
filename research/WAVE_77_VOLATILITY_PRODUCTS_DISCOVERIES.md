# Wave 77O — Volatility Products & Vol-Targeting Mechanics

Namespace: **W77O**

Thesis: volatility products and volatility-targeting strategies create mechanical, partly predictable flow. VIX/VX settle from SPX option opening quotes (SOQ), VIX itself is a minutes-based interpolation of options between 23 and 37 days, leveraged and inverse ETPs must rebalance daily (rebalance notional ~ A*L*(L-1)*r), and vol-control, CTA and risk-parity portfolios scale exposure inversely to estimated vol. The wave converts these into computable states with explicit sign and lag uncertainty. Verified anchors: Cboe VIX Methodology PDF (read directly), Tuzun FEDS 2013-48 (late-day LETF rebalancing), Augustin-Cheng-Van den Bergen FAJ 2021 (Volmageddon), Moreira-Muir JF 2017 with its out-of-sample critiques.

Boundary: W26R owns SOQ expiry/futures roll and index rebalance flows (this wave only uses SOQ for VIX settlement); W27V owns LULD/halts; W62C owns CFTC positioning; W69O owns dealer-Greeks. EDGE_ATLAS items on VIX are used only as context.

All candidates are research hypotheses only. Claude owns later implementation. No profitability is claimed; every edge is subject to the intermediate-outcome promotion gate (timing-safe data, purged walk-forward, multiple-testing control, named placebo).

## W77O-E01 — VIX Calculation Tenor Weight Migration

Primary source: Cboe VIX Methodology PDF (verified: options with >23 and <37 days to expiry; minutes-based T; N30 interpolation, 525,600 minutes per 365-day year)

Mechanism / Features: VIX is an interpolation of near and next terms; the weights w_near = (N_next - N30)/(N_next - N_near) change deterministically as time passes, so VIX loads on different expiries. Feature: w_near(t), and the quantity VIX_term_contribution.

Target: Deterministic VIX drift vs term-structure slope.

Falsify-if: Falsify if weights have no explanatory power for day-over-day VIX change beyond the 30d-VIX futures differences.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: A-

## W77O-E02 — Weekly Expiry Insertion Kink in VIX Term

Primary source: Cboe VIX Methodology (weeklys PM-settled; included in spot VIX)

Mechanism / Features: With weeklys, near and next terms are close together; term roll-in kinks. Feature: gap between near and next expiries (days).

Target: VIX jump on term switch.

Falsify-if: Falsify if switch dates show no abnormal VIX move vs placebo days.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W77O-E03 — Zero-Bid Truncation Understatement in Stress

Primary source: Cboe VIX Methodology (strike set ends at two consecutive zero bids; only non-zero bids included; verified)

Mechanism / Features: In violent moves wings lose bids and are excluded, so VIX can understate tail pricing; the number of eligible strikes is a hidden state. Feature: strikes_used / strikes_baseline per term.

Target: VIX shortfall vs realized in following hours.

Falsify-if: Falsify if strike count carries no information after VIX level.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W77O-E04 — Index Staleness: VX Futures vs VIX Index Lead-Lag

Primary source: Cboe VIX index (computed from SPX option midpoints, cadence PROVENANCE_PENDING) vs VX futures

Mechanism / Features: The index is computed from option quotes and can lag futures during fast tape; VX1 changes may lead index changes. Feature: cross-correlation at lags.

Target: VIX index update.

Falsify-if: Falsify if lag zero at the data cadence.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W77O-E05 — SOQ Settlement Basis (Wednesday Gap)

Primary source: Cboe VIX futures settlement process document (cdn.cboe.com/resources/futures/VIX_Futures_Settlement_Process.pdf returned 403; content UNVERIFIED)

Mechanism / Features: VX/VIX options final settlement is based on SPX option opening quotations (SOQ), not the prior close. Feature: basis_SOQ = SOQ_VIX - VIX_prev_close; VX1 final settle gap vs Tuesday settle.

Target: Distribution of basis conditional on overnight ES move.

Falsify-if: Falsify if basis is predictable from overnight ES move and opening spreads, which would show it is priced; else residual unpredictability remains.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: A

## W77O-E06 — SOQ Opening-Quote Spread Dependence

Primary source: Cboe settlement process (UNVERIFIED); SPX option opening quotes

Mechanism / Features: Wide opening spreads (late opening in constituents) make SOQ noisy. Feature: opening width in key strikes and number of late-opening S&P constituents (W26R-E27).

Target: SOQ minus 9:45 VIX.

Falsify-if: Falsify if basis dispersion unrelated to spread/late-open metrics.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W77O-E07 — VX Settlement-Day Convergence Path

Primary source: CFE VX daily settlement (cboe.com futures market statistics settlement page, verified existence of VX/VXM settlements)

Mechanism / Features: Last-day VX1 should converge to SOQ; convergence error reveals hedger positioning. Feature: VX1 settle - SOQ expectation.

Target: Size of final gap.

Falsify-if: Falsify if distribution centered at zero with no state dependence.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W77O-E08 — Contango per Trading Day Roll Yield State

Primary source: VX settlement prices (Cboe settlement page); S&P 500 VIX Short-Term Futures Index rolls daily from first to second month (per ProShares fund page, verified summary)

Mechanism / Features: Normalized roll: r = (VX2 - VX1)/(VX1 * business_days_between) rather than raw spread. Feature: daily roll yield; sign persists.

Target: Next-day VX1 change and short-vol ETP behavior.

Falsify-if: Falsify if normalized roll yields no gain over raw spread in predicting VX1 returns.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: A

## W77O-E09 — VX-Spot Basis Expected Convergence Rate

Primary source: VX1 and spot VIX

Mechanism / Features: Convergence is not guaranteed; basis/days gives implied drift. Feature: basis/(days to expiry).

Target: Realized spot-VIX drift.

Falsify-if: Falsify if realized drift unrelated.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W77O-E10 — VIX Convexity-Adjusted Forward Gap

Primary source: Option strip forward variance; Jensen gap

Mechanism / Features: VIX futures price equals expectation of sqrt variance, below sqrt of expected variance. Feature: sqrt(E[var]) - VX.

Target: VX forecast error.

Falsify-if: Falsify if gap is constant (no state info).

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B

## W77O-E11 — VX Term-Structure Inversion Risk Gate

Primary source: VX1..VX4 settlements

Mechanism / Features: Inversion (VX1 > VX2 after day-adjustment) flags acute hedging demand. Gate: reduce risk entries when inverted.

Target: Next-day ES variance.

Falsify-if: Falsify if inversion adds nothing to VIX level and RV.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A+

## W77O-E12 — VX Curve PCA State (Level/Slope/Curvature)

Primary source: VX settlements; PCA fit rolling

Mechanism / Features: Compact state: three factors. Use factor changes as regime features.

Target: Regime accuracy.

Falsify-if: Falsify if PCA state redundant vs VIX and slope.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B

## W77O-E13 — Short-Vol Equity of ETP Net Vega State

Primary source: ProShares UVXY/SVXY objectives (1.5x and -0.5x since 2018-02-27 per ProShares 8-K exhibit) and shares outstanding/AUM

Mechanism / Features: Aggregate ETP exposure approximated as sum L_i*AUM_i in VIX-futures equivalents. Feature: net_vega_ETP.

Target: VX move sensitivity.

Falsify-if: Falsify if AUM-weighted exposure does not predict end-of-day VX imbalance.

Horizon: DAILY

Availability: PUBLIC_DELAYED

Priority: A

## W77O-E14 — Daily Rebalance Notional Formula for Leveraged Vol ETPs

Primary source: Cheng and Madhavan, 'The Dynamics of Leveraged and Inverse ETFs', JOIM 2009 (rebalance exacerbates volatility toward the close)

Mechanism / Features: For leverage L and AUM A, end-of-day rebalance in underlying exposure ~ A*L*(L-1)*r (r = underlying index return). For L = 1.5 and L = -0.5, L(L-1) = 0.75 in both cases, so both products require same-direction buying after up moves. Feature: R = A*0.75*r.

Target: Late-day VX volume and price drift.

Falsify-if: Falsify if R does not correlate with closing-window VX returns after controlling for day return.

Horizon: DAILY

Availability: PUBLIC_DELAYED

Priority: S-

## W77O-E15 — VX Contract Conversion of ETP Rebalance

Primary source: Index weights across VX1/VX2 per SPVXSTR methodology (weights ~ constant-maturity roll; exact index methodology PROVENANCE_PENDING)

Mechanism / Features: Convert R to contract count N = R/(1000*VX price)*weights; compare to VX volume in the closing window. Feature: participation ratio rho = N/volume.

Target: Price impact.

Falsify-if: Falsify if rho does not increase impact beyond volume.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W77O-E16 — Volmageddon-Class Fragility Indicator

Primary source: Augustin, Cheng, Van den Bergen, 'Volmageddon and the Failure of Short Volatility Products', FAJ 77(3) 2021 (2018-02-05 loss >90% in short-vol ETPs; rebalance feedback loop)

Mechanism / Features: Fragility = rho * (short ETP AUM/VX OI) * recent VX jump; ratio of short exposure to market depth.

Target: Probability of VX gap in the closing window.

Falsify-if: Falsify if fragility has no relation to extreme VX moves in post-2018 sample (structure changed).

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A

## W77O-E17 — Post-2018 Structural Break Control for Vol ETPs

Primary source: ProShares 8-K Feb 2018 (multiple changes)

Mechanism / Features: All pre-2018-02-27 ETP flow results must be separated from post-change; run split.

Target: Parameter stability.

Falsify-if: Falsify results that rely only on pre-change sample.

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B+

## W77O-E18 — Vol-ETP Premium/Discount Stress Indicator

Primary source: ETP price vs NAV

Mechanism / Features: Gaps signal creation-redemption stress. Feature: premium z-score.

Target: Subsequent VX move.

Falsify-if: Falsify if premium indistinguishable from noise.

Horizon: DAILY

Availability: PUBLIC_DELAYED

Priority: B

## W77O-E19 — Equity LETF Closing-Hour Rebalance Estimator (NQ/ES)

Primary source: Tuzun FEDS 2013-48 'Are Leveraged and Inverse ETFs the New Portfolio Insurers?' (verified: concentrated in 3-4 pm; about $1.04B purchases per 1% rise on $20B in Dec 2011; partial reversal next day)

Mechanism / Features: For equity LETFs (TQQQ, SQQQ, SPXL, SPXS), R_i = A_i*L_i*(L_i-1)*r. Sum signed R_i by index. Feature: R_NQ, R_ES as late-session flow and next-day reversal.

Target: ES/NQ 15:00-16:00 ET return.

Falsify-if: Falsify if R is not related to last-hour return after Baltussen gamma and rest-of-day return controls.

Horizon: INTRADAY

Availability: PUBLIC_DELAYED

Priority: A+

## W77O-E20 — LETF Rebalance x Option Gamma Same-Sign Agreement

Primary source: Tuzun FEDS 2013; Baltussen et al. JFE 2021

Mechanism / Features: Both flows late-day; when their signs agree, amplification may be stronger. Feature: sign(R)*sign(gamma flow).

Target: Magnitude of last-30-min move.

Falsify-if: Falsify if agreement indicator no better than either alone.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W77O-E21 — LETF Flow vs MOC Imbalance Check

Primary source: Exchange MOC imbalance feeds (NYSE/Nasdaq; W26R-E19)

Mechanism / Features: Compare estimated LETF flow with published imbalance to detect execution timing. Feature: corr(R, imbalance).

Target: Timing of execution.

Falsify-if: Falsify if zero correlation.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W77O-E22 — VVIX Level and Percentile State

Primary source: Cboe VVIX (launched 2012-03-14 per secondary; computed with VIX-style logic from VIX options; Cboe VVIX white paper not retrieved - PROVENANCE_PENDING)

Mechanism / Features: Expected vol of VIX; high VVIX flags tail hedge demand in VIX options. Feature: VVIX percentile, VVIX/VIX ratio.

Target: Next-day VIX jump probability.

Falsify-if: Falsify if VVIX/VIX ratio adds nothing to VIX and VX slope.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A

## W77O-E23 — VVIX-VIX Divergence (Event Hedging)

Primary source: VVIX and VIX

Mechanism / Features: VIX flat with VVIX rising implies hedgers buying VIX calls ahead of event. Feature: d VVIX - beta*d VIX.

Target: Pre-event realized vol.

Falsify-if: Falsify if divergence has no relation to event move vs placebo.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W77O-E24 — SKEW Index Level Regime (Tail Hedge Demand)

Primary source: Cboe SKEW Index (SKEW = 100 - 10*S, with S the skewness of 30-day SPX log return from option strip; white paper not directly retrieved - PROVENANCE_PENDING)

Mechanism / Features: High SKEW is not a direct crash predictor; join with VIX. Feature: SKEW z-score, SKEW-VIX quadrants.

Target: Left-tail frequency.

Falsify-if: Falsify if tail frequency same across quadrants.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W77O-E25 — SKEW Wing-Liquidity Contamination Control

Primary source: Same as above

Mechanism / Features: SKEW is sensitive to deep OTM strike prices; apply a control by recomputing SKEW with trimmed strikes.

Target: Rank correlation.

Falsify-if: Falsify if trimmed and untrimmed behave the same.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B

## W77O-E26 — Weekend and Holiday Calendar-Time Mismatch in Implied Vol

Primary source: Cboe VIX Methodology (T in calendar minutes; verified)

Mechanism / Features: VIX accrues over calendar time while realized variance accrues on trading days; Friday-to-Monday implied variance per trading day is mispriced if the market uses trading-day variance. Feature: VIX^2/ (trading days in 30 cal days) vs VIX^2/ (calendar).

Target: Monday VIX change and RV.

Falsify-if: Falsify if Monday effect zero vs matched weekdays.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: A

## W77O-E27 — Realized Variance Estimator Selection (Kernel vs Sparse)

Primary source: Barndorff-Nielsen, Hansen, Lunde, Shephard, Econometrica 76(6) 2008 (realized kernels with microstructure noise)

Mechanism / Features: Choose RV estimator for ES/NQ intraday: sparse 5-min RV, realized kernel, two-scale; signature plot. Feature: RV_kernel vs RV_5min.

Target: Forecast MSE for next-hour RV.

Falsify-if: Falsify if complicated estimator no better than 5-min RV out of sample.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W77O-E28 — Overnight vs Intraday Variance Share

Primary source: ES Globex vs RTH

Mechanism / Features: Variance split by session; allocation affects vol-target scaling. Feature: share_overnight.

Target: Next-day gap size.

Falsify-if: Falsify if no predictive power.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A-

## W77O-E29 — Intraday Variance Risk Premium via VX Futures vs ES RV

Primary source: VX1 and ES RV

Mechanism / Features: VX1 - RV proxy changes during day. Feature: VX1^2 - RV_forecast.

Target: Next-hour VX return.

Falsify-if: Falsify if premium has no sign information.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W77O-E30 — VA Variance Futures Accrual State

Primary source: Cboe S&P 500 Variance Futures (VA); search-verified: realized variance from listing-day SPX close to SOQ on final date, daily log returns, zero mean, 252-day annualization, rounded to 0.01; settlement prices on Cboe futures settlement page

Mechanism / Features: Remaining-variance implied by VA price after subtracting accrued realized variance; compare to VIX^2 of same maturity. Feature: implied_remaining = (VA*T_total - accrued)/T_remaining.

Target: Next-week RV.

Falsify-if: Falsify if implied_remaining no better than VIX^2.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W77O-E31 — VA vs VIX^2 Spread

Primary source: VA settlement and VIX

Mechanism / Features: Spread captures dividend/hedge differences and variance premium. Feature: VA - VIX^2.

Target: Spread persistence.

Falsify-if: Falsify if spread is constant noise.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B

## W77O-E32 — Vol-Control Fund Exposure Curve Estimator

Primary source: Press-sourced sizing (Reuters 2022: ~$10B sale on a rise to 35-40 realized vol; Barclays 2018 estimate of $225B of ~$500B; Nomura 2026 estimates ~$108B sold) - broker research, not primary; fund prospectuses PROVENANCE_PENDING

Mechanism / Features: Exposure E = min(cap, target/RV_est) with RV_est = max(RV_1m, RV_3m); flow = AUM*(E_t - E_{t-1}). Parameters: target 10-15%, cap 100-150%, lags.

Target: Next-day ES return conditional on predicted selling.

Falsify-if: Falsify if predicted flow has no relationship to returns across lag variants; unknown AUM scale treated as nuisance parameter.

Horizon: DAILY

Availability: PUBLIC_DELAYED

Priority: A

## W77O-E33 — Vol-Control Lag Identification

Primary source: Same

Mechanism / Features: Identify T+1/T+2 execution lag by regressing ES flow-proxy (volume imbalance) on exposure change at lags 0..5.

Target: Best lag.

Falsify-if: Falsify if no lag shows significance (then flow isn't visible).

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W77O-E34 — Realized-Vol Crossing Trigger Distance

Primary source: RV_1m, RV_3m

Mechanism / Features: Distance to the RV level where exposure changes by x%: price move needed to push RV across threshold. Feature: required_move to hit RV threshold.

Target: Probability of trigger in next day.

Falsify-if: Falsify if proximity unrelated to flow.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W77O-E35 — CTA Vol-Scaling Cut Estimator

Primary source: Hurst, Ooi, Pedersen, 'A Century of Evidence on Trend-Following Investing' (JPM 2017; positions scaled to 10% annualized ex-ante vol)

Mechanism / Features: Position_i = sign(trend)*sigma_target/sigma_i; when sigma jumps, cut = 1 - sigma_old/sigma_new even without a signal flip. Feature: implied position change from sigma jump.

Target: ES/NQ/other futures direction.

Falsify-if: Falsify if no predictive link after trend control.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A

## W77O-E36 — CTA Trend-Flip Distance Map

Primary source: Multi-lookback moving averages | futures price

Mechanism / Features: Price levels where signals flip (e.g., 1m,3m,6m,12m). Feature: distance-to-flip in ATR units.

Target: Reaction near flip levels.

Falsify-if: Falsify if flip levels behave like arbitrary levels (placebo).

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A

## W77O-E37 — Risk-Parity Cross-Asset Vol Shock Transmission

Primary source: Realized vols in ES, ZN, others

Mechanism / Features: When bond and equity vol both rise, risk parity de-levers both. Feature: joint vol z-score of equity and rates.

Target: Next-day cross-asset selling.

Falsify-if: Falsify if joint-shock days show no excess comovement vs placebo.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A-

## W77O-E38 — Correlation-Jump Leverage Amplifier

Primary source: Realized correlation matrix

Mechanism / Features: Portfolio vol depends on correlation; spikes raise target exposure cut. Feature: d(corr) times weights.

Target: Cross-asset flows.

Falsify-if: Falsify if correlation adds nothing beyond vols.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W77O-E39 — Moreira-Muir Baseline Overlay for Own System

Primary source: Moreira and Muir, 'Volatility-Managed Portfolios', JF 72(4) 2017 (critiques: Cederburg et al. 2020 out-of-sample; Barroso-Detzel 2021 costs)

Mechanism / Features: Scale own system risk by 1/RV forecast; baseline comparator for any new vol gating. Feature: weight = c/RV_forecast.

Target: Net Sharpe vs unscaled.

Falsify-if: Falsify if scaling does not improve net-of-cost drawdown out-of-sample.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A+

## W77O-E40 — Vol-Spike Half-Life State (HAR)

Primary source: ES realized vol

Mechanism / Features: Estimate how quickly volatility shocks decay; used to time vol-control re-entry. Feature: HAR decay parameter.

Target: Re-risking timing.

Falsify-if: Falsify if half-life unstable.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W77O-E41 — Spot-Vol Correlation Breakdown (Spot-Up Vol-Up)

Primary source: ES and VX1 5-min changes

Mechanism / Features: Rolling beta of dVX on dES; positive beta indicates unusual regime (call buying or event hedging). Feature: beta, sign.

Target: Next-hour reversal.

Falsify-if: Falsify if breakdown not followed by regime difference.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W77O-E42 — Vol-of-Vol Intraday Regime

Primary source: 1-min VX1 changes realized vol

Mechanism / Features: Vol-of-vol clustering is a separate regime. Feature: RV of dVX1 (5-min), percentile.

Target: Next-hour ES range.

Falsify-if: Falsify if vol-of-vol adds nothing to ES RV.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W77O-E43 — VIX Short-Dated Indices Event Gauge (VIX9D, VIX1D)

Primary source: Cboe volatility indices (VIX9D and VIX1D existence/methodology PROVENANCE_PENDING)

Mechanism / Features: Ratio of short-dated to 30d vol quantifies event concentration. Feature: VIX9D/VIX.

Target: Event realized.

Falsify-if: Falsify if ratio no better than 0DTE straddle.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W77O-E44 — Cross-Asset Vol Composite (VIX, GVZ, OVX, MOVE)

Primary source: Cboe GVZ/OVX; ICE MOVE (rights/methodology PROVENANCE_PENDING)

Mechanism / Features: Dispersion of implied vols across equity, gold, oil, rates. Feature: z-score vector and PCA.

Target: Cross-asset regime.

Falsify-if: Falsify if redundant with VIX.

Horizon: DAILY

Availability: LICENSED_REALTIME

Priority: B+

## W77O-E45 — Crypto Implied Vol Link (DVOL)

Primary source: Deribit DVOL index (existence from memory; PROVENANCE_PENDING)

Mechanism / Features: BTC implied vol vs VIX for crypto risk gates. Feature: DVOL/VIX ratio.

Target: BTC move.

Falsify-if: Falsify if no incremental.

Horizon: INTRADAY

Availability: PUBLIC_REALTIME

Priority: B

## W77O-E46 — Pre-Event VX Drift and Post-Event Crush

Primary source: VX futures vs macro calendar

Mechanism / Features: VX run-up before FOMC/CPI and crush after. Feature: VX1 return from t-2h to event.

Target: Post-event reversal.

Falsify-if: Falsify if equal to non-event days.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W77O-E47 — VIX Options Expiry and VX Final Settlement Hedging Activity

Primary source: CFE VX expiry procedures (UNVERIFIED)

Mechanism / Features: Settlement-day activity may distort VIX around the SOQ. Feature: VX volume spike near open.

Target: SPX open dispersion.

Falsify-if: Falsify if no distortion vs placebo Wednesdays.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: B

## W77O-E48 — Holiday-Shifted VX Settlement Calendar

Primary source: Cboe holiday rule for VX (UNVERIFIED)

Mechanism / Features: Settlement shifts around holidays create atypical gaps. Feature: indicator.

Target: Gap size.

Falsify-if: Falsify if equal.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: B

## W77O-E49 — Short-Vol ETP Positioning via CFTC Reports (links W62C)

Primary source: CFTC COT for VIX futures (W62C)

Mechanism / Features: Weekly positioning; use as slow prior only. Feature: net managed money.

Target: Weekly VX return.

Falsify-if: Falsify if lag makes useless.

Horizon: WEEKLY

Availability: PUBLIC_SCHEDULED

Priority: B

## W77O-E50 — VX Open Interest and Volume Intraday Participation State

Primary source: CFE volume data

Mechanism / Features: Volume spikes relative to OI indicates hedger activity. Feature: volume/OI.

Target: Next-hour VX return.

Falsify-if: Falsify if no relation.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W77O-E51 — Vol-Regime Hysteresis HMM with Vol-of-Vol

Primary source: ES RV, VX slope, VVIX

Mechanism / Features: Two-dimensional regime with hysteresis to avoid flicker. Feature: posterior.

Target: Regime-conditional edge.

Falsify-if: Falsify if HMM no better than threshold rules.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W77O-E52 — Own-System Vol-Target Re-estimation Cadence

Primary source: Own system returns

Mechanism / Features: Intraday re-estimation of risk target vs daily. Feature: ex-ante vol at 5-min cadence.

Target: Realized vs target.

Falsify-if: Falsify if cadence irrelevant.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W77O-E53 — Gap-Aware Vol Floor for Position Sizing

Primary source: ES overnight gaps

Mechanism / Features: Floor sigma by gap volatility to avoid under-estimating. Feature: sigma_floor.

Target: Drawdown.

Falsify-if: Falsify if floor harms net.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W77O-E54 — VIX Index Level vs Tradable Futures Execution Gap

Primary source: VIX not tradable (index) vs VX

Mechanism / Features: Signals derived from spot VIX must be mapped to VX with basis; ensure signal uses tradable instrument. Feature: execution-adjusted return.

Target: Net return.

Falsify-if: Falsify if mapping cost eliminates edge.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W77O-E55 — Placebo Vol-Control Dates (Shuffled Flow)

Primary source: Shuffled flows

Mechanism / Features: Control: shuffle estimated vol-control flows in time.

Target: n/a

Falsify-if: Required negative control.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A

## W77O-E56 — VX Calendar-Spread Liquidity and Slippage Gate

Primary source: CFE VX order book depth (feed spec PROVENANCE_PENDING)

Mechanism / Features: Execution in VX during ETP rebalance windows has worse spreads; gate trading in VX only when spread/depth normal. Feature: spread z-score, depth ratio.

Target: Execution slippage.

Falsify-if: Falsify if slippage unrelated to rebalance windows.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W77O-E57 — GVZ-Gold Implied-Realized Gap Gate

Primary source: Cboe Gold ETF Volatility Index (GVZ; methodology PROVENANCE_PENDING) vs GC realized variance

Mechanism / Features: Gap between implied and realized vol on gold gates breakout vs mean-reversion entries in gold. Feature: GVZ^2 - RV_kernel.

Target: Gold next-hour range.

Falsify-if: Falsify if gap adds nothing over own RV.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: B+

## W77O-E58 — OVX-Energy Implied-Realized Gap Gate

Primary source: Cboe Crude Oil ETF Volatility Index (OVX; PROVENANCE_PENDING)

Mechanism / Features: Same construction for CL.

Target: CL next-hour range.

Falsify-if: Falsify if redundant with own RV.

Horizon: INTRADAY

Availability: LICENSED_REALTIME

Priority: B

## W77O-E59 — Dynamic ES-VX Hedge Ratio Estimator

Primary source: ES and VX1 5-min returns

Mechanism / Features: Rolling regression hedge ratio for using VX as overlay for ES risk; unstable ratio flags regime. Feature: beta_t and its instability.

Target: Hedge effectiveness.

Falsify-if: Falsify if ratio unstable beyond noise or no variance reduction vs static.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W77O-E60 — Vol-Complex Truth Ladder

Primary source: All of the above

Mechanism / Features: SETTLEMENT/SOQ MECHANICS -> VIX/VX/VVIX/SKEW STATE -> ETP REBALANCE & VOL-CONTROL/CTA FLOW ESTIMATES -> REALIZED VOL (KERNEL) VS IMPLIED -> EQUITY-INDEX FUTURES RESPONSE -> OWN RISK TARGET. Rule: each rung passes its gate before the next is used.

Target: Architecture.

Falsify-if: Falsify if signal passes while lower rungs fail.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S

## Highest-priority W77O tests

1. W77O-E14 Daily Rebalance Notional Formula for Leveraged Vol ETPs
2. W77O-E19 Equity LETF Closing-Hour Rebalance Estimator (NQ/ES)
3. W77O-E41 Spot-Vol Correlation Breakdown (Spot-Up Vol-Up)
4. W77O-E11 VX Term-Structure Inversion Risk Gate
5. W77O-E05 SOQ Settlement Basis (Wednesday Gap)
6. W77O-E39 Moreira-Muir Baseline Overlay for Own System
7. W77O-E26 Weekend and Holiday Calendar-Time Mismatch in Implied Vol
8. W77O-E32 Vol-Control Fund Exposure Curve Estimator
9. W77O-E16 Volmageddon-Class Fragility Indicator
10. W77O-E27 Realized Variance Estimator Selection (Kernel vs Sparse)
