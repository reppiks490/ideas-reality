# Wave 81E — Equity Index Structure, Auctions and ETF Plumbing

Namespace: **W81E**

Thesis: equity index futures (ES, NQ) are priced off a cash basket whose price formation concentrates in opening and closing auctions, a small number of mega-cap constituents, an ETF primary-market arbitrage, and regulator-mandated data with known publication clocks. The edge is the live, venue-specific auction information state (NYSE Pillar and Nasdaq NOII fields, cutoffs, cadences), index concentration and constraint proximity, ETF plumbing disclosures, and the legal timestamps of SEC/FINRA data, used as regime, risk-gate, execution-quality and entry-confirmation state in the last and first minutes of the cash session.

Boundary: W26R owns rebalance and forced-flow edges (S&P, Nasdaq-100, Russell changes, weight-cap redistribution E09, fast entry E08, auction imbalance amplification E19, ETF creation/redemption confirmation E17, fund-vs-index gap E18); W27V owns LULD, halts, reopening, Rule 201 and market-wide circuit breaker state; W33S owns FTD, threshold lists, short interest, off-exchange short-sale ratio per name (E15); W69O owns options expiry and gamma effects; W70B owns Globex book mechanics; W78B owns execution-quality ledgers; W73E owns macro release clocks. W81E adds live auction information states on non-rebalance days, concentration state, ETF disclosure plumbing, and data-legality clocks, and states the increment against these waves where they touch.

All candidates are research hypotheses only. Claude owns later implementation.

## W81E-E01 — NYSE 3:50 Regulatory Imbalance Direction Persistence

Primary source: NYSE opening and closing auctions fact sheet https://www.nyse.com/publicdocs/nyse/NYSE_Auctions_Closing_Process_Fact_Sheet.pdf (read: MOC/LOC cutoff 3:50 p.m., systemic MOC/LOC Significant Imbalance released at 3:50, only offsetting orders thereafter); NYSE Pillar Order Imbalances Client Specification v2.2k (read)

Mechanism: After 3:50 NYSE-listed MOC/LOC interest cannot be added on the imbalance side, so imbalance side at 3:50 is partially locked in and only contra interest can respond. Direction of the 3:50 imbalance may predict close-versus-3:50 price displacement if offset supply is price-elastic only at worse prices.

Features: imb_side_i, imb_qty_i/ADV20_i, weight_i; aggregate WIP = sum_i w_i * sign_i * imb_qty_i / ADV20_i (see E05).

Target: r_{3:50 mid..auction print} per name; ES/NQ return 15:50-16:00.

Falsify-if: Correlation of WIP with 3:50-4:00 ES return not above that of last-10-minute momentum alone and not above placebo using shuffled days.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S

## W81E-E02 — Nasdaq Closing Information Step Clock

Primary source: Nasdaq Closing Cross FAQ https://www.nasdaqtrader.com/content/productsservices/Trading/ClosingCrossfaq.pdf (read; dated 2019: early dissemination 3:50, NOII every 10 seconds 3:50-3:55, every second 3:55-4:00, MOC stop 3:55, LOC entry to 3:58, IO to 4:00); current rule text PROVENANCE_PENDING

Mechanism: Information arrives in steps (3:50, 3:55, 3:58). Features should be indexed to the step, because cancel/modify rights and order-type availability change at each step; a model that ignores steps mixes states.

Features: step_id in {S0 pre-3:50, S1 3:50-3:55, S2 3:55-3:58, S3 3:58-4:00}; time since last step; NOII update frequency.

Target: Return and imbalance revision by step.

Falsify-if: Step-conditional models do not beat a single time-of-day model out-of-sample, or the live rulebook changed the steps (then edge retired).

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W81E-E03 — Near-Versus-Far Indicative Clearing Gap

Primary source: Nasdaq FAQ and NOII spec https://www.nasdaqtrader.com/content/technicalsupport/specifications/dataproducts/Noiview-v2spec.pdf (read: Far Price = cross orders only; Near Price = cross plus continuous orders; Current Reference Price; Cross Type O/C/H)

Mechanism: Far price reflects auction-only interest; near price adds continuous book. A wide near-far gap means closing interest alone would clear far from where continuous liquidity would absorb it, i.e. the book is doing the offsetting.

Features: gap_i = (Near_i - Far_i) / Ref_i; index-weighted mean and dispersion; sign.

Target: Price move from 3:55 to official close relative to Near-Ref.

Falsify-if: Near price at 3:55 is no better predictor of the official close than current reference price.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W81E-E04 — Price Variation Indicator Extremes Breadth

Primary source: Nasdaq NOII spec (read): Price Variation Indicator L, 1..9, A (10-19.99%), B, C (30%+) of near price vs reference

Mechanism: The indicator is a categorical measure of how far the indicated cross is from reference. Breadth of high categories across index names is a stress state.

Features: pv_cat_i mapped to numeric bucket; share of index weight with bucket >= k.

Target: Realized 15:55-16:00 index volatility and close-to-reference displacement.

Falsify-if: Weighted share with high bucket does not add to E05 after controlling for imbalance size.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W81E-E05 — Index-Weighted Imbalance Pressure (WIP)

Primary source: NYSE Pillar order imbalances feed (fields: ImbalanceSide, PairedQty, TotalImbalanceQty, UnpairedQty; read); Nasdaq NOII feed (Paired Shares, Imbalance Shares, Imbalance Direction; read); constituent weights from index provider (PROVENANCE_PENDING for licensed weights)

Mechanism: Closing imbalances on constituents aggregate into an index-level forced-flow estimate; futures trade through 4:00 (and to 4:15 per CME hours PROVENANCE_PENDING) so the aggregate maps to ES/NQ. Boundary: W26R-E03 owns rebalance-day ratio and E19 amplification; this edge is the daily live aggregate for non-rebalance days.

Features: WIP_idx = sum_i w_i * (imb_signed_i / ADV20_i) with cap and winsor; separate NYSE and Nasdaq components.

Target: ES/NQ return from 15:50 to 16:00 and 16:00 to 16:15 (if tradable); sign.

Falsify-if: WIP sign has zero predictive relation with futures returns; magnitude relation absent after cost.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S

## W81E-E06 — Imbalance Revision Path 3:50 to 3:59

Primary source: NYSE and Nasdaq imbalance feeds (every second if changed; read)

Mechanism: If offsetting liquidity arrives, the imbalance shrinks and price pressure dissipates; if it grows, pressure persists. The path of revisions is more informative than the level.

Features: d_imb = imb_3:59 - imb_3:50 (signed, scaled); slope; fraction of names with shrinking imbalance.

Target: Return from 3:59 to close; official close minus 3:59 mid.

Falsify-if: Revision slope has no conditional predictive power for residual price move beyond E01.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A+

## W81E-E07 — NYSE Unpaired Quantity Residual

Primary source: NYSE Pillar spec v2.2k: Unpaired Qty and Unpaired Side fields (number of unpaired shares priced at or better than reference, closing auction only; read)

Mechanism: Unpaired shares at the reference price indicate liquidity needed beyond what is paired; relevant even if total imbalance is similar.

Features: unpaired_i/total_imb_i; side.

Target: Close vs reference price slippage for MOC buyers.

Falsify-if: Unpaired fraction has no incremental explanatory power over total imbalance.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W81E-E08 — Continuous-Book Clearing Distance

Primary source: NYSE Pillar spec: ContinuousBookClearingPrice (price closest to reference where imbalance is zero), AuctionInterestClearingPrice; defaulted to 0 for regulatory imbalances (read)

Mechanism: Distance from reference to the price where the imbalance is zero is the price move needed to clear; normalized by volatility gives a state of required concession.

Features: cbc_dist_i = (CBC_i - Ref_i)/(ATR_i); handle zeros (undefined) as missing not zero.

Target: Official close relative to reference price.

Falsify-if: Official close does not move toward CBC beyond chance.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W81E-E09 — Significant-Imbalance Flag Breadth

Primary source: NYSE Pillar spec: Significant Imbalance indicator (Y when continuous book clearing price is more than a significant range from reference; for Auction Types C or P in NYSE-listed symbols; read); fact sheet: systemic publication at 3:50

Mechanism: A flag is a compact stress measure per name. Breadth across the index weights is an index-level stress state.

Features: share_sig = sum_i w_i * 1[sig_i = Y]; count and concentration.

Target: ES 15:50-16:00 realized volatility and absolute return.

Falsify-if: Breadth is uninformative after controlling for E05.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W81E-E10 — Extreme Closing Imbalance Event (Auction Type P) Aftermath

Primary source: NYSE Pillar spec: AuctionType P Extreme Closing Imbalance (NYSE only); TotalImbalanceQty = extreme order imbalance quantity (read)

Mechanism: An extreme imbalance event signals unusual one-sided demand; overnight/next-open reversion is the competing hypothesis.

Features: P_count, side, weighted share.

Target: Next-day open gap relative to close; 1-day continuation.

Falsify-if: No reversal or continuation distinguishable from zero.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W81E-E11 — Contra-Side Offset Supply Elasticity

Primary source: NYSE fact sheet (read): after 3:50 only contra-side MOC/LOC entry; Closing Offset orders yield to all other interest and never add to imbalance; cancellations after 3:50 restricted

Mechanism: The speed at which contra interest arrives after 3:50 reveals the elasticity of offsetting supply; elasticity is a state.

Features: e = -d(imb)/d(price concession) estimated from 3:50-3:58 path per name, pooled.

Target: Residual close concession versus predicted.

Falsify-if: Pooled elasticity does not vary with VIX or time-of-month.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W81E-E12 — Listing-Venue Imbalance Split (ES versus NQ Relative)

Primary source: NYSE Pillar and Nasdaq NOII feeds; listing exchange of each constituent

Mechanism: NQ is dominated by Nasdaq-listed names and ES includes many NYSE-listed names; venue-specific imbalances differ and may produce relative moves between ES and NQ in the last 10 minutes.

Features: WIP_nyse, WIP_nasdaq; spread = WIP_nasdaq - WIP_nyse.

Target: NQ-minus-ES beta-adjusted return 15:50-16:00.

Falsify-if: Spread has no relation with relative return.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W81E-E13 — Opening Imbalance Aggregate and Gap Resolution

Primary source: NYSE fact sheet: opening information from 8:00 a.m. every second until stock opens; Pillar spec: core opening auction 8:00 to open; Arca/American windows; boundary: W73E-E54 uses 8:30 shocks

Mechanism: Aggregate opening imbalance for the index indicates whether the 9:30 cash open confirms or fades the futures-implied gap.

Features: OIM = sum_i w_i * open_imb_i / ADV; indicative match price vs previous close; gap_ES at 9:29.

Target: ES return 9:30-10:00; gap closing fraction.

Falsify-if: OIM adds nothing to gap_ES alone.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W81E-E14 — NYSE Manual-Open Share

Primary source: NYSE fact sheet (read): securities able to open within 10% of reference can be opened algorithmically by the DMM; outside that range, manual

Mechanism: Names that need manual opens open later and with more uncertainty; the weighted share of manual opens is a delayed-open stress state. Boundary: W27V-E12 reopening gaps are halts; this is the ordinary open.

Features: time_to_open_i, manual_flag_i (inferred from open delay), weight share not yet opened at t.

Target: ES-SPX basis noise and 9:30-9:35 volatility.

Falsify-if: Weighted delayed-open share not related to basis dispersion.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W81E-E15 — Closing-Auction Share of Volume Regime

Primary source: Nasdaq FAQ (read): almost 10% of Nasdaq ADV occurs in closing auction; Bogousslavsky and Muravyev, Journal of Financial Markets 66 (2023) (title confirmed via search; seminar abstract of working paper states 7.3% of daily volume in 2018, strongly associated with ETF ownership; PARTIAL)

Mechanism: A rising closing-auction share concentrates price formation in one print; informativeness of the close for next-day price may fall.

Features: cas_t = auction volume/daily volume per name and index-weighted; z-score vs trailing 60 days.

Target: Next-day open-to-first-hour return conditional on cas z and imbalance.

Falsify-if: cas has no relation with next-day reversal after controlling for imbalance and return.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A-

## W81E-E16 — Close-to-Open Reversal Conditional on Imbalance

Primary source: Nasdaq/NYSE closing imbalance feeds; Bogousslavsky-Muravyev (price pressure at the close; PARTIAL)

Mechanism: If the close is displaced by uninformed flow, the next open partially reverses; if informed, it continues. The sign is regime dependent.

Features: signed (close - 15:50 mid) normalized; imbalance size; next-open gap.

Target: Next-day open return versus the displacement.

Falsify-if: No reversal after cost; sign inconsistent across regimes.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: A

## W81E-E17 — Close-Print Displacement Versus 15:59 Reference

Primary source: NYSE/Nasdaq official close; consolidated tape; Nasdaq Official Close Price (NOCP) defined in FAQ (read)

Mechanism: Displacement of auction print from the last continuous price measures realized auction impact and cost for MOC participants.

Features: disp_i = (NOCP_i - mid_{15:59:59})/spread; index-weighted.

Target: Cost of MOC execution; next-day reversal.

Falsify-if: disp is indistinguishable from noise relative to pre-auction spread.

Horizon: DAILY

Availability: PAID_REALTIME

Priority: B+

## W81E-E18 — Early-Close Compressed Auction Clock

Primary source: NYSE Pillar spec v2.2k (read): on early closing days the Arca/American closing auction runs 12:00 to 1:00 pm and NYSE closing auction runs from 12:50; holiday calendar for early closes PROVENANCE_PENDING

Mechanism: Early closes compress schedule and may thin liquidity; all hard-coded 3:50/4:00 times fail.

Features: schedule_offset computed from exchange calendar; early_close_flag.

Target: Auction share, imbalance revision, slippage.

Falsify-if: Early-close days indistinguishable after scaling by offset.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B+

## W81E-E19 — Post-Auction Futures Reaction to Official Close

Primary source: CME equity index futures hours (PROVENANCE_PENDING; CME trading hours page returned 503); NYSE/Nasdaq official close

Mechanism: Futures can trade after cash close; the first futures reaction after the official close reveals whether auction print surprised relative to futures-implied fair value.

Features: fair_value_gap = ES_{16:00:00} - basis-adjusted SPX_close_implied; sign.

Target: ES return 16:00-16:15 vs gap.

Falsify-if: Gap does not predict post-close return.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W81E-E20 — Pre-Auction Volume Deficit 15:30 to 15:50

Primary source: Own consolidated tape; auction timeline from NYSE fact sheet and Nasdaq FAQ (read)

Mechanism: Participants may defer to the auction (cutoff 3:50); lower continuous volume before the cutoff increases auction dependence.

Features: deficit = vol_{15:30..15:50} / median same window; plus cumulative auction share.

Target: Auction imbalance size; last-10-minute realized variance.

Falsify-if: deficit does not predict imbalance size or variance.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W81E-E21 — Nasdaq-100 Weight-Constraint Proximity Monitor

Primary source: Nasdaq-100 methodology https://indexes.nasdaqomx.com/docs/Methodology_NDX.pdf (read; copyright 2026): special rebalance if any weight exceeds 24% or aggregate weight of companies above 4.5% exceeds 48% (adjusted to 40%), based on end-of-day values; quarterly rebalance effective after third Friday; boundary: W26R-E09 owns weight-cap redistribution flows

Mechanism: The proximity of the 48% aggregate and 24% single-name limits is a slow state that conditions the probability of a special-rebalance announcement and subsequent forced flow; intraday it conditions megacap liquidity risk.

Features: A = sum_{w_i > 4.5%} w_i; distance (48% - A); max w_i vs 24%; daily changes; estimated from holdings.

Target: Probability of special rebalance within next 20 trading days; NQ response to announcement.

Falsify-if: Distance does not predict announcements (few events) - requires pooling with historical constraint breaches; if events fewer than minimum N, mark UNTESTABLE not failed.

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: A

## W81E-E22 — Nasdaq-100 IPO Reference-Clock

Primary source: Methodology (read): IPO ranked at end of seventh trading day; typically added after 15 trading days, announcement after tenth trading day; Fast Entry if rank in top 40 constituents by market cap; boundary: W26R-E08 owns pressure

Mechanism: The IPO timeline gives deterministic dates that condition auction flow for the new name and for peers; incremental is the deterministic clock itself.

Features: t_listing, day_7, day_10 announcement, day_15 effective; market cap rank vs 40th.

Target: Closing-auction share for the IPO name on effective day; peer reaction.

Falsify-if: No event of the type exists in sample or effect indistinguishable from zero.

Horizon: WEEKLY

Availability: PUBLIC_EVENT_DRIVEN

Priority: B

## W81E-E23 — Effective-N Concentration Slow Prior

Primary source: S&P Dow Jones Indices factsheet (official URL not fetched; third-party summaries report top-10 near 38-40 percent, figures PROVENANCE_PENDING); Nasdaq-100 methodology weights (read)

Mechanism: Higher concentration means index returns are driven by fewer names, so single-name news and auctions transmit more to NQ and ES.

Features: N_eff = 1/sum(w_i^2); top-3, top-10 weights; daily change.

Target: ES/NQ intraday variance explained by top-3 names.

Falsify-if: N_eff has no relation to explained variance after controlling for volatility.

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: A

## W81E-E24 — Top-Contributor Narrow-Move State

Primary source: Own constituent tape plus weights

Mechanism: When the top 3 contributors explain most of the index move, the move is fragile to idiosyncratic news and can reverse quickly.

Features: narrow = sum_{top3} contribution_i / index_move over trailing 15 minutes; contribution_i = w_i * r_i.

Target: Subsequent 15-minute reversal probability.

Falsify-if: narrow fails to predict reversal after controlling for vol and time of day.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W81E-E25 — Constituent Breadth Divergence ES versus NQ

Primary source: Own tape; weights

Mechanism: Index up with median constituent down indicates concentration-driven move; ES versus NQ breadth can diverge.

Features: median_ret, adv_decl_weighted, equal-weight minus cap-weight return.

Target: Next 30-minute index return and ES-NQ spread.

Falsify-if: No predictive content after controlling for narrow state.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W81E-E26 — Nasdaq-100 Closing-Value Correction Window

Primary source: Methodology (read): index disseminated once per second 09:30:01 to 17:16:00 ET; closing value may change up to 17:15:00 ET due to Last Sale corrections

Mechanism: Official closing value is not final at 4:00; late corrections shift settlement-relevant values.

Features: diff_close = official_final_close - first_published_close; frequency.

Target: Impact on tracking and next-day open reference.

Falsify-if: Differences are zero in all observed days (edge dead) or immaterial relative to tick size.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B

## W81E-E27 — Weighted After-Close Reporter Event Risk

Primary source: Earnings calendar (Alpha Vantage EARNINGS_CALENDAR tool or issuer IR; PROVENANCE_PENDING for use); constituent weights

Mechanism: Large after-close earnings from heavily weighted constituents create overnight risk that is index-weight-scaled and is known ahead.

Features: ER = sum_i w_i * expected_abs_move_i for reporters in the next evening; implied move from options PROVENANCE_PENDING.

Target: NQ overnight range and next-open gap.

Falsify-if: ER does not predict overnight range beyond calendar-day effects.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: A

## W81E-E28 — ES-NQ Shared Mega-Cap Factor Share

Primary source: Own constituent tape and weights; boundary: not a rebalance edge

Mechanism: ES and NQ overlap in mega-caps; their relative move depends on weights of shared names versus non-overlap names.

Features: shared_share = weight of overlapping names within each; residual after removing shared contribution.

Target: NQ-ES spread explained.

Falsify-if: Shared factor explains little of the spread.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W81E-E29 — Own-Computed Index Versus Official Second Lag

Primary source: Nasdaq-100 methodology (read: dissemination once per second); own constituent tick computation

Mechanism: Official index values update once per second; own computation from last sale is near real time; difference is a fair-value tracker and a staleness measure.

Features: fv_gap = own_index - official_index; staleness.

Target: Predictive power of fv_gap for next-second futures move.

Falsify-if: No incremental information beyond futures microprice.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W81E-E30 — Concentration Provenance Gate

Primary source: Multiple third-party concentration figures disagree (37.9, 38, 39.1, 40.7 percent top-10 at differing dates; PROVENANCE_PENDING)

Mechanism: Concentration claims from blogs are inconsistent; features must be computed from provider holdings with stated dates and share-class treatment.

Features: source_id, as_of, float vs full cap flag.

Target: Feature stability across providers.

Falsify-if: Computed N_eff differs materially across data vendors for the same date.

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B+

## W81E-E31 — Rule 6c-11 Premium/Discount Persistence Flag

Primary source: SEC small entity compliance guide https://www.sec.gov/investment/exchange-traded-funds-small-entity-compliance-guide (read: premium or discount above 2 percent for more than seven consecutive trading days triggers disclosure; website daily NAV, market price, premium or discount; effective Dec 23 2019)

Mechanism: Persistent premium/discount indicates impaired arbitrage; for sector ETFs and non-US underlyings it is a slow stress flag. Index ETFs rarely trigger it.

Features: pd_t = (price - NAV)/NAV (prior day); streak length; indicator for >2% and >7 days.

Target: Next-day ETF vs underlying basis; spread.

Falsify-if: Flag never triggers in sample for target ETFs (untestable) or has no relation to basis.

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B+

## W81E-E32 — ETF 30-Day Median Bid-Ask Spread Prior

Primary source: SEC compliance guide (read): median bid-ask spread over most recent 30 calendar days on website

Mechanism: A slow measure of ETF trading cost and liquidity quality; informs hedge instrument choice.

Features: med_spread_30d_i, change vs prior; ratio to futures tick cost.

Target: Realized execution cost of ETF hedges.

Falsify-if: Median spread is stale relative to same-day spread and gives no incremental predictive power.

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B

## W81E-E33 — Pre-Open Holdings Disclosure Clock

Primary source: SEC compliance guide (read): holdings used for NAV as of prior business day posted before regular trading opens on primary listing exchange

Mechanism: Daily holdings appear before the open; the disclosed portfolio vs index gives tracking gap; boundary: W26R-E18 owns the fund-vs-index gap; increment is disclosure timing.

Features: t_disclosure_i, holdings_hash, gap_vs_index.

Target: Opening ETF premium and tracking error.

Falsify-if: Disclosure time varies without relation to premium.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B

## W81E-E34 — iNAV Premium at 3:50

Primary source: ETF indicative NAV feed (vendor/exchange; PROVENANCE_PENDING)

Mechanism: If ETF price deviates from iNAV at the auction cutoff, authorized participants have arbitrage incentives that feed MOC flow.

Features: prem_350 = (ETF mid - iNAV)/iNAV.

Target: ETF auction imbalance; close premium.

Falsify-if: No relation with ETF auction imbalance.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W81E-E35 — ETF Flow Share of Closing Auction

Primary source: Bogousslavsky-Muravyev (PARTIAL: closing auction volume strongly associated with ETF ownership); constituent ETF ownership PROVENANCE_PENDING

Mechanism: Names with high ETF ownership have larger closing auction share and imbalance sensitivity to ETF flow days.

Features: etf_own_i * cas_i; ETF shares outstanding change (issuer data).

Target: Closing imbalance size scaled.

Falsify-if: No cross-sectional relationship after controlling for market cap.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B+

## W81E-E36 — Leveraged ETF End-of-Day Rebalance Estimate

Primary source: Cheng and Madhavan, The Dynamics of Leveraged and Inverse Exchange-Traded Funds, Journal of Investment Management 7(4) 2009 (abstract: daily reset can intensify late-day price swings; full text not read); holdings AUM from issuer sites PROVENANCE_PENDING; boundary: W77 covers volatility-product ETFs; this covers equity-index leveraged ETFs

Mechanism: Daily-reset leveraged ETFs must trade in the direction of the day's return near the close in proportion to leverage squared; the estimate is a known-direction late-day flow.

Features: reb_flow = sum_f AUM_f * (L_f^2 - L_f) * r_day (formula to verify against issuer methodology; PROVENANCE_PENDING); scaled by auction volume.

Target: ES/NQ return 15:30-16:00 residual.

Falsify-if: Estimated flow is too small relative to auction volume to move prices (untestable) or sign opposite.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W81E-E37 — Authorized Participant Order Cutoff Clock

Primary source: Issuer prospectuses (PROVENANCE_PENDING; typical cutoffs not verified)

Mechanism: Creation and redemption order cutoffs determine when primary-market arbitrage can be executed; cutoff alignment with auction closes.

Features: cutoff_time_i; time-to-cutoff.

Target: Premium/discount compression before cutoff.

Falsify-if: No behavior change around cutoff.

Horizon: INTRADAY

Availability: PUBLIC_SCHEDULED

Priority: B

## W81E-E38 — ETF-Future-Basket Lead-Lag Under Stress

Primary source: Own SPY/QQQ, ES/NQ and constituent tapes

Mechanism: Price discovery migrates among ETF, futures and cash basket when constituents are stale or stressed; the leader is a state. Boundary: W27V-E08 handles halts.

Features: hasbrouck_information_share_futures, etf, basket in 1-minute windows.

Target: Lead identity and next-minute return.

Falsify-if: Leader identity is unstable and unpredictive.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A-

## W81E-E39 — Custom-Basket Opacity Negative Control

Primary source: SEC compliance guide (read): custom baskets permitted under written policies; baskets exchanged are recorded, not published on website

Mechanism: Because custom baskets are not public, any attempt to infer AP basket composition is non-public inference and must be excluded. This is a boundary and negative control.

Features: none; exclude features requiring basket-level inference.

Target: Any feature requiring custom-basket data fails the confidentiality gate.

Falsify-if: Feature is built from public data only.

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B

## W81E-E40 — ETF Share of Underlying Volume

Primary source: Own tapes; ETF and constituent consolidated volumes

Mechanism: A rising ETF-to-underlying volume ratio signals that price discovery shifted into ETFs.

Features: ratio_t = ETF dollar volume / basket dollar volume.

Target: Next-hour basket return vs ETF return.

Falsify-if: No relation to subsequent basket convergence.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B

## W81E-E41 — FINRA Short Volume Publication Clock

Primary source: FINRA daily short sale volume files https://www.finra.org/finra-data/browse-catalog/short-sale-volume-data/daily-short-sale-volume-files (read: posted by 6:00:00 pm ET on trade date; may be updated later)

Mechanism: Same-day short volume is not available intraday; using it for an intraday decision is leakage. Legal only as next-session feature.

Features: published_time = 18:00 ET same day (upper bound).

Target: Next-day return/volume.

Falsify-if: Any intraday use of same-day file is a failed leakage test.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: A

## W81E-E42 — Index-Weighted Short-Volume Ratio Next-Day Signal

Primary source: FINRA daily files (read: aggregated short sale volume by security; consolidated NMS and TRF/ADF/ORF; boundary: W33S-E15 per-name off-exchange short-sale ratio)

Mechanism: Weighted ratio across index names is an index-level shorting activity gauge; increment is the aggregate.

Features: SVR_idx = sum w_i * short_vol_i / vol_i; z-score.

Target: Next-day ES/NQ open and close returns, sign ambiguous.

Falsify-if: No relation after cost; sign unstable.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B+

## W81E-E43 — SPY and QQQ Short-Volume Hedge Flow Ratio

Primary source: FINRA daily files; ETF tickers

Mechanism: Short volume in ETFs is partly hedging by market makers and APs, so its ratio is a flow gauge not bearishness. Sign ambiguous by design.

Features: SVR_ETF z-score and relation to creation/redemption days.

Target: Next-day ETF premium and returns.

Falsify-if: Ratio adds no information over ETF volume.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B

## W81E-E44 — Off-Exchange Share at the Close

Primary source: FINRA TRF files by venue (read: FNQC Nasdaq TRF Chicago, FNRA, FNSQ, FNYX, FORF files); consolidated NMS file CNMS

Mechanism: Off-exchange share may shift around the close; venue mix affects measurable liquidity and tape completeness.

Features: TRF share, ADF share, trend.

Target: Last-30-minute volatility.

Falsify-if: Share has no relation after controlling for volume.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B

## W81E-E45 — FINRA OTC and ATS Transparency Lag Prior

Primary source: FINRA OTC transparency pages (URL not fetched; PROVENANCE_PENDING)

Mechanism: ATS and non-ATS weekly volume is delayed; a slow prior only.

Features: dark_share_ticker_week.

Target: Next-month liquidity.

Falsify-if: No relation.

Horizon: SLOW_PRIOR

Availability: PUBLIC_DELAYED

Priority: B

## W81E-E46 — Short Interest Cycle Calendar

Primary source: FINRA short interest page returned HTTP 404 in this session; semi-monthly settlement cycle PROVENANCE_PENDING; boundary: W33S-E10..E13 own short interest

Mechanism: Short interest is a delayed snapshot; its calendar is a known timing state. Increment: clock only.

Features: settlement_date, publication_date, lag.

Target: None beyond W33S.

Falsify-if: Clock never aligns with any pattern.

Horizon: SLOW_PRIOR

Availability: PUBLIC_DELAYED

Priority: B

## W81E-E47 — Daily File Update and Correction Leakage

Primary source: FINRA daily files page (read: files may be updated later; updated versions labelled Updated; both appear)

Mechanism: Corrected files differ from first-posted values; research using final versions leaks.

Features: diff_first_vs_final.

Target: Backtest sensitivity.

Falsify-if: Differences are zero; vintage storage unnecessary.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B+

## W81E-E48 — Media-Reported Coverage Bias

Primary source: FINRA short sale volume files (read): includes only short sale trades reported for public dissemination; not consolidated with exchange data unless CNMS used

Mechanism: Coverage omissions can bias ratios; ratio of covered to total volume varies.

Features: covered_volume/consolidated_volume.

Target: Bias in SVR.

Falsify-if: Coverage ratio is stable and near one.

Horizon: DAILY

Availability: PUBLIC_BATCH

Priority: B

## W81E-E49 — Short-Volume Data Start-Date Constraint

Primary source: FINRA files (read: consolidated NMS files start Aug 1 2018; TRF Chicago Sept 10 2018)

Mechanism: Samples before Aug 2018 are not available; regime mixing with 2020 and 2022 limits power.

Features: sample_start; regime dummies.

Target: Estimated effect sensitivity to start date.

Falsify-if: Effect disappears when excluding the 2020 spike.

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B

## W81E-E50 — Stale-Open Weight Share

Primary source: NYSE fact sheet and Nasdaq opening; own constituent tapes; boundary: W27V-E05 covers halted names

Mechanism: At 9:30 some index constituents have not printed; cash index uses stale prices so ES-SPX basis is noisy in the first minutes.

Features: stale_w(t) = weight share without a trade since 9:30.

Target: |basis| and ES-implied cash gap.

Falsify-if: stale_w has no relation to basis noise.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: A

## W81E-E51 — Time-to-First-Print Weighted

Primary source: Own tape

Mechanism: Weighted time to first print is a continuous measure of opening completion; slower completion implies greater uncertainty.

Features: TTFP_idx = sum_i w_i * (t_first_print_i - 9:30).

Target: 9:30-10:00 volatility.

Falsify-if: No relation.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W81E-E52 — Arca-Listed ETF Early Closing Imbalance (from 3:00 p.m.)

Primary source: NYSE Pillar spec v2.2k (read): for Arca and American primary-listed securities, closing auction imbalance period 3:00 pm to 4:00 pm ET (NYSE-listed from 3:50)

Mechanism: SPY (NYSE Arca listed; confirm listing PROVENANCE_PENDING) gets imbalance information from 3:00 pm, 50 minutes before NYSE names; this earlier ETF imbalance may lead constituent closing flow.

Features: etf_imb at 3:00..3:50 for Arca-listed ETFs; sign and size.

Target: ES return 15:00-15:50 and later constituent imbalance at 3:50.

Falsify-if: ETF early imbalance does not predict constituent imbalance sign at 3:50.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S-

## W81E-E53 — Arca Early Opening Auction ETF Pre-Open

Primary source: NYSE Pillar spec v2.2k (read): Arca early opening auction period 3:30 am to 4:00 am ET for auction eligible securities; American 6:30 to 7:00

Mechanism: ETF pre-open auctions provide early US-equity indications before the regular session.

Features: early_open_imbalance_etf; overnight gap alignment.

Target: Overnight ES gap prior to 9:30.

Falsify-if: No relation.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: B+

## W81E-E54 — T+1 Settlement Closing Flow Regime

Primary source: SEC T+1 adoption (PROVENANCE_PENDING; not fetched in this session)

Mechanism: Shorter settlement cycle changes funding/settlement timing and can alter closing flow patterns; sample break.

Features: t1_dummy.

Target: Closing auction share pre/post.

Falsify-if: No break found.

Horizon: SLOW_PRIOR

Availability: PUBLIC_BATCH

Priority: B

## W81E-E55 — Holiday-Adjacent Auction Share

Primary source: NYSE early-close schedule; holiday calendars PROVENANCE_PENDING

Mechanism: Pre-holiday sessions have lower participation and may show larger auction share.

Features: holiday_adj flag.

Target: Auction share.

Falsify-if: No difference.

Horizon: DAILY

Availability: PUBLIC_SCHEDULED

Priority: B

## W81E-E56 — Cross-Venue Auction Window Alignment Matrix

Primary source: Pillar spec v2.2k table of auction periods (read); Nasdaq FAQ (read)

Mechanism: Windows differ by venue and listing; a matrix of which information is available at each time prevents look-ahead.

Features: window_matrix(t, venue, listing).

Target: Leakage audit.

Falsify-if: Feature uses information unavailable at decision time.

Horizon: SLOW_PRIOR

Availability: PUBLIC_SCHEDULED

Priority: A

## W81E-E57 — Equity Index Structure State Vector (Truth Ladder)

Primary source: Composite of E01-E56

Mechanism: A conditioning layer: auction step, aggregate imbalance, concentration, ETF stress, data availability. Not a standalone signal.

Features: vector with versioning of exchange rules.

Target: Gate quality.

Falsify-if: Gated system not better out-of-sample than ungated.

Horizon: INTRADAY

Availability: PAID_REALTIME

Priority: S

## Final architecture edge (Truth Ladder)

Truth Ladder: (1) rule-version-verified auction clock; (2) legally available imbalance fields at decision time; (3) index-weighted aggregation with point-in-time weights; (4) placebo and rebalance-stratified tests; (5) intermediate outcomes (imbalance-to-close prediction accuracy, execution slippage tail); (6) only then P&L. The Equity Index Structure State Vector is a conditioning layer.

## Highest-priority W81E tests

1. W81E-E05 Index-Weighted Imbalance Pressure (WIP)
2. W81E-E01 NYSE 3:50 Regulatory Imbalance Direction Persistence
3. W81E-E06 Imbalance Revision Path 3:50 to 3:59
4. W81E-E13 Opening Imbalance Aggregate and Gap Resolution
5. W81E-E52 Arca-Listed ETF Early Closing Imbalance (from 3:00 p.m.)
6. W81E-E12 Listing-Venue Imbalance Split (ES versus NQ Relative)
7. W81E-E36 Leveraged ETF End-of-Day Rebalance Estimate
8. W81E-E02 Nasdaq Closing Information Step Clock
9. W81E-E50 Stale-Open Weight Share
10. W81E-E24 Top-Contributor Narrow-Move State
