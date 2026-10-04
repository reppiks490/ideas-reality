# Wave 12C — Research Methods

Namespace: W12C

## W12C-M01 — Margin Notice / Effective Dual Clock
Store notice timestamp and effective timestamp separately. A known future margin change can affect behavior before it becomes effective.

## W12C-M02 — Exchange-vs-House Margin Separation
CME requirements are clearing/exchange minimums. FCMs may impose higher house margin. Never claim CME data equals a customer's actual required margin.

## W12C-M03 — Maintenance / Initial Separation
Track maintenance, Non-HRP initial and HRP initial independently.

## W12C-M04 — Notional Normalization
Normalize margin dollars by contract notional and optionally by volatility risk.

## W12C-M05 — Endogenous Margin Control
Margin changes react to volatility. Use matched/event controls and pre-notice market variables before claiming margin causes subsequent behavior.

## W12C-M06 — Risk-Parameter Vintage Store
Archive exact RPF/SPAN parameter vintages by business date. Do not recalculate old backtests using today's parameters.

## W12C-M07 — SPAN / SPAN2 Methodology Regime
Record risk-framework transition and product migration dates explicitly.

## W12C-M08 — Access-Tier Classification
Distinguish public notices, legacy free files, current SFTP-entitled RPFs, licensed Margin Service APIs and local deployable-software outputs.

## W12C-M09 — Cross-Product Offset Reconstruction
When researching spread-credit changes, reconstruct the whole relevant portfolio; single-leg margin is insufficient.

## W12C-M10 — Open-Interest Availability Lag
Cleared OI is generally prior-day state. Do not treat end-of-day OI as intraday live positioning unless a source explicitly provides it.

## W12C-M11 — Delivery Calendar
Respect first notice day, intent date, delivery date, last trade date, spot-month rules and contract-specific delivery mechanics.

## W12C-M12 — Clearing-Firm Identity Boundary
Issues/stops identify clearing firms/organizations, not necessarily beneficial owners. No ultimate-owner inference without evidence.

## W12C-M13 — Inventory Status Semantics
Registered = eligible metal with warrant issued.
Eligible = meets delivery specs but no warrant.
Do not equate all eligible metal with immediately offered supply.

## W12C-M14 — Inventory Unit Conversion
Convert ounces/pounds into exact contract equivalents using contract specs before ratios.

## W12C-M15 — Pledged Gold Treatment
Gold stock reports can distinguish inventory pledged as performance-bond collateral. Treat pledged status separately from available registered supply.

## W12C-M16 — BPR Publication Mask
Monthly BPR first-Tuesday data become usable only after first-Friday public release.

## W12C-M17 — Gross-Options Constraint
BPR options positions are gross and not delta-adjusted. Avoid fake delta/gamma inference.

## W12C-M18 — Price-Limit Reference Reconstruction
Archive official reference/fixing price and current applicable limit schedule for each trade date.

## W12C-M19 — Exact Session Rule
NQ active constraints differ across overnight, U.S. cash-market, late-day and post-cash sessions. Use session-specific rules.

## W12C-M20 — DCB State Machine
Replicate rolling-window DCB behavior, monitoring/pause state and post-pause reopening rather than using a static percentage threshold.

## W12C-M21 — Non-Tradable Price Awareness
Backtests must not fill orders through a hard exchange limit or during a halt/pre-open state.

## W12C-M22 — Promotion Gate
A clearing/margin signal must first explain leverage/OI/liquidity/delivery mechanics before being promoted as directional alpha.
