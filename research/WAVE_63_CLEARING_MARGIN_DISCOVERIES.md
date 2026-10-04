# Wave 63M — Clearing Margin & Forced Deleveraging

Namespace: **W63M**

Thesis: crowded positioning becomes mechanically dangerous when clearing collateral requirements rise faster than market participants' liquidity buffers. Exchange performance-bond changes, CCP initial-margin growth, FCM capital requirements and customer-funds buffers form a measurable transmission chain from volatility to liquidity demand to forced position reduction.

W39F owns fund-level structural fragility. W62C owns futures positioning/crowding. W63M owns the **clearing-margin and intermediary-capital transmission layer**.

All candidates are research hypotheses only. Claude owns later implementation.

## W63M-E01 — CME Performance-Bond Change Event
Primary source:
CME Clearing performance-bond advisories.

Capture:
notice time,
effective-after-close time,
contract,
current requirement,
new requirement,
account class where applicable.

Priority: S

## W63M-E02 — Outright Margin Shock
Feature:
(new outright margin - old margin) / old margin.

Map by exact contract and expiry where relevant.

Priority: S

## W63M-E03 — Initial-vs-Maintenance Margin Delta
Preserve initial and maintenance/performance-bond semantics separately.

Priority: A+

## W63M-E04 — Price Scan-Range Shock
CME SPAN scan-risk parameter changes can increase portfolio requirements even when headline outright tables are unchanged.

Priority: S-

## W63M-E05 — Volatility Scan-Range Shock
For options:
change in implied-volatility scan range.

Potentially important for concentrated short-volatility portfolios.

Priority: S

## W63M-E06 — Short Option Minimum Shock
CME advisories can alter Short Option Minimum parameters.

Feature:
new SOM burden on deep-OTM short-option portfolios.

Priority: S-

## W63M-E07 — Intra-Commodity Spread Charge Shock
Track margin change for calendar/related spreads within a combined commodity.

Priority: A+

## W63M-E08 — Inter-Commodity Credit Compression
Lower offset credit between related products can sharply increase portfolio margin without directional exposure changing.

Priority: S

## W63M-E09 — Delivery-Risk Add-On Shock
Physically delivered contracts can receive greater delivery/spot risk near delivery.

Fuse with W49 physical-delivery state.

Priority: A+

## W63M-E10 — Margin Announcement-to-Effective Clock
Feature:
hours from public advisory
to
effective after close.

This is a deterministic funding deadline.

Priority: S

## W63M-E11 — Margin Surprise
Estimate expected margin from recent volatility/model behavior.

Feature:
actual announced change
-
expected change.

Priority: S

## W63M-E12 — ICE Risk-Parameter Shock
Primary source:
ICE Clear U.S. current/historical margin parameter files/notices.

Track:
scanning risk,
inter-month add-ons,
inter-commodity credits,
implied-volatility scan ranges,
butterfly spread add-ons.

Priority: S

## W63M-E13 — ICE Effective-to-Call Clock
ICE notes parameter changes are reflected on effective date and called the following business day.

Model the exact liquidity-call timing.

Priority: A+

## W63M-E14 — CCP Aggregate Initial-Margin Level
Primary source:
CFTC Cleared Margin Reports.

Track aggregate IM posted at covered DCOs by futures vs swaps and house vs customer where available.

Priority: S-

## W63M-E15 — CCP Margin Acceleration
Feature:
month-over-month and multi-month change in aggregate initial margin.

Use as slow systemic collateral-state indicator.

Priority: A+

## W63M-E16 — Futures-vs-Swaps Margin Rotation
Compare margin growth across product/clearing categories.

Fuse with W38 OTC derivatives.

Priority: A

## W63M-E17 — FCM Adjusted-Net-Capital Buffer
Primary source:
CFTC monthly FCM financial data.

Feature:
adjusted net capital
-
minimum/net-capital requirement.

Normalize by requirement and customer assets.

Priority: S

## W63M-E18 — FCM Risk-Margin Capital Sensitivity
CFTC Regulation 1.17 links an FCM minimum capital requirement partly to 8% of aggregate risk margin carried for customer/noncustomer positions under current rules.

Estimate:
incremental capital requirement induced by exchange/CCP margin shock.

Priority: S

## W63M-E19 — FCM Customer-Segregation Excess
Track customer-segregated funds:
amount held
-
amount required.

Priority: S-

## W63M-E20 — FCM Residual-Interest Cushion
Where public data permit:
target residual interest / actual segregated excess.

Use as customer-funding-buffer context.

Priority: A

## W63M-E21 — FCM Buffer Compression Breadth
Count/share of large FCMs simultaneously showing declining:
capital cushion,
segregation excess,
or other public liquidity-buffer measures.

Priority: S-

## W63M-E22 — Clearing Intermediary Concentration
Measure concentration of customer-segregated assets and cleared business among FCMs.

Large concentration can amplify operational/capital stress at one intermediary.

Priority: A+

## W63M-E23 — Margin Shock × W62C Crowding
Core cross-wave state:

large margin increase
× extreme leveraged/managed-money crowding.

Hypothesis:
raises probability of forced position reduction.

Priority: S

## W63M-E24 — Margin Shock × Physical Constraint
If a physically supported trend is already forcing volatility higher, a margin hike can accelerate financial deleveraging without resolving the physical shortage.

Priority: S

## W63M-E25 — Margin Shock × Fund Fragility
Fuse W39F:
fund liquidity buffer / derivatives exposure
with
new futures/option margin demand.

Priority: S

## W63M-E26 — Initial + Variation Margin Double Shock
Scenario:
higher initial margin
+
adverse mark-to-market variation margin.

Estimate combined same-day/next-day liquidity requirement.

Priority: S

## W63M-E27 — Margin-to-Open-Interest Exit Response
Target:
OI contraction after margin change,
conditioned on price move and volatility.

Priority: S-

## W63M-E28 — Margin-to-Volume Migration
Research whether activity migrates:
standard -> micro,
one exchange -> substitute,
futures -> ETF/options/OTC
after margin changes.

Priority: A+

## W63M-E29 — Spread-Credit Compression Unwind
Portfolios relying on cross-product/inter-month margin offsets can face abrupt funding needs when credits compress.

Priority: S

## W63M-E30 — Short-Volatility Forced-Cover Hazard
SOM/volatility-scan increases
× short-option concentration
× realized-volatility shock.

Priority: S

## W63M-E31 — Clearing Default-Resource State
Use CCP public disclosures for:
initial margin on deposit,
guaranty/default fund,
CCP contributions,
assessment resources.

This is a structural resilience state, not a default forecast by itself.

Priority: A

## W63M-E32 — Default-Waterfall Coverage Ratio
Scenario:
stressed clearing-member loss
/
available member-specific + mutualized public resource layers.

Only where exposure assumptions are explicitly scenario-based.

Priority: B+

## W63M-E33 — Forced Deleveraging Quotient
FDQ =
incremental collateral + variation-margin need
/
liquid resources available to the crowded risk holders/intermediaries.

Output as a range.

Priority: S

## W63M-E34 — Margin Procyclicality State
Measure how rapidly margin responds to volatility relative to historical regime.

Recent research shows margin design can affect position-exit feedback.

Priority: S-

## W63M-E35 — Clearing Stress Reality Gap
Compare:
exchange-level margin shock
vs
slow CFTC aggregate IM/FCM financial data when later released.

Use later data to validate whether the event propagated systemically.

Priority: A+

## W63M-E36 — Clearing Stress Truth Ladder
VOLATILITY/PHYSICAL SHOCK
-> EXCHANGE/CCP MARGIN CHANGE
-> COLLATERAL CALL
-> FCM CAPITAL/SEGREGATION PRESSURE
-> POSITION REDUCTION
-> OI/LIQUIDITY CHANGE
-> PRICE/VOLATILITY FEEDBACK
-> NORMALIZATION.

Priority: S architecture

## Highest-priority W63M tests

1. W63M-E02 Outright Margin Shock
2. W63M-E08 Inter-Commodity Credit Compression
3. W63M-E10 Announcement-to-Effective Clock
4. W63M-E18 FCM Risk-Margin Capital Sensitivity
5. W63M-E23 Margin Shock × W62C Crowding
6. W63M-E26 Initial + Variation Margin Double Shock
7. W63M-E27 Margin-to-Open-Interest Exit Response
8. W63M-E29 Spread-Credit Compression Unwind
9. W63M-E33 Forced Deleveraging Quotient
10. W63M-E36 Clearing Stress Truth Ladder
