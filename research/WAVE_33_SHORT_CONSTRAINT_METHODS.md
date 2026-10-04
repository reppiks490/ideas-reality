# Wave 33S — Research Methods

Namespace: **W33S**

## W33S-M01 — FTD Publication Mask
SEC FTD files are delayed: first half of month near month-end; second half around the 15th of the next month.
Backtests use public file date, not settlement date.

## W33S-M02 — FTD Balance Semantics
SEC quantity is total fail-to-deliver balance outstanding in NSCC CNS on that settlement date.
It is not newly created daily fails and not a direct naked-short count.

## W33S-M03 — FTD Corporate-Action Adjustment
CUSIP/symbol/share-count changes must be reconciled before persistence calculations.

## W33S-M04 — Threshold Source Time
Use listing SRO daily threshold-list publication/applicability timestamp.

## W33S-M05 — Threshold Entry Definition
Require source-defined five consecutive settlement days meeting the fail threshold.

## W33S-M06 — Threshold Exit Definition
Removal requires five consecutive settlement days below the specified fail threshold under Reg SHO semantics.

## W33S-M07 — Participant-Level Opacity
Public threshold/FTD data do not identify the clearing participant responsible for a fail.
Never infer exact participant forced-cover quantity.

## W33S-M08 — Short Interest Availability
FINRA short interest is twice monthly and publicly disseminated after the reporting settlement date.
Do not interpolate future values as known.

## W33S-M09 — Short Interest != Short Volume
Positions outstanding and executed short-sale volume are different concepts.

## W33S-M10 — FINRA Short-Volume Scope
Daily short-sale volume covers media-reported trades executed and reported to FINRA TRFs, ADF or ORF.
It is not consolidated all-venue market short volume.

## W33S-M11 — Short-Exempt Separation
Keep short-exempt volume separate from ordinary short volume.

## W33S-M12 — Fractional-Share Format Break
FINRA NMS short-volume files can include fractional shares beginning Feb. 23, 2026.
Normalize historical comparisons.

## W33S-M13 — Option-Implied Borrow Contract Filter
Use liquid option pairs with synchronized quotes, correct dividends/rates and no obvious stale/crossed markets.

## W33S-M14 — American Exercise Adjustment
Single-stock U.S. options are generally American style; parity-based borrow inference must handle early-exercise effects.

## W33S-M15 — Dividend Forecast Vintage
Implied borrow calculations require point-in-time expected dividends, not realized later dividends.

## W33S-M16 — Passive Ownership Lag
13F/index ownership inputs are delayed; use only at public availability.

## W33S-M17 — Rule 201 Separation
Price-test restriction state is distinct from settlement fail/threshold state.

## W33S-M18 — SLATE Hard Gate
FINRA currently states SLATE implementation is extended to Sept. 28, 2028.
No synthetic 2026 SLATE observations.

## W33S-M19 — Squeeze vs Fundamental Short Thesis
High constraint can coexist with negative informed short signal.
Model squeeze fragility separately from expected long-run return direction.

## W33S-M20 — Intermediate Promotion Gate
Before market alpha require OOS prediction of:
threshold entry/exit,
FTD persistence,
borrow proxy,
short-interest change,
covering intensity,
or liquidity dislocation.
