# Wave 78B — Execution Quality And Transaction-Cost Science For Futures

Namespace: **W78B**

Thesis: for an intraday multi-asset futures system the dominant controllable drag is execution cost, and it is state-dependent: slippage, adverse selection of passive fills, protection-order outcomes, latency and session/roll windows vary with spread-in-ticks, depth percentile, queue rank, volatility and clock position. Treating cost as a constant per-contract haircut hides both the tail (exits in stress) and the decision boundary between passive and aggressive execution. W78B defines cost as a modeled, tested, versioned object: implementation-shortfall ledgers, realized-spread/impact decompositions, quantile slippage surfaces, monotonicity diagnostics, latency budgets, fee hurdles and session/roll multipliers.

Boundary: W70B owns the order-book and exchange-rule state variables (queue position, protection envelopes, price limits, timestamps) that W78B consumes. W17P owns venue status; W63M/W12 own margin and performance-bond events; W49P/W56G/W55T own physical-delivery, bullion and financing mechanics that affect roll windows; W27V owns equity LULD. W78B owns measurement, modeling and decision rules for execution cost and order-type choice, and economic items (fees, data fees). Fee numbers are secondary-source and UNVERIFIED against the CME schedule.

All candidates are research hypotheses only. Claude owns later implementation. No profitability is claimed; every candidate must pass the vault's intermediate-outcome promotion gate (source predicts an intermediate microstructure/cost outcome before any return claim) and must beat its named negative control.

## W78B-E01 — Four-Part Shortfall Ledger Per Parent Order

Primary source: Perold, The implementation shortfall: paper versus reality, J. Portfolio Management 14(3), 1988 (classical; bibliographic detail PROVENANCE_PENDING) (W78B-D01)

Mechanism: Implementation shortfall splits paper-vs-real return into delay, spread/impact, and opportunity (unfilled) cost. For intraday futures the decision price is the signal timestamp price; the ledger isolates which component the strategy actually loses to.

Features: IS = delay (arrival-decision) + execution (fill-arrival) + opportunity (unfilled qty * subsequent move) + fees; per parent order, per instrument, per state bucket.

Target: Total and component cost in ticks and in sigma_1min.

Falsify-if: Component shares are unstable (rank of dominant component changes in >50% of weeks) so ledger cannot guide design.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: S-

## W78B-E02 — Benchmark Choice Sensitivity (Mid vs Micro-Price vs Touch)

Primary source: Perold, The implementation shortfall: paper versus reality, J. Portfolio Management 14(3), 1988 (classical; bibliographic detail PROVENANCE_PENDING) (W78B-D01) + Cont, Kukanov, Stoikov, arXiv:1011.6402 (W78B-D16)

Mechanism: Reported slippage sign and size depends on benchmark: arrival mid, micro-price, far touch. In large-tick books the mid-vs-touch gap alone is half a tick.

Features: Report slippage under B in {mid, micro-price, touch, next-event mid}; benchmark-spread = max-min across B.

Target: Whether a cost-model conclusion survives benchmark change.

Falsify-if: Rank of strategies by cost is invariant to B (then benchmark debate is moot).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W78B-E03 — Realized-Spread / Price-Impact Fill Decomposition

Primary source: Perold, The implementation shortfall: paper versus reality, J. Portfolio Management 14(3), 1988 (classical; bibliographic detail PROVENANCE_PENDING) (W78B-D01)

Mechanism: Effective spread splits into realized spread (maker revenue) and price impact (information). Classical decomposition; applying it to our own fills tells whether passive fills are paid or picked off.

Features: eff = 2*s*(P_fill-M_0)/M_0; real_spread_k = 2*s*(P_fill-M_k); impact_k = eff-real_spread_k, k in {1s,5s,30s,300s}.

Target: Role-conditional (maker/taker) realized spread.

Falsify-if: Realized spread for our maker fills is negative at 5s and 30s horizons in the majority of weeks (then passive posting is net unprofitable under current state set).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A+

## W78B-E04 — Sigma-Normalized Cross-Asset Cost Ledger

Primary source: CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W78B-D08) + CME ZN/CL/GC contract spec pages (see W78B-D19), tick: ZN 1/64 pt, CL $0.01, GC $0.10

Mechanism: Tick values differ (ES $12.50, ZN $15.625, CL $10, GC $10); costs only compare after normalizing by volatility and tick. Normalized costs identify which instrument the strategy can afford to trade aggressively.

Features: c_sigma = slippage_ticks*tick/sigma_1min; ratio to expected alpha per trade in sigma.

Target: Cost-to-alpha ratio ranking.

Falsify-if: Instrument ranking by c_sigma differs between regimes in >40% of days (not stable enough to allocate on).

Horizon: DAILY
Availability: PUBLIC_SCHEDULED
Priority: B+

## W78B-E05 — Slippage-By-State Quantile Surface

Primary source: Cont, Kukanov, Stoikov, arXiv:1011.6402 (W78B-D16) + Dayri, Rosenbaum, arXiv:1207.6325 (W78B-D17)

Mechanism: Mean slippage hides tails. Quantile regression on state vector (spread ticks, imbalance, depth ratio, realized vol, time-of-day, minutes-to-event) gives q50/q90/q99 slippage forecasts used as inputs to sizing and routing.

Features: Q_tau(slip | x) with x=[spread_ticks, I, size/D1, rv_1m, tod, event_prox, depth_pctile]; pinball loss.

Target: Out-of-sample pinball loss vs unconditional quantiles.

Falsify-if: Pinball loss improvement <3% relative to unconditional quantile by instrument OOS.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: S

## W78B-E06 — Cost Monotonicity Test (Size, Urgency, Spread)

Primary source: Almgren, Chriss, Optimal execution of portfolio transactions, J. Risk 3(2), 2000 (classical; PROVENANCE_PENDING) (W78B-D02)

Mechanism: Expected cost should be non-decreasing in child size and urgency (and weakly in spread). Violations imply data bugs, mismeasured arrival price or a model fitted on selection bias.

Features: Isotonic test: fit cost(size) and cost(spread_ticks) with and without monotonic constraint; report violation share and Spearman rho.

Target: Model-validation flag (go/no-go for cost model).

Falsify-if: None; this is a diagnostic. Failure = monotonicity violated in more than 10% of size bins, which blocks promotion of the cost model.

Horizon: DAILY
Availability: PAID_REALTIME
Priority: A+

## W78B-E07 — Participation-Impact Square-Root Fit On Futures

Primary source: Almgren, Chriss, Optimal execution of portfolio transactions, J. Risk 3(2), 2000 (classical; PROVENANCE_PENDING) (W78B-D02) + Frazzini, Israel, Moskowitz, Trading costs (SSRN, 2018) (PROVENANCE_PENDING) (W78B-D18)

Mechanism: Impact often fits a concave (square-root) function of participation in equities; futures with deep books may differ. Fit exponent delta in impact = a*sigma*(Q/V)^delta using own fills; compare delta to 0.5 and 1.

Features: log-log regression of slippage_sigma on participation over 1-5 min windows; CI on delta.

Target: Estimated exponent and capacity curve for ES/NQ lots.

Falsify-if: delta CI excludes concavity (>=1) or fit R2<0.05 in our size range (then impact term is negligible; treat as fixed spread cost).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W78B-E08 — Shortfall Versus Delay: Decision-To-Order Latency Cost

Primary source: Perold, The implementation shortfall: paper versus reality, J. Portfolio Management 14(3), 1988 (classical; bibliographic detail PROVENANCE_PENDING) (W78B-D01)

Mechanism: The delay component (decision to order arrival) is large when signals are fast; it is the cost of information age that no queue strategy can recover.

Features: delay_cost = sign*(M_arrival - M_decision) in ticks; regress on A (information age).

Target: Marginal ticks per ms of delay.

Falsify-if: Slope of delay_cost on A is indistinguishable from zero over the observed A range.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E09 — Fill-Conditional Adverse Selection Curve

Primary source: Moallemi, Yuan, A model for queue position valuation in a limit order book (Columbia GSB WP 2017) (W78B-D11)

Mechanism: Passive orders fill disproportionately when price is about to move through them (winner's curse): E[markout | fill] is worse than E[markout] unconditional. Size the curve by queue rank, imbalance and spread.

Features: AS_k(state) = E[sign*(M_{t+k}-P_fill) | fill, state] for k in 1s,5s,30s; versus unconditional drift for placebo timestamps.

Target: Markout shortfall of fills versus placebo.

Falsify-if: AS_k is not different from placebo markouts (paired bootstrap p>0.1) in any state bucket.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: S-

## W78B-E10 — Imbalance-Conditional Posting Rule

Primary source: Moallemi, Yuan, A model for queue position valuation in a limit order book (Columbia GSB WP 2017) (W78B-D11) + Cont, Kukanov, Stoikov, arXiv:1011.6402 (W78B-D16)

Mechanism: Posting a bid when queue imbalance is already negative gets filled only as the book thins (toxic). Conditioning posting on imbalance filters toxic fills.

Features: post_bid iff I_t > theta; fill markout by I deciles; theta chosen on training folds.

Target: Net passive PnL per fill after conditioning.

Falsify-if: Net PnL per fill does not improve over unconditional posting by at least the fee per contract (cost model from W78B-E33).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A+

## W78B-E11 — Cancel-Before-Adverse Latency Value

Primary source: Lehalle, Mounjid, arXiv:1610.00261 (W78B-D09)

Mechanism: Latency determines whether a cancel can beat the information that makes the resting order stale. Value of cancel option V_c = P(adverse event) * P(cancel wins) * loss avoided.

Features: P(cancel wins) from own measured cancel-ack latency distribution vs event lead time; V_c per order.

Target: Avoided adverse fills per 1000 orders.

Falsify-if: Cancel-win probability is below 10% at our latency tier, so cancel logic has no value and passive orders must be sized small instead.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E12 — Passive-vs-Aggressive Decision Boundary

Primary source: Moallemi, Yuan, A model for queue position valuation in a limit order book (Columbia GSB WP 2017) (W78B-D11) + Lehalle, Mounjid, arXiv:1610.00261 (W78B-D09)

Mechanism: Post if p_fill*(h - AS) > (1-p_fill)*C_chase, where h is half-spread, AS fill-conditional adverse selection, C_chase the cost of converting to aggressive after delay. The boundary is a function of state.

Features: Compute both sides per decision from W78B-E09,E14 and W70B-E18; choose min expected cost.

Target: Expected cost difference passive vs aggressive.

Falsify-if: Realized cost under the rule is not lower than always-aggressive (paired by decision) over 3 months.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: S

## W78B-E13 — Fill Survival With Competing Risks

Primary source: Moallemi, Yuan, A model for queue position valuation in a limit order book (Columbia GSB WP 2017) (W78B-D11)

Mechanism: A passive order ends in fill, cancel or price-moved-away; naive time-to-fill ignores censoring and overstates fill rates.

Features: Cause-specific hazards h_fill, h_away, h_cancel; cumulative incidence at 1s..60s.

Target: Cumulative incidence of fill vs moved-away.

Falsify-if: Cumulative incidence from competing-risk model is no better calibrated than Kaplan-Meier with censoring only.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W78B-E14 — Chase Cost Distribution After Unfilled Passive

Primary source: Perold, The implementation shortfall: paper versus reality, J. Portfolio Management 14(3), 1988 (classical; bibliographic detail PROVENANCE_PENDING) (W78B-D01)

Mechanism: When a passive order is abandoned after tau seconds, the subsequent adverse move is the opportunity cost; its distribution depends on volatility state and imbalance.

Features: C_chase(tau)=E[sign*(M_{t+tau}-M_t) | unfilled at tau]*; by state quantile.

Target: Expected and q90 chase cost.

Falsify-if: C_chase is statistically equal to unconditional drift (no selection) in all states.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E15 — Accidental-Taker Rate (Latency Crossing)

Primary source: Lehalle, Mounjid, arXiv:1610.00261 (W78B-D09) + CME iLink Order Types, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227032/iLink+Order+Types (W78B-D07)

Mechanism: A limit order intended passive can cross and become taker if the book moved between decision and arrival; the fee/role changes and information is lost.

Features: accidental_taker = fills with aggressor role at price equal opposite touch at arrival; rate vs A.

Target: Share of passive intents executed as taker and their markout.

Falsify-if: Rate below 1% in all states (then immaterial).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W78B-E16 — Reprice Message Cost Versus Fill Gain

Primary source: CME Globex Messaging Efficiency Program, https://cmegroup.com/globex/trade-on-cme-globex/messaging-efficiency-program.html (W78B-D06)

Mechanism: Repricing a passive order retains queue position only if unchanged; modifications cost messages (MEP weights) and may lose priority. Fill gain from repricing must exceed message cost.

Features: marginal_fill_prob(reprice) - priority_loss; message_score weights from MEP (values PROVENANCE_PENDING).

Target: Net value per reprice.

Falsify-if: Repricing never improves expected cost versus cancel-and-hold in simulation using MBO queue (W70B-E09).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W78B-E17 — Maker-Taker Asymmetry Audit

Primary source: Public fee evidence: Interactive Brokers CME fee pass-through page https://interactivebrokers.com/en/accounts/fees/CME.php (non-member Globex E-mini equity USD 1.386 per search excerpt), Topstep fee article https://intercom.help/topstep-llc/en/articles/8284231 (ES exchange fee USD 2.76 round turn, MES USD 0.70, Feb 2025); CME's own fee schedule NOT retrieved (W78B-D04)

Mechanism: Where CME fees do not differentiate maker from taker (UNVERIFIED for our products), the passive-vs-aggressive choice is determined by spread capture vs adverse selection rather than rebates. An audit confirms fee symmetry by product and account type.

Features: fee_taker - fee_maker per product from fee schedule; difference in ticks.

Target: Fee asymmetry in ticks.

Falsify-if: CME schedule shows maker/taker or tiered asymmetry > 0.05 tick for our products (then include in decision boundary).

Horizon: SLOW_PRIOR
Availability: PUBLIC_SCHEDULED
Priority: B+

## W78B-E18 — MWP Versus Marketable Limit Slippage

Primary source: CME iLink Order Types, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227032/iLink+Order+Types (W78B-D07)

Mechanism: Market-with-protection caps fills at best +/- protection points but fills as many levels as available; a marketable limit set at touch+k ticks caps explicitly. Difference arises in sweep fill price and unfilled-remainder behavior.

Features: paired simulation using MBO: fill price & remainder for MWP vs limit(k) with k in 0..4 ticks.

Target: Expected cost and fill completeness.

Falsify-if: No difference in total cost within 0.05 tick across order types when depth >= size.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E19 — Exit Order Type Under Gap: Stop vs Stop-Limit vs Stop-Protection

Primary source: CME iLink Order Types, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227032/iLink+Order+Types (W78B-D07)

Mechanism: Stop-limit may not fill after trigger; stop-with-protection fills within protection then rests; market stop is not offered (protection mandatory). Choose by gap risk.

Features: P(no fill within 5s after trigger) by type and by state (depth_pctile, spread, time-to-event).

Target: Failure-to-exit probability and tail loss.

Falsify-if: P(no fill) identical across types (when protection points exceed gap size).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A+

## W78B-E20 — Iceberg Display-Quantity Cost Benefit On Futures

Primary source: Bessembinder, Panayides, Venkataraman, Hidden liquidity, JFE 94(3):361-383 (W78B-D12)

Mechanism: Hidden-size orders in the cited equity study had smaller shortfall but lower and slower execution; futures iceberg value is untested. DisplayQty (iLink order qualifier) controls exposure.

Features: Compare fill rate, time-to-fill and markout for display fraction f in {1,0.5,0.2} in sim and live-shadow.

Target: Net cost per intended contract.

Falsify-if: Cost and fill rate independent of f within noise.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W78B-E21 — Volatility-Scaled Urgency Schedule

Primary source: Almgren, Chriss, Optimal execution of portfolio transactions, J. Risk 3(2), 2000 (classical; PROVENANCE_PENDING) (W78B-D02) + Obizhaeva, Wang, Optimal trading strategy and supply/demand dynamics, J. Financial Markets 16(1) (PROVENANCE_PENDING) (W78B-D03)

Mechanism: Almgren-Chriss trade-off between impact and risk: higher volatility argues for faster execution; resilience slows it. Intraday state determines lambda.

Features: child schedule n_k as function of lambda(rv_1m) and resilience tau (W70B-E57).

Target: Shortfall mean and variance vs flat schedule.

Falsify-if: Mean-variance of cost under state-scaled schedule not better than TWAP over matched samples.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W78B-E22 — Child-Size To Displayed-Depth Fraction Cap

Primary source: Cont, Kukanov, Stoikov, arXiv:1011.6402 (W78B-D16) + Almgren, Chriss, Optimal execution of portfolio transactions, J. Risk 3(2), 2000 (classical; PROVENANCE_PENDING) (W78B-D02)

Mechanism: Cost is convex in child size relative to displayed depth; capping f=Q_child/D1 maintains linear region.

Features: slip(f) piecewise-linear fit; knee f*; per instrument.

Target: Cost per contract by f.

Falsify-if: No knee (slip linear or flat in f up to 1.0).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E23 — Participation Cap By Time-Of-Day

Primary source: Almgren, Chriss, Optimal execution of portfolio transactions, J. Risk 3(2), 2000 (classical; PROVENANCE_PENDING) (W78B-D02)

Mechanism: Volume patterns create different liquidity per minute; a POV cap based on recent volume avoids over-participation in thin periods.

Features: POV_t = child_qty/volume_{t-60s}; cost vs POV by session segment.

Target: Slippage vs POV.

Falsify-if: No relationship between POV and slippage in any segment.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W78B-E24 — Timing Randomization Leakage Test

Primary source: Obizhaeva, Wang, Optimal trading strategy and supply/demand dynamics, J. Financial Markets 16(1) (PROVENANCE_PENDING) (W78B-D03)

Mechanism: Regular slice timing/size is detectable by others; the test is whether our own post-trade price reversal is larger when schedule is regular, i.e., information leakage from patterns. Legitimate execution randomization only.

Features: Randomize child interval & size within bounds; compare impact (reversal) vs fixed schedule in A/B shadow.

Target: Impact difference randomized vs fixed.

Falsify-if: Impact equal across schedules (no leakage).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B

## W78B-E25 — Exit-Versus-Entry Cost Asymmetry

Primary source: Perold, The implementation shortfall: paper versus reality, J. Portfolio Management 14(3), 1988 (classical; bibliographic detail PROVENANCE_PENDING) (W78B-D01)

Mechanism: Exits (stops, risk reductions) happen in adverse states and cost more than entries chosen by the strategy; a symmetric cost assumption understates strategy cost.

Features: cost_exit_ticks - cost_entry_ticks by exit type; state distribution at exit.

Target: Round-trip cost.

Falsify-if: Exit and entry costs equal in mean and q90 after state control.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E26 — Micro Versus E-Mini Routing Cost

Primary source: Public fee evidence: Interactive Brokers CME fee pass-through page https://interactivebrokers.com/en/accounts/fees/CME.php (non-member Globex E-mini equity USD 1.386 per search excerpt), Topstep fee article https://intercom.help/topstep-llc/en/articles/8284231 (ES exchange fee USD 2.76 round turn, MES USD 0.70, Feb 2025); CME's own fee schedule NOT retrieved (W78B-D04) + CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W78B-D08)

Mechanism: Secondary fee data show exchange fee 2.76 RT for ES vs 0.70 RT for MES (Feb 2025), i.e., micro fee per notional ~2.5x; but micros have thinner books. Breakeven size where ES is cheaper per notional.

Features: cost_per_notional = (fee+slippage_ticks*tick)/notional for ES vs MES at size Q.

Target: Optimal contract choice by size.

Falsify-if: MES total cost per notional lower than ES at all sizes >= 10 MES-equivalents (UNVERIFIED fees).

Horizon: DAILY
Availability: PAID_REALTIME
Priority: B+

## W78B-E27 — Spread-Order Versus Leg-Separately Roll Execution

Primary source: CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W78B-D08)

Mechanism: ES calendar spreads trade with 0.05 index point tick (spec) and via implied matching; rolling with a spread order vs two legs differs in cost and leg risk.

Features: cost_spread_order vs cost_legs = slippage_front + slippage_next + legging_risk; paired in roll window.

Target: Roll cost in ticks.

Falsify-if: Roll cost equal between spread order and leg-by-leg after legging risk.

Horizon: DAILY
Availability: PAID_REALTIME
Priority: B+

## W78B-E28 — Signal Half-Life Latency Tolerance

Primary source: Lehalle, Mounjid, arXiv:1610.00261 (W78B-D09)

Mechanism: Value of a signal decays with latency: V(L)=V0*exp(-L/tau). Each signal has a latency budget L*=tau*ln(V0/V_min).

Features: Estimate tau by replay with delay L in {0,1,5,20,100,500 ms}; budget table per signal.

Target: Budget in ms per signal; which signals are executable at our tier.

Falsify-if: Replay PnL independent of delay up to 500 ms for a given signal (then latency not binding) or exceeds budget for all signals.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A+

## W78B-E29 — Slippage-Versus-Latency Monotonicity

Primary source: Lehalle, Mounjid, arXiv:1610.00261 (W78B-D09)

Mechanism: Own telemetry: decision-to-ack and decision-to-fill latency should be monotone with slippage; non-monotone means confounding by state.

Features: Isotonic fit slip ~ L controlling for state; Spearman.

Target: Marginal ticks per ms.

Falsify-if: No monotone relationship (rho<0.03) in stationary windows.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E30 — Latency Tier Break-Even

Primary source: Lehalle, Mounjid, arXiv:1610.00261 (W78B-D09)

Mechanism: Moving from cloud to co-location is worth it only if marginal tick savings * volume > cost; savings function from W78B-E29 slope.

Features: benefit = slope*delta_L*N_trades*tick_value - extra_cost.

Target: Break-even trade count.

Falsify-if: Benefit < cost at our volume (then keep current tier); infrastructure costs are PROVENANCE_PENDING.

Horizon: SLOW_PRIOR
Availability: PAID_REALTIME
Priority: B

## W78B-E31 — Pick-Off Rate Of Resting Orders

Primary source: Lehalle, Mounjid, arXiv:1610.00261 (W78B-D09)

Mechanism: Resting orders are picked off by faster participants just after information events; rate = fraction of fills within delta of a trade-through or large aggressive print in correlated instrument.

Features: pickoff = fills within 5 ms..250 ms after external trigger events (cross-instrument sweep).

Target: Pick-off share of passive fills and its markout.

Falsify-if: Pick-off share below placebo shifted-trigger share.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W78B-E32 — Event-Clock Execution Decision Boundary

Primary source: CME iLink Order Types, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227032/iLink+Order+Types (W78B-D07)

Mechanism: Acting between match-event boundaries sends orders against an intermediate book; executing decisions only on event commits avoids phantom states (W70B-E01).

Features: decision_at_commit vs decision_at_message; difference in slippage.

Target: Slippage difference.

Falsify-if: No difference in slippage between commit-based and message-based triggers.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B

## W78B-E33 — Fee-To-Tick Hurdle

Primary source: Public fee evidence: Interactive Brokers CME fee pass-through page https://interactivebrokers.com/en/accounts/fees/CME.php (non-member Globex E-mini equity USD 1.386 per search excerpt), Topstep fee article https://intercom.help/topstep-llc/en/articles/8284231 (ES exchange fee USD 2.76 round turn, MES USD 0.70, Feb 2025); CME's own fee schedule NOT retrieved (W78B-D04) + CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W78B-D08)

Mechanism: Round-turn exchange fee as fraction of tick value sets minimum edge: ES 2.76/12.50 = 0.22 tick (secondary fee data, UNVERIFIED). All-in hurdle includes slippage and commissions.

Features: hurdle_ticks = (fee_exch+fee_clear+fee_reg+commission)/tick_value + expected_slippage_ticks.

Target: Whether expected edge exceeds hurdle per signal.

Falsify-if: Realized net edge per trade is below 0 although gross edge exceeds hurdle (then hurdle misestimated).

Horizon: DAILY
Availability: PUBLIC_SCHEDULED
Priority: A

## W78B-E34 — Volume-Tier Fee Dynamics

Primary source: Public fee evidence: Interactive Brokers CME fee pass-through page https://interactivebrokers.com/en/accounts/fees/CME.php (non-member Globex E-mini equity USD 1.386 per search excerpt), Topstep fee article https://intercom.help/topstep-llc/en/articles/8284231 (ES exchange fee USD 2.76 round turn, MES USD 0.70, Feb 2025); CME's own fee schedule NOT retrieved (W78B-D04)

Mechanism: Tiered discounts (documented for equity member firms in 2015 notice per search excerpt) change marginal fee with month-to-date volume; strategy volume planning should include tier thresholds. Current schedule UNVERIFIED.

Features: marginal_fee(vol_mtd); thresholds from schedule.

Target: Fee variance across the month.

Falsify-if: No tier structure applies to our membership class.

Horizon: DAILY
Availability: PUBLIC_SCHEDULED
Priority: B

## W78B-E35 — Regulatory And Clearing Fee Stack Reconciliation

Primary source: Public fee evidence: Interactive Brokers CME fee pass-through page https://interactivebrokers.com/en/accounts/fees/CME.php (non-member Globex E-mini equity USD 1.386 per search excerpt), Topstep fee article https://intercom.help/topstep-llc/en/articles/8284231 (ES exchange fee USD 2.76 round turn, MES USD 0.70, Feb 2025); CME's own fee schedule NOT retrieved (W78B-D04)

Mechanism: All-in per-side cost = exchange (Globex) + clearing + NFA regulatory (~USD 0.02 per side per secondary sources) + broker commission. Reconciling statements to model prevents hidden drift.

Features: stack_model vs statement per fill; residual in cents.

Target: Reconciliation residual.

Falsify-if: Residual >2% of stack for more than 5% of fills (then model incomplete).

Horizon: DAILY
Availability: PUBLIC_SCHEDULED
Priority: B+

## W78B-E36 — Fee Schedule Change Event Study

Primary source: Public fee evidence: Interactive Brokers CME fee pass-through page https://interactivebrokers.com/en/accounts/fees/CME.php (non-member Globex E-mini equity USD 1.386 per search excerpt), Topstep fee article https://intercom.help/topstep-llc/en/articles/8284231 (ES exchange fee USD 2.76 round turn, MES USD 0.70, Feb 2025); CME's own fee schedule NOT retrieved (W78B-D04)

Mechanism: CME transaction fee changes are announced by Special Executive Reports (e.g., SER-6913 in 2014 and SER-9050 in 2022 surfaced in search; contents only partly read) and step-change net edge for marginal strategies.

Features: event dates; compute hurdle_ticks pre/post; strategies near zero edge flagged.

Target: Net edge change.

Falsify-if: No fee notices affecting our products in last 24 months (then edge is dormant).

Horizon: SLOW_PRIOR
Availability: PUBLIC_SCHEDULED
Priority: B

## W78B-E37 — Market-Data Fee Fixed-Cost Breakeven

Primary source: CME January 2026 Market Data Fee List, https://www.cmegroup.com/market-data/files/january-2026-market-data-fee-list.pdf (contents not read) (W78B-D05)

Mechanism: Market data fees are fixed monthly costs; capacity needs to cover them. Fee-list contents not read; breakeven requires actual professional/non-professional status and display classification.

Features: break_even_trades = fixed_data_cost / net_edge_per_trade_usd.

Target: Minimum trade count for profitability.

Falsify-if: Data cost <1% of expected monthly gross edge (then irrelevant).

Horizon: SLOW_PRIOR
Availability: PUBLIC_SCHEDULED
Priority: B

## W78B-E38 — Spread Capture Ratio

Primary source: Perold, The implementation shortfall: paper versus reality, J. Portfolio Management 14(3), 1988 (classical; bibliographic detail PROVENANCE_PENDING) (W78B-D01)

Mechanism: Spread capture ratio = realized spread / quoted spread for passive fills; reveals how much of the spread is retained after adverse selection.

Features: SCR = real_spread_30s / quoted_spread; distribution by state.

Target: Share of spread retained.

Falsify-if: SCR indistinguishable from 0 or negative in typical states (so posting is not paid).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E39 — Cross-Asset Fee Per Sigma Ranking

Primary source: CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W78B-D08) + CME ZN/CL/GC contract spec pages (see W78B-D19), tick: ZN 1/64 pt, CL $0.01, GC $0.10

Mechanism: Fee per contract vs tick value vs volatility determines which instruments are cheap to trade at a given horizon; normalizes ES/NQ/GC/ZN/CL.

Features: fee_sigma = fee_rt/(sigma_1min*multiplier).

Target: Instrument ranking.

Falsify-if: Ranking equals slippage-only ranking (then fee layer adds nothing).

Horizon: DAILY
Availability: PUBLIC_SCHEDULED
Priority: B

## W78B-E40 — Sunday Reopen Liquidity Ramp

Primary source: CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W78B-D08)

Mechanism: Globex trading resumes Sunday 6:00 pm ET and daily 5-6 pm ET maintenance breaks (spec). First minutes after reopening have thinner books and gap risk; cost multiplier m(t_since_open).

Features: slippage and spread vs minutes since 18:00 ET Sunday and daily reopen.

Target: Ramp curve to baseline.

Falsify-if: Spread/slippage at +1 minute equal to baseline.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E41 — Pre-Maintenance Flattening Cost

Primary source: CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W78B-D08)

Mechanism: Daily maintenance 5-6 pm ET (4-5 pm CT) creates a hard boundary; flattening in the last minutes faces thinning books. Cost curve of holding vs flattening.

Features: slippage for exit orders in last 15 minutes before 17:00 ET vs earlier.

Target: Cost multiplier.

Falsify-if: No cost difference vs matched earlier windows.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W78B-E42 — RTH Open And Close Transition Liquidity

Primary source: CME S&P 500 Price Limits FAQ, https://www.cmegroup.com/trading/equity-index/sp-500-price-limits-faq.html (W78B-D13)

Mechanism: Cash equity open/close (08:30 and 15:00 CT) and the settlement VWAP window create liquidity step changes in ES/NQ.

Features: depth/spread/volume profile around 08:30, 14:59:30-15:00, 15:00 CT; cost multipliers.

Target: Cost multipliers by minute.

Falsify-if: Profile flat within +/-10% of adjacent segments.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E43 — Overnight Session Cost Multiplier

Primary source: CME S&P 500 Price Limits FAQ, https://www.cmegroup.com/trading/equity-index/sp-500-price-limits-faq.html (W78B-D13)

Mechanism: Overnight ES carries tighter price limits (7% with dynamic breakers) and thinner books; costs scale. Ratio overnight/RTH of spread, depth, slippage.

Features: mult = cost_overnight/cost_RTH by instrument and sub-session (Asia, Europe open).

Target: Multiplier table.

Falsify-if: Multipliers < 1.1 for all instruments.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E44 — Quarterly Equity-Index Roll Liquidity Crossover

Primary source: CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W78B-D08)

Mechanism: ES/NQ quarterly contracts terminate 9:30 a.m. ET on 3rd Friday (ES spec); liquidity migrates to next contract before expiry. Holding or trading the expiring contract after volume crossover pays higher costs.

Features: crossover date = first day next-contract volume > front; costs of front vs next in the 10 days before expiry.

Target: Cost difference around crossover; cost of holding front after crossover.

Falsify-if: Front-month costs do not exceed next-month costs after crossover.

Horizon: DAILY
Availability: PAID_REALTIME
Priority: A+

## W78B-E45 — ZN Roll Window Cost And Message Constraint

Primary source: CME ZN/CL/GC contract spec pages (see W78B-D19), tick: ZN 1/64 pt, CL $0.01, GC $0.10 + CME Globex Messaging Efficiency Program, https://cmegroup.com/globex/trade-on-cme-globex/messaging-efficiency-program.html (W78B-D06)

Mechanism: Treasury futures have a roll window before First Notice; CME applies a roll volume-ratio benchmark for 5/10Y notes (secondary source). Costs and quoting policy change.

Features: ZN slippage vs days to FND; roll_ratio vs 3000 benchmark.

Target: ZN cost curve by days to FND.

Falsify-if: No cost elevation in last 10 trade dates before FND.

Horizon: DAILY
Availability: PAID_REALTIME
Priority: B+

## W78B-E46 — CL Expiry-Week Execution Cost Curve

Primary source: CME ZN/CL/GC contract spec pages (see W78B-D19), tick: ZN 1/64 pt, CL $0.01, GC $0.10

Mechanism: WTI front month approaches expiry with volatility and delivery-related flow (W49P physical delivery wave owns delivery mechanics); here only execution cost vs days to expiry. Last trade date rule UNVERIFIED.

Features: slippage, depth, spread vs days to expiry; CL front vs second month.

Target: Cost curve.

Falsify-if: Costs flat through expiry week.

Horizon: DAILY
Availability: PAID_REALTIME
Priority: B+

## W78B-E47 — GC Active-Month Roll Cost

Primary source: CME ZN/CL/GC contract spec pages (see W78B-D19), tick: ZN 1/64 pt, CL $0.01, GC $0.10

Mechanism: Gold futures liquidity concentrates in specific months (UNVERIFIED which); roll cost depends on migration. Link to W56G global bullion mechanics for physical flows.

Features: cost vs month-type; calendar spread liquidity.

Target: Cost curve.

Falsify-if: No difference across months.

Horizon: DAILY
Availability: PAID_REALTIME
Priority: B

## W78B-E48 — Scheduled-Event Slippage Multiplier

Primary source: CME S&P 500 Price Limits FAQ, https://www.cmegroup.com/trading/equity-index/sp-500-price-limits-faq.html (W78B-D13)

Mechanism: Scheduled macro releases (owned by other waves) change spread and depth within seconds; here only execution multiplier and pre-release withdrawal. Extension: execution cost, not directional alpha.

Features: mult(t - release_time) for t in [-300s, +600s]; withdrawal onset.

Target: Multiplier curve per event class.

Falsify-if: Multiplier ~1 around releases.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E49 — Holiday And Early-Close Session Cost

Primary source: CME holiday and trading hours calendar (cmegroup.com; exact page not retrieved) (W78B-D20)

Mechanism: Reduced-hours and holiday sessions have thinner books; costs scale. CME holiday calendar must be versioned.

Features: mult_holiday vs normal day; early-close timing.

Target: Cost multiplier.

Falsify-if: Cost on holiday sessions equals normal sessions.

Horizon: DAILY
Availability: PUBLIC_SCHEDULED
Priority: B+

## W78B-E50 — Calendar-Spread Fair-Carry Deviation As Roll Cost

Primary source: CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W78B-D08)

Mechanism: Spread price vs cost-of-carry fair value (W55T treasury financing / W63M margin own adjacent mechanics) deviation measures roll cost beyond execution.

Features: dev = spread - fair_carry; roll_cost_extra.

Target: Roll cost residual.

Falsify-if: |dev| < 1 tick always.

Horizon: DAILY
Availability: PAID_REALTIME
Priority: B

## W78B-E51 — US-EU DST Mismatch Liquidity Timing Shift

Primary source: CME S&P 500 Price Limits FAQ, https://www.cmegroup.com/trading/equity-index/sp-500-price-limits-faq.html (W78B-D13)

Mechanism: US and EU DST transitions differ by weeks, shifting relative timing of European open versus US releases for rates/CL; cost windows shift.

Features: cost profile by ET-minute during mismatch weeks vs normal.

Target: Profile shift.

Falsify-if: Cost minute-profile unchanged in mismatch weeks.

Horizon: DAILY
Availability: PAID_REALTIME
Priority: B

## W78B-E52 — Depth Collapse Regime Detector

Primary source: Global Trading, S&P500 futures liquidity declined 90% at height of tariff turmoil, https://www.globaltrading.net/?p=38057 (W78B-D15; trade press, secondary) + Quantitative Brokers, Liquidity of E-mini S&P 500 futures 2012-2018, https://quantitativebrokers.com/market-updates/liquidity-of-e-mini-sp-500-futures-from-2012-2018 (W78B-D14; content not read)

Mechanism: Trade press reports large depth reductions during stress (April 2025 ~90% per headline; March 2020). Regime detector from own book data triggers size reduction.

Features: depth_pctile < p; spread blow-out; slippage multiplier forecast.

Target: Slippage tail in detected regime.

Falsify-if: Detector fires without slippage uplift (false-alarm ratio >80%).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E53 — Fill-Model Reality Gap

Primary source: Moallemi, Yuan, A model for queue position valuation in a limit order book (Columbia GSB WP 2017) (W78B-D11)

Mechanism: Backtests using touch-fill assumptions overstate passive fills. Reality gap = backtest fill rate/markout vs live shadow by queue rank.

Features: gap = (sim_fill_rate - live_fill_rate)/live_fill_rate by q_rank; markout gap.

Target: Backtest-to-live degradation.

Falsify-if: Gap below 5% after queue-aware model (otherwise model rejected).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: S-

## W78B-E54 — Touch-Fill Versus MBO-Aware Fill Bias

Primary source: Moallemi, Yuan, A model for queue position valuation in a limit order book (Columbia GSB WP 2017) (W78B-D11)

Mechanism: Touch-fill (fill when price trades through) vs MBO-aware (fill only if queue ahead is exhausted) differ in sign of PnL for marginal strategies.

Features: PnL under both; difference by strategy.

Target: Sign flips under realistic fill model.

Falsify-if: No strategy changes sign.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E55 — Cost-Model Drift CUSUM Gate

Primary source: Perold, The implementation shortfall: paper versus reality, J. Portfolio Management 14(3), 1988 (classical; bibliographic detail PROVENANCE_PENDING) (W78B-D01)

Mechanism: Cost models drift with microstructure changes (tick/NRR/fee changes). CUSUM on cost residuals triggers re-estimation or size cut.

Features: CUSUM on e_t = slip_t - E[slip|state]; threshold h.

Target: Time to detect drift.

Falsify-if: Alarm fraction under planted drift < 50% (detector underpowered).

Horizon: DAILY
Availability: PAID_REALTIME
Priority: A

## W78B-E56 — Cost-Aware Signal Gate With Random-Gate Control

Primary source: Perold, The implementation shortfall: paper versus reality, J. Portfolio Management 14(3), 1988 (classical; bibliographic detail PROVENANCE_PENDING) (W78B-D01) + Cont, Kukanov, Stoikov, arXiv:1011.6402 (W78B-D16)

Mechanism: Trade only if expected alpha exceeds k * expected cost(state). Control: random gate with same trade count.

Features: gate_on = alpha_hat > k*Q_0.75(cost|x); compare net PnL vs random gate.

Target: Net PnL difference versus random gate.

Falsify-if: Net PnL gate not better than random gate at 5% (bootstrap).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: S-

## W78B-E57 — Tail-Quantile Cost For Exit Sizing

Primary source: Kirilenko, Kyle, Samadi, Tuzun, The Flash Crash, J. Finance 72(3) (W78B-D21)

Mechanism: Position sizing and stop placement should use q90-q99 cost, not mean, because exits happen in stress.

Features: size such that loss at q95 cost <= risk budget.

Target: Realized max exit cost vs budget.

Falsify-if: Realized exit cost exceeds q95 forecast >10% of time.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E58 — Cost Model Transfer E-Mini To Micro

Primary source: CME E-mini S&P 500 contract specs, https://www.cmegroup.com/markets/equities/sp/e-mini-sandp500.contractSpecs.html (W78B-D08)

Mechanism: Micro contracts share underlying but not book; test whether ES cost model scaled by notional predicts MES costs.

Features: ratio_realized/predicted for MES using ES model; CI.

Target: Transfer error.

Falsify-if: Ratio outside [0.8,1.25].

Horizon: DAILY
Availability: PAID_REALTIME
Priority: B

## W78B-E59 — Slippage Attribution: State vs Own Impact vs Latency

Primary source: Almgren, Chriss, Optimal execution of portfolio transactions, J. Risk 3(2), 2000 (classical; PROVENANCE_PENDING) (W78B-D02) + Lehalle, Mounjid, arXiv:1610.00261 (W78B-D09)

Mechanism: Decompose slippage variance into market state, own size, and latency to guide where engineering effort pays.

Features: Shapley/variance decomposition of slippage on (state, size/D1, A).

Target: Shares of variance.

Falsify-if: One component explains <5% in all instruments.

Horizon: DAILY
Availability: PAID_REALTIME
Priority: A-

## W78B-E60 — Execution-Quality Score As Risk Throttle

Primary source: Perold, The implementation shortfall: paper versus reality, J. Portfolio Management 14(3), 1988 (classical; bibliographic detail PROVENANCE_PENDING) (W78B-D01)

Mechanism: Rolling markout z-score of last N fills as live execution-quality score; sharp deterioration throttles size or switches to conservative order types.

Features: z_t = (mean markout_N - mu_ref)/(sd_ref/sqrt(N)); throttle when z<-z*.

Target: Subsequent cost reduction vs unthrottled.

Falsify-if: Throttled and unthrottled cost equal (placebo: random throttle).

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A

## W78B-E61 — Imbalance-Triggered Taker Timing

Primary source: Cont, Kukanov, Stoikov, arXiv:1011.6402 (W78B-D16) + Bechler, Ludkovski, Optimal Execution with Dynamic Order Flow Imbalance, arXiv:1409.2618 (W78B-D10)

Mechanism: Optimal execution with dynamic order-flow imbalance suggests accelerating/decelerating by OFI; test simple rule: delay marketable child if OFI adverse and resilience short.

Features: delay_i = f(OFI,tau); compare cost to immediate send.

Target: Cost improvement per child.

Falsify-if: Cost not lower than immediate execution net of delay opportunity cost.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: A-

## W78B-E62 — Cancel-Replace In-Flight Mitigation Loss

Primary source: CME iLink Order Types, https://cmegroupclientsite.atlassian.net/wiki/spaces/EPICSANDBOX/pages/457227032/iLink+Order+Types (W78B-D07)

Mechanism: Cancel-replace with in-flight fills creates exposure risk; cost of mismatched quantity events and rejects.

Features: in-flight fill incidence per modification; extra exposure contracts.

Target: Exposure error rate.

Falsify-if: No in-flight fills in logs.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B

## W78B-E63 — Passive Exit Opportunity: Take-Profit Limit Fill Quality

Primary source: Moallemi, Yuan, A model for queue position valuation in a limit order book (Columbia GSB WP 2017) (W78B-D11)

Mechanism: Take-profit limits fill passively at favorable level but with adverse selection after fill; compare to marketable take-profit.

Features: markout after TP fill vs after marketable TP.

Target: Net exit value.

Falsify-if: No difference in net exit value.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W78B-E64 — Queue-Jump Via Spread Improvement Cost

Primary source: Dayri, Rosenbaum, arXiv:1207.6325 (W78B-D17)

Mechanism: Improving price by one tick (jumping queue) costs one tick but gains priority; value depends on large-tick regime.

Features: value_improve = Δp_fill*gain - tick; by state.

Target: Net value of price improvement.

Falsify-if: Never positive in any state bucket.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B+

## W78B-E65 — Order Resting-Time Alpha Decay Cap

Primary source: Lehalle, Mounjid, arXiv:1610.00261 (W78B-D09)

Mechanism: Resting beyond signal half-life converts alpha entry into noise exposure; cancel-time cap from tau.

Features: cap = c*tau; cost with/without cap.

Target: Cost and fill change.

Falsify-if: No difference.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B

## W78B-E66 — Multi-Instrument Basket Execution Skew

Primary source: Cont, Kukanov, Stoikov, arXiv:1011.6402 (W78B-D16)

Mechanism: Executing ES and NQ legs sequentially leaves leg risk; order and timing determine cost.

Features: skew_cost by order of legs; correlation of slippage.

Target: Leg cost asymmetry.

Falsify-if: No leg-order effect.

Horizon: INTRADAY
Availability: PAID_REALTIME
Priority: B

## Final architecture edge (Truth Ladder)

The Truth Ladder for W78B: (1) rule/fee/spec fact versioned by effective date; (2) own order-and-fill telemetry reconciled to exchange drop-copy/statement; (3) reconstructed counterfactual (what a touch, MWP, or queue-aware fill would have been) using W70B book state; (4) state-conditional cost model with calibration and monotonicity diagnostics; (5) decision rules (post vs take, order type, slicing, gating) evaluated against random-gate and always-aggressive controls; (6) only then any net-of-cost return claim.

## Highest-priority W78B tests

1. W78B-E05 Slippage-By-State Quantile Surface
2. W78B-E09 Fill-Conditional Adverse Selection Curve
3. W78B-E12 Passive-vs-Aggressive Decision Boundary
4. W78B-E06 Cost Monotonicity Test (Size, Urgency, Spread)
5. W78B-E28 Signal Half-Life Latency Tolerance
6. W78B-E44 Quarterly Equity-Index Roll Liquidity Crossover
7. W78B-E19 Exit Order Type Under Gap: Stop vs Stop-Limit vs Stop-Protection
8. W78B-E53 Fill-Model Reality Gap
9. W78B-E56 Cost-Aware Signal Gate With Random-Gate Control
10. W78B-E03 Realized-Spread / Price-Impact Fill Decomposition
