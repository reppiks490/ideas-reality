# Edge Atlas

Status labels:
- LIVE: source is currently available for research.
- DELAYED: usable for research but not live enough for certain horizons.
- WATCH: future source or source whose deployment is not yet live.
- PROPRIETARY: may require paid or licensed access.

Every candidate below is a hypothesis, not a claim of alpha.

## Tier S — highest-priority candidates

### E01 — Institutional Risk-Transfer Shadow Book
Mechanism:
Public swap-repository dissemination reveals institutional risk transfer outside the futures order book. Build signed notional surprise by asset class, tenor, trade direction proxy, concentration, and price concession. Test whether residualized swap flow leads ES, NQ, rates, GC, FX, or volatility futures after controlling for contemporaneous futures price/order flow.

Candidate feature:
IRTI = signed_notional_surprise × tenor_weight × price_concession × cross_asset_concentration

Sources:
- CME Swap Data Repository public dissemination
- DTCC/ICE SDR public dissemination where accessible

Targets:
ES, NQ, ZN/ZB, GC, DXY/FX futures.

Falsify if:
No out-of-sample information remains after controlling for futures returns, rates, VIX, macro announcements, and known reporting delays.

Priority: S

### E02 — 0DTE Gamma Phase Field
Mechanism:
Dealer option hedging can change the market response function rather than simply predict direction. Positive-gamma regimes may dampen shocks and favor reversal; negative-gamma regimes may amplify shocks and favor continuation. Extend beyond gamma to vanna/charm/time-to-close and distance to dominant strikes.

Candidate state:
REVERSION_FIELD / NEUTRAL / ACCELERATION_FIELD

Interactions:
gamma sign × gamma magnitude × spot-strike distance × vanna × charm × time-to-close × VIX state × ES/NQ liquidity.

Key test:
Does the same futures setup have materially different conditional expectancy depending on the phase field?

Priority: S

### E03 — Mechanical Hedge Pressure / Absorption Capacity
Mechanism:
Estimate options-driven hedge demand, then divide by the futures market's capacity to absorb it. This is deliberately different from static GEX.

Candidate:
MHPA = estimated_delta_rehedge_demand / executable_liquidity_capacity

Liquidity capacity can include depth, replenishment speed, spread, queue geometry, recent sweep recovery, and expected impact.

Hypothesis:
Nonlinear moves occur when required hedge demand becomes large relative to replenishing liquidity.

Priority: S

### E04 — Treasury Auction Absorption Tensor
Mechanism:
Auction results contain information about who absorbed issuance and at what concession. Model tail, dealer/direct/indirect shares, bid-to-cover, issue size, maturity, reopening status, when-issued move, and pre-auction positioning.

Candidate:
AAT = surprise(tail, indirect share, dealer take, direct share, BTC, size) conditioned on rates regime.

Cross-market targets:
ZN/ZB first, then ES/NQ/GC.

Composite:
AAT × Gamma Phase Field may explain why identical rate shocks produce different equity responses.

Priority: S

### E05 — TRACE Treasury Flow State
Status: LIVE, next-day for public non-commercial access; professional data products may be fee-based.

Mechanism:
FINRA publishes transaction-level activity for on-the-run nominal Treasury coupons, including price, capped size, counterparty type, ATS flag, and modifiers. Daily aggregate Treasury data are also available.

Research direction:
Construct dealer-customer imbalance proxies, ATS share, block-intensity, maturity-bucket pressure, and price-impact residuals. Use uncapped six-month-delayed history for model development where licensing permits, then test next-day state effects.

Do not mislabel as real-time intraday: public transaction-level access is next-day.

Priority: S

### E06 — Fiscal Liquidity Impulse
Mechanism:
Daily Treasury operations move reserves through the Treasury General Account. Tax receipts drain bank reserves; Treasury spending injects them. A 2026 empirical paper found daily fiscal flows added information to asset-pricing models.

Candidate:
FLI = normalized(TGA withdrawals - deposits), decomposed by tax, benefit, debt, customs, and agency flows.

Subfeatures:
- withheld tax pulse
- corporate tax pulse
- customs-duty pulse
- Social Security/Medicare disbursement pulse
- interest/redemption pulse
- debt issuance settlement pulse

Targets:
SOFR/rates first; ES/NQ as secondary.

Priority: S

### E07 — Cross-Venue Causal Flow Graph
Mechanism:
Do not assume ES/NQ always lead. Estimate a sparse, time-varying graph across futures, ETFs, index constituents, options-derived state, VIX products, and rates.

Nodes:
ES, NQ, SPY, QQQ, VIX/VIX futures, megacap basket, semis, rates, DXY.

Output:
Leader identity, propagation direction, edge strength, edge half-life, confidence.

Required:
Strict lagging and no contemporaneous leakage.

Priority: S

### E08 — Liquidity Replenishment / Resilience Field
Mechanism:
Static imbalance misses whether liquidity refills after being consumed. Measure how quickly the book heals after sweeps/cancellations.

Features:
- refill half-life
- same-side vs opposite-side refill asymmetry
- spread recovery
- depth recovery L1-LN
- cancellation-to-add ratio
- queue reformation speed
- liquidity-hole persistence

Hypothesis:
Aggressive shocks followed by fast opposing refill mean-revert; shocks with failed refill continue.

Priority: S

### E09 — Hawkes Propagation / Exhaustion State
Mechanism:
Model self- and cross-excitation among submissions, cancellations, market orders, and price changes. Recent work suggests non-monotonic triggering kernels can matter, so do not force simple exponential decay.

Output:
- excitation matrix
- endogenous pressure
- exogenous shock score
- propagation half-life
- exhaustion probability

Priority: S

### E10 — Edge Decay / Causal Half-Life Engine
Mechanism:
Predict the health of each edge instead of only market direction.

For every candidate track:
effect size, calibration error, regime stability, turnover, crowding proxy, time since discovery, residual correlation with sibling models, and sequential evidence.

Output:
ACTIVE / DECAYING / DORMANT / RETIRED.

Priority: S

## Tier A — physical-world and forward-state edges

### E11 — Port of Los Angeles Forward Cargo Field
Status: LIVE.

The Port of Los Angeles Signal provides approximately three weeks of forward inbound cargo visibility based on carrier manifest records; Horizon provides longer-horizon forecasts.

Candidate surprises:
- projected TEU vs seasonal baseline
- rail-vs-truck mode shift
- forecast revision velocity
- scheduled vessel count surprise
- import/export/empty mix

Use:
Consumer/import/inventory nowcasting; later test ES/NQ and sector exposure.

Priority: A

### E12 — Global Port Satellite Congestion Field
Mechanism:
NASA/ESA-style imagery can measure container stacks, vessel queues, and port activity. Published research found satellite-derived port container measures predicted stock-index returns across many countries, though this must be independently replicated.

Candidate:
port_stack_anomaly × vessel_arrival_delta × dwell_proxy × trade-weight exposure

Priority: A

### E13 — Mississippi Physical Logistics Graph
Status: LIVE public components.

Combine:
- USGS streamflow/gage height
- USACE lock queues/status/delay
- USDA grain export/market data
- barge/freight rates where available
- NOAA precipitation/drought

Targets:
corn, soy, wheat, fertilizer, energy basis; later macro spillovers.

The key variable is not river level alone. It is transport capacity surprise relative to expected commodity flow.

Priority: A

### E14 — Grid Forecast Error Network
Status: LIVE.

PJM, EIA, ERCOT and CAISO publish actual load, load forecasts, generation/outages and interchange data.

Candidates:
- load forecast error
- renewable forecast error
- forced outage surprise
- interchange stress
- scarcity-state transition
- weather-adjusted thermal generation residual

Targets:
NG/power/energy first; broader macro only after proof.

Priority: A

### E15 — NASA Black Marble Industrial Pulse
Status: LIVE; NASA says near-real-time Black Marble products are available within hours, including daily and some granular products.

Mechanism:
Nighttime-light deviations can proxy power outages, industrial activity, gas flaring, shipping/fishing and disaster impact.

Research:
Geofence factories, data centers, refineries, ports, mines, oil fields, and industrial clusters. Compute weather/moon/cloud-corrected deviations.

Targets:
Company/sector baskets, energy, macro nowcast.

Priority: A

### E16 — NO2 / Atmospheric Industrial Pulse
Mechanism:
Satellite NO2 and related atmospheric measures can proxy combustion, industrial activity, shipping and power generation.

Requirements:
Strong weather normalization, wind transport controls, seasonality, cloud mask, wildfire contamination controls.

Targets:
Industrial production nowcasts, refinery/port activity, regional shock confirmation.

Priority: A-

### E17 — National Mobility Pulse
Sources:
FAA SWIM/SWIFT where accessible; TSA daily checkpoint throughput; BTS.

Features:
- passenger throughput surprise
- ground-delay anomaly
- flight-volume anomaly
- regional disruption dispersion
- airport network centrality shock

Use:
Consumer/travel nowcasts first; broad index only if incremental.

Priority: A-

### E18 — Internet Activity / Outage Pulse
Status: LIVE through Cloudflare Radar API.

Cloudflare exposes network traffic time series down to 15-minute aggregation for appropriate windows, traffic anomalies, outages, geography/ASN, and cause labels.

Candidate:
internet_activity_residual by geography / cloud / network, normalized by time-of-day and weekday.

Use:
Disaster confirmation, cloud-service outage, regional business interruption, geopolitical disruption. Avoid naive "internet up = stocks up."

Priority: A-

### E19 — FEMA Shock Confirmation Layer
Status: LIVE, OpenFEMA updates some declaration datasets roughly every 20 minutes.

Use:
Not as a standalone predictor. Use as official event confirmation and geographic severity metadata in a multi-source disaster graph.

Combine:
NWS alerts + FEMA + Black Marble + Cloudflare + grid outages + logistics.

Priority: A-

### E20 — Korea Semiconductor Export Pulse
Status: LIVE release cadence via Korea Customs; first-10-day and first-20-day preliminary export statistics are widely disseminated, with semiconductor breakouts.

Mechanism:
South Korea is highly exposed to the global semiconductor cycle. Build calendar-adjusted chip export surprise and test whether it leads global semiconductor earnings/revisions and US tech/semiconductor baskets.

Targets:
SOX/semis first, NQ second.

Priority: A

### E21 — Forward Manifest Revision Velocity
Mechanism:
The revision path of a forward forecast can be more informative than the level. Track Port of LA expected cargo at T-21, T-14, T-7, and realized arrival.

Feature:
revision_velocity + forecast_error_history + source confidence.

Priority: A

### E22 — Rail / Intermodal Industrial Pulse
Sources:
AAR weekly traffic, STB railroad performance data where available.

Features:
commodity carloads, intermodal units, train speed, dwell, service deterioration, sector mix.

Use:
Industrial production, autos, metals, coal, grain, retail inventory nowcasts.

Priority: A-

### E23 — USDA Cash-to-Futures Basis Graph
Source:
USDA MyMarketNews MARS API and related USDA publications.

Mechanism:
Build regional cash/basis, livestock auction, cold-storage, movement, truck-rate and point-of-sale signals against futures.

Goal:
Detect physical-market divergence before futures convergence.

Priority: A

### E24 — Daily Labor Demand Pulse
Source:
Indeed Hiring Lab daily observations refreshed weekly, with sector and geography detail.

Candidate:
new-posting acceleration, sector breadth, geographic diffusion, tech-labor delta.

Use:
Payroll/unemployment nowcast and cross-sectional sector research. Must version vintages because methodology and historical series can be revised.

Priority: A-

### E25 — Daily Travel-to-Revenue Nowcast
TSA throughput is published quickly and BTS research shows it can forecast enplanements accurately.

Research:
Use carrier exposure, geography, route mix, international share and capacity to transform national TSA counts into company-specific demand nowcasts.

Priority: A-

## Tier B — institutional/corporate/event research

### E26 — EDGAR Information Diffusion Graph
Status: LIVE; SEC says submissions metadata update in real time, typically under a second, XBRL typically under a minute.

Mechanism:
A filing from one company may contain information for suppliers, customers, competitors or index peers before those firms file.

Build:
company knowledge graph + filing semantic event + exposure weights + market reaction.

Strict rule:
Use public dissemination timestamp, not period-of-report.

Priority: B+

### E27 — Filing Surprise Without NLP Hype
Features:
form/item type, filing time, amendment, exhibit count, XBRL fact deltas, unexpected balance-sheet/account changes, auditor changes, financing events.

Use structured facts before free-form language.

Priority: B

### E28 — NHTSA Recall Supply-Chain Shock
Status: LIVE daily public data.

Mechanism:
Map recalls to manufacturers and suppliers; scale by affected population, component severity, production dates and supply-chain centrality.

Targets:
auto OEMs/suppliers, sector baskets.

Priority: B

### E29 — openFDA Event Graph
Mechanism:
Use official approvals, recalls, safety and enforcement data as structured event inputs for pharma/device baskets. Focus on event surprise relative to expected calendar and product revenue exposure.

Priority: B

### E30 — Fund Crowding / Derivatives Map
Source:
SEC Form N-PORT structured quarterly public datasets.

Features:
fund crowding, position concentration, derivative notional, counterparties, liquidity classifications, DV01/CS01, securities lending.

Use:
slow state/crowding risk, not intraday trading.

Priority: B

### E31 — Primary Dealer Balance-Sheet Pressure
Source:
New York Fed Primary Dealer Statistics, weekly with one-week lag.

Features:
net positions by Treasury maturity, repo/reverse-repo, securities borrowed/lent, fails, transactions.

Composite:
dealer inventory pressure × upcoming auction supply × volatility × funding cost.

Priority: B+

### E32 — FICC Sponsored Repo Capacity
Source:
DTCC publishes sponsored repo/reverse-repo activity charts/data.

Research:
Treat clearing/sponsored-repo expansion/contraction as dealer-balance-sheet/funding-capacity state, subject to publication timing.

Priority: B

### E33 — Money-Market Cash Reservoir
Source:
ICI weekly money-market fund assets plus fund-flow estimates.

Features:
institutional vs retail, government vs prime, rate differentials, Treasury bill supply.

Use:
slow liquidity state and potential cash-rotation capacity.

Priority: B

### E34 — ETF Primary-Flow Close Pressure
Mechanism:
Research suggests authorized-participant/index-arbitrage effects concentrate in liquid underlying names and can intensify near the close.

Research:
Predict closing liquidity stress from ETF creation/redemption, basket composition, index flow, and constituent liquidity.

Priority: B+

### E35 — Customs Duty Shadow Import Pulse
Source:
Daily Treasury Statement customs receipts.

Mechanism:
Customs cash receipts may provide a noisy high-frequency proxy for tariffed import activity.

Mandatory controls:
tariff-rate changes, payment lags, de minimis/rule changes, working days.

Priority: B

## Tier C — experimental/weird

### E36 — Cloud/Internet × Data-Center Power Coupling
Combine:
Cloudflare traffic anomalies + regional grid load + Black Marble + weather.

Hypothesis:
Large cloud/data-center activity shocks may have observable power and network signatures with regional economic implications.

Test first as anomaly detection, not directional market alpha.

Priority: C+

### E37 — Space-Weather Infrastructure Stress
Use only if empirical evidence survives.
Combine SWPC solar/geomagnetic events with grid, GNSS/aviation, satellite and communications disturbances.

Do not promote based on folklore or trader-superstition correlations.

Priority: C-

### E38 — Earthquake / Geospatial Supply Shock
Use USGS seismic events mapped to refinery, port, mine, semiconductor fab, pipeline and logistics exposure.

Require physical exposure and disruption confirmation.

Priority: C

### E39 — Factory-Light Company Nowcast
Geofence major factories using Black Marble. Track adjusted nighttime activity against company production KPIs.

Requires:
facility-level mapping, shift schedules, weather/cloud normalization, lighting retrofits, maintenance shutdown controls.

Priority: C+

### E40 — Disaster Multi-Sensor Severity Score
NWS/FEMA event × Black Marble outage × Cloudflare drop × grid load loss × transport disruption.

The edge is the disagreement:
headline severity can differ from observed physical severity.

Priority: A-

## Watchlist edges

### W01 — FINRA SLATE Securities Lending
Status: WATCH — NOT LIVE.
FINRA currently states launch has been extended to September 28, 2028.

When live, it is likely high-value because planned public data include loan activity and loan-rate distributions.

Potential future features:
borrow stress, short crowding, loan-rate jumps, borrow-demand breadth.

Do not implement as a current source.

### W02 — Future broader Treasury transparency
Monitor FINRA/Treasury expansion beyond currently public on-the-run transaction-level scope.

### W03 — New NASA/NOAA-21 night-light products
NASA released newer NOAA-20/NOAA-21 NRT products in 2026. Track continuity as Suomi-NPP products retire/change.

## Research ordering

First 10 to test:
E03, E04, E05, E06, E08, E11, E13, E15, E20, E26.

Why:
They span independent causal channels: hedging mechanics, Treasury supply, fiscal liquidity, microstructure resilience, physical trade, logistics, remote sensing, semiconductor demand and corporate information diffusion.
