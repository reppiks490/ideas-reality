# Wave 49P — Research Methods

Namespace: **W49P**

## W49P-M01 — Daily Warehouse Vintage Archive
Archive each official daily stock file with first-public timestamp.

## W49P-M02 — Registered != Total Vault Metal
Registered is warrant-backed exchange-deliverable stock.

Eligible and off-warrant are separate states.

## W49P-M03 — Eligible Conversion Uncertainty
Never count all eligible inventory as guaranteed delivery supply.

## W49P-M04 — Warrant-State vs Physical Movement
Separate status changes from receipts/shipments.

## W49P-M05 — Contract Unit Normalization
Convert ounces/tonnes/pounds to exact futures-equivalent contracts using the contract version active at the time.

## W49P-M06 — Contract-Specific Delivery Rules
Gold, silver, copper and other metals have different units, grades, notice calendars and eligible forms.

## W49P-M07 — Open-Interest Intent Caveat
Open interest is not physical-delivery demand.

Model roll/liquidation probability.

## W49P-M08 — Notice Calendar Versioning
First notice, last notice, last trade and delivery windows must be sourced per contract/month.

## W49P-M09 — Delivery-Notice Deduplication
Distinguish new daily notices from cumulative counts.

## W49P-M10 — Clearing-Member Interpretation
Issued/stopped clearing-member activity is not necessarily end-beneficial-owner identity.

## W49P-M11 — Position-Limit Versioning
Spot-month limits/exemptions change historically.

## W49P-M12 — LME Publication Lag
Daily LME public stock breakdown is delayed under current publication policy.

Use actual public availability.

## W49P-M13 — LME Live/Cancelled Semantics
Cancelled warrants remain within warehouse until load-out and can later be re-warranted.

## W49P-M14 — Queue Capacity Model
Estimate minimum physical load-out time from applicable warehouse rule and queued tonnage.

## W49P-M15 — Off-Warrant Rights Gate
LME faster off-warrant data may be licensed; public delayed data have different production rights.

## W49P-M16 — Location-Level Aggregation
Avoid national/global aggregation when contract delivery is location-specific.

## W49P-M17 — External Supply Gate
Metal outside approved warehouses counts as near-term deliverable only if quality, location, logistics and timing are validated.

## W49P-M18 — Inventory Endogeneity
High prices/basis can attract inventory into exchange warehouses.

Do not claim one-way causality without design.

## W49P-M19 — Roll/Expiry Common-Cause Control
Delivery-month effects overlap with mechanical futures roll.

Use W26R controls.

## W49P-M20 — Physical Promotion Gate
Before return testing require OOS improvement in:
warrant conversion,
delivery notices,
load-out,
inventory depletion/replenishment,
basis,
or physical premiums.
