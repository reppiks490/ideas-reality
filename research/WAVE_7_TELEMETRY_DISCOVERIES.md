# Wave 7T — Physical Network Telemetry Discoveries

Namespace: W7T

Wave 7T moves deeper into direct physical-economy telemetry: electric-grid load and interchange, river/lock constraints, rail-service performance, fund-positioning disclosure, leverage, satellite thermal anomalies, drug supply, aviation constraints, and multimodal recovery.

Everything below is a research hypothesis until independently falsified and promoted under RESEARCH_PROTOCOL.md.

## W7T-E01 — Hourly Grid Demand Residual Field

Primary source:
U.S. Energy Information Administration Form EIA-930 / Hourly Electric Grid Monitor.

Status:
LIVE / NEAR-LIVE.

Official EIA behavior:
- hourly demand can be published for the previous hour
- demand forecasts are generally available each morning
- generation and interchange fields carry additional lag
- EIA revises anomalous historical observations

Mechanism:
Electricity demand is a direct measurement of physical economic activity plus weather-sensitive load.

Core feature:
actual regional load - weather/calendar/model expected load

Candidates:
- hourly demand residual
- regional load breadth
- industrial-region residual
- weekday/holiday-adjusted acceleration
- forecast error
- load recovery after disruption
- disagreement across neighboring balancing authorities

Targets:
natural gas, regional power, industrial/utility baskets, macro nowcasts.

Priority: S

## W7T-E02 — Grid Interchange Stress / Regional Scarcity

Source:
EIA-930 balancing-authority interchange and generation.

Mechanism:
Physical transfers between balancing authorities reveal where power is scarce or abundant.

Features:
- net import dependence
- interchange surprise
- export reversal
- neighboring-system stress breadth
- generation shortfall vs demand
- fuel-mix substitution under stress

Validate against power prices and gas burn before equity/index targets.

Priority: S-

## W7T-E03 — Generation Fuel-Switching State

Sources:
EIA-930 generation by fuel + EPA CAMPD historical hourly plant emissions/gross-load data.

Candidate state:
GAS_MARGINAL / COAL_MARGINAL / RENEWABLE_SURPLUS / IMPORT_DEPENDENT / SCARCITY.

Use:
natural-gas demand state and regional electricity stress.

Boundary:
CAMPD is detailed but should be treated as historical validation unless exact point-in-time publication latency is proven.

Priority: A+

## W7T-E04 — River Navigation Constraint Field

Primary source:
USGS Water Data APIs.

Status:
LIVE / NEAR-LIVE.

USGS continuous sensors can report streamflow, gage height and other parameters at high frequency; telemetry may appear within minutes.

Features:
- gage-height percentile
- discharge percentile
- rate of change
- seasonal residual
- distance to navigation threshold
- upstream/downstream breadth

Targets:
grain basis, barge freight, fertilizer, coal, petrochemical logistics.

Priority: S

## W7T-E05 — USACE Lock Queue / Status Pressure

Source:
U.S. Army Corps of Engineers Corps Locks / LPMS.

Status:
LIVE / NEAR-LIVE public views.

Public reports include:
- lock queue flotilla, roughly 15-minute updates
- lock status, roughly 15-minute updates
- river-at-a-glance, roughly 30-minute updates
- monthly tonnage and historical usage/closure summaries

Features:
- vessels waiting
- queue duration
- closure duration
- queue acceleration
- consecutive constrained locks
- congestion propagation
- reopening velocity

Priority: S

## W7T-E06 — Inland Waterway Commodity Pressure

Fuse:
USGS river stage
+ USACE lock queue/status
+ USACE tonnage
+ USDA grain transport
+ barge freight
+ export inspections/sales.

Output:
NORMAL / CAPACITY_LOSS / QUEUE_BUILD / FREIGHT_SPIKE / RECOVERY.

Question:
Can physical navigation stress predict basis/spread pressure before slower aggregate reports?

Priority: S

## W7T-E07 — Rail Service Stress Field

Source:
Surface Transportation Board EP 724 weekly rail-service data.

Candidate features:
- train speed
- terminal dwell
- cars online
- origin dwell
- commodity-specific service measures
- railroad dispersion
- persistent deterioration
- recovery after disruption

Use:
industrial/logistics/commodity supply-chain state.

Priority: A+

## W7T-E08 — Intermodal Substitution Graph

Fuse:
river + rail + trucking/freight proxies + ports.

Mechanism:
A disruption matters more when substitute transport capacity is unavailable.

Research:
river constraint -> rail demand
port congestion -> inland rail/truck spillover
rail slowdown -> barge/truck substitution

Priority: A+

## W7T-E09 — N-PORT Institutional Crowding Atlas

Source:
SEC Form N-PORT public datasets.

Status:
DELAYED / RETROSPECTIVE.

Potential features:
- ownership concentration
- cross-fund overlap
- crowded longs
- crowded derivatives
- repo/counterparty concentration
- leverage/borrowings
- liquidity mismatch
- common exit exposure

Hard rule:
public dissemination time, not portfolio report date, controls feature availability.

Priority: A

## W7T-E10 — Crowded Exit Fragility

Fuse:
N-PORT overlap
+ underlying liquidity
+ fund-flow state
+ options/crowding
+ volatility shock.

Hypothesis:
common ownership plus correlated redemptions can create nonlinear exits.

Priority: A

## W7T-E11 — FINRA Margin Leverage Regime

Source:
FINRA Margin Statistics.

Status:
MONTHLY / LAGGED.

Measures:
customer margin debit balances and free credit balances.

Candidate:
net_leverage_pressure =
margin_debit_growth - liquid_credit_growth

Use as slow leverage/risk-appetite state, not naive short-horizon timing.

Priority: B+

## W7T-E12 — Satellite Thermal-Anomaly Event Confirmation

Source:
NASA FIRMS / LANCE VIIRS and MODIS.

Status:
NEAR-REAL-TIME; some U.S./Canada products can be faster.

Mechanism:
thermal anomalies can confirm wildfire, flaring change, refinery/industrial incidents, or restart activity.

Research:
facility geofence
+ historical thermal baseline
+ confidence
+ cloud/view geometry
+ independent official incident source.

One hotspot is never sufficient evidence of facility failure.

Priority: A

## W7T-E13 — Industrial Heat / Flare Deviation

Use FIRMS detections around known:
refineries, LNG terminals, petrochemical complexes, steel/cement plants, power plants.

Feature:
observed thermal activity - facility-specific seasonal/time-of-day baseline.

Validate against official production/outage data first.

Priority: B+

## W7T-E14 — FDA Recall Exposure Graph

Source:
openFDA Enforcement Reports APIs.

Status:
PUBLIC; drug enforcement records are updated weekly.

Coverage:
drug, device, food recalls/enforcement.

Features:
- classification/severity
- distribution breadth
- product revenue materiality
- manufacturer/brand mapping
- substitute beneficiaries
- repeat-quality issue state

Priority: A

## W7T-E15 — Drug Shortage Substitution Graph

Source:
FDA Drug Shortage Database / openFDA Drug Shortages.

Graph:
ingredient -> presentation -> manufacturer -> substitutable products -> therapeutic category.

Fields include company, availability, status, shortage reason and posting/change/update dates.

Research target:
manufacturer volume/revenue substitution and healthcare supply-chain stress.

Priority: A

## W7T-E16 — FAA National Airspace Constraint State

Source:
FAA NAS Status public machine-readable feed.

Status:
LIVE.

Events include:
airport closures, ground stops, ground-delay programs, arrival/departure delays, airspace flow programs and forecast constraints.

Features:
- capacity-weighted affected airports
- average/max delay
- stop duration
- expected vs realized reopening
- hub centrality
- cause
- geographic breadth

Priority: A+

## W7T-E17 — Aviation Network Propagation

Fuse:
FAA restrictions + hub graph + airline schedule/exposure + cargo-hub dependence + weather.

Question:
Which restrictions remain local versus propagate through hub-and-spoke networks?

Targets:
airlines and express freight/logistics.

Priority: A

## W7T-E18 — AIS Historical Flow Baseline

Source:
NOAA/BOEM Marine Cadastre AIS/vessel-traffic datasets.

Status:
HISTORICAL / DELAYED.

Use:
learn normal shipping lanes, port approaches, vessel-class seasonality and route baselines.

Then compare lawful current AIS against the historical baseline.

Priority: A infrastructure

## W7T-E19 — River × Lock × Grain Basis Constraint

Fuse:
USGS stage + USACE queue/status + USDA barge/grain transport + export inspections + futures/cash basis.

Hypothesis:
price-relevant state =
navigation capacity shortfall × export demand × local inventory.

Priority: S

## W7T-E20 — Grid Load Economic Nowcast

Aggregate weather-normalized EIA-930 demand residuals across industrial/commercial regions.

Intermediate targets:
industrial production, regional activity, weather-sensitive demand, holiday/economic disruptions.

Only after mechanism validation test macro/futures surprise.

Priority: A+

## W7T-E21 — Grid Stress × Natural Gas Burn

Fuse:
load surprise + gas-generation share + renewable shortfall + interchange scarcity + weather.

Hypothesis:
gas sensitivity rises when marginal incremental load must be served by gas generation.

Priority: S-

## W7T-E22 — Multimodal Recovery Curve

For river, rail, air, port and grid disruptions estimate:
onset, peak impairment, 50% recovery, 90% recovery, backlog liquidation and overshoot.

Potential edge:
markets may price the shock faster than the recovery path.

Priority: A+

## W7T-E23 — Public Operational State Vector

Fuse orthogonal physical channels:
GRID / RIVER / LOCKS / RAIL / PORTS / AIR / ENERGY / WAREHOUSE / CLOUD / SUPPLY_RECALLS.

Purpose:
describe what the economy is physically able to move, produce and deliver.

Use as regime/context, not a single giant direction signal.

Priority: S

## Highest-priority W7T tests

1. W7T-E01 Hourly Grid Demand Residual Field
2. W7T-E04 River Navigation Constraint Field
3. W7T-E05 USACE Lock Queue / Status Pressure
4. W7T-E06 Inland Waterway Commodity Pressure
5. W7T-E07 Rail Service Stress Field
6. W7T-E19 River × Lock × Grain Basis Constraint
7. W7T-E21 Grid Stress × Natural Gas Burn
8. W7T-E12 Satellite Thermal-Anomaly Event Confirmation
9. W7T-E16 FAA National Airspace Constraint State
10. W7T-E23 Public Operational State Vector
