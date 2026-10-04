# Wave 63M — Research Methods

Namespace: **W63M**

## W63M-M01 — Announcement-vs-Effective Time
Store advisory public time and effective margin time separately.

## W63M-M02 — Exact Contract Identity
Margin rules are contract/product specific.
Do not infer ES from MES or NQ from MNQ without explicit mapping.

## W63M-M03 — Account-Class Semantics
Preserve clearing/member/customer/speculative/hedge account distinctions where rates differ.

## W63M-M04 — Initial-vs-Maintenance Semantics
Do not mix initial margin with maintenance/performance bond.

## W63M-M05 — Parameter Decomposition
For SPAN-style systems preserve:
scan risk,
volatility scan,
spread charges/credits,
delivery add-ons,
SOM.

## W63M-M06 — Portfolio Margin Reconstruction
A single contract margin increase does not equal portfolio-level increase because offsets matter.

## W63M-M07 — Offset-Credit Versioning
Archive historical inter/intra commodity credits and parameter files.

## W63M-M08 — CME/ICE Methodology Version
SPAN, SPAN 2 and ICE IRM versions can change.
Use the model active on the historical date.

## W63M-M09 — CFTC Cleared-Margin Lag
CFTC aggregate cleared-margin data are monthly and generally published within 10 business days after month-end.

Never use as live event state.

## W63M-M10 — FCM Financial Lag
CFTC FCM selected financial data are monthly and published after regulatory filing lag.

## W63M-M11 — FCM Capital Rule Versioning
Apply the Regulation 1.17 requirement effective at that date.

## W63M-M12 — Public FCM Identity
Normalize legal FCM entities; do not automatically equate an FCM with listed parent economics.

## W63M-M13 — Customer-vs-House Funds
Segregated customer assets are not proprietary liquidity available for arbitrary firm use.

## W63M-M14 — Variation-Margin Scenario
Public initial-margin data do not reveal participant-specific VM.
Model VM from marked positions only as scenario/distribution.

## W63M-M15 — Positioning Vintage
Cross with W62C only using COT/BPR information that was public by the margin announcement time.

## W63M-M16 — Volatility Endogeneity
Margin increases respond to volatility, which also drives exits.
Use matched/event designs before claiming causal margin effects.

## W63M-M17 — Roll/Expiry Control
OI changes around roll/expiry are mechanical and must be controlled.

## W63M-M18 — Default-Fund Semantics
Mutualized resources are available under specific default-waterfall rules, not general liquidity buffers.

## W63M-M19 — Market-Absorption Target
Pre-register intermediate outcomes:
OI,
spread/depth,
volume migration,
position exit,
or collateral usage.

## W63M-M20 — Incremental Promotion Gate
Promote only if W63M features add OOS information beyond:
volatility,
price change,
open interest,
W62C crowding,
and W39F fund fragility.
