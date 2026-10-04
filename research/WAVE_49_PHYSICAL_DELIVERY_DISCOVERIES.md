# Wave 49P — Physical Inventory & Delivery Pressure

Namespace: **W49P**

Thesis: exchange warehouse inventory is not a single quantity. Metal can be eligible but unwarranted, registered and warrant-backed, live but canceled, scheduled for load-out, queued behind warehouse capacity, or held off-warrant. Futures open interest becomes economically meaningful only after being compared with the subset of inventory that is actually deliverable under contract rules and within the relevant delivery clock.

The research target is physical tightness, conversion friction and delivery pressure—not simplistic "open interest divided by total vault stock" ratios.

All candidates are research hypotheses only. Claude owns implementation.

## W49P-E01 — COMEX Registered Stock State

Primary source:
CME/COMEX approved depository stock reports.

Registered metal:
eligible exchange-grade metal for which a warrant has been issued.

Track daily by depository/metal.

Priority: S

## W49P-E02 — COMEX Eligible Stock State

Eligible metal:
meets delivery specifications/approved brands but has no exchange warrant issued.

Treat as potentially convertible supply, not immediately equivalent to registered stock.

Priority: S

## W49P-E03 — Registered-to-Eligible Conversion

Feature:
daily eligible -> registered movement.

Hypothesis:
rapid warranting can signal preparation for futures delivery.

Priority: S

## W49P-E04 — Registered-to-Eligible De-Warranting

Feature:
registered -> eligible decline without physical shipment.

Interpretation may include removing immediate exchange delivery status while metal remains in approved storage.

Priority: S-

## W49P-E05 — Physical Vault Inflow / Outflow

CME depositories report receipts and shipments.

Separate:
physical metal arriving/leaving
from
warrant-status changes inside the vault.

Priority: S

## W49P-E06 — Deliverable Stock Lower Bound

Conservative near-term deliverable supply:
registered inventory.

Do not assume all eligible stock is economically available.

Priority: S architecture

## W49P-E07 — Eligible Conversion Probability

Estimate:
P(eligible becomes registered within delivery window)
from:
historical conversion rates,
basis,
lease/funding economics,
depository behavior,
delivery-month state.

Priority: S

## W49P-E08 — Effective Deliverable Supply

General candidate:

effective_deliverable =
registered
+
P(convert eligible in time) × eligible
+
validated external economically deliverable supply.

Maintain uncertainty bands.

Priority: S

## W49P-E09 — Open Interest / Effective Deliverable Ratio

Compare nearby/spot-month open interest with effective deliverable supply.

Do not treat every open contract as intending physical delivery.

Priority: S

## W49P-E10 — First-Notice Compression

As first notice approaches:
track remaining open interest
× warrant inventory
× roll/liquidation velocity.

Priority: S

## W49P-E11 — Delivery Intention Acceleration

Use official daily delivery notices to track:
new delivery intentions,
cumulative deliveries,
remaining open interest.

Priority: S

## W49P-E12 — Issues-vs-Stops Concentration

Where official report fields support:
measure concentration of issuing/stopping clearing members.

Research whether delivery activity is broadly distributed or dominated by a few firms.

Priority: A+

## W49P-E13 — Delivery Concentration Herfindahl

Compute concentration by clearing member/depository/warehouse where report semantics permit.

Priority: A

## W49P-E14 — Registered Stock Burn Rate

Feature:
registered withdrawals + deliveries
relative to
registered replenishment.

Priority: S-

## W49P-E15 — Inventory Replenishment Half-Life

After a delivery-heavy period:
time for registered stock to recover toward normal.

Priority: A+

## W49P-E16 — Metal-Specific Tightness State

Build separate state machines for:
gold,
silver,
copper,
platinum/palladium where data and contract mechanics support.

No universal threshold.

Priority: S

## W49P-E17 — Gold Warrant Pressure

Specialize to GC:
registered ounces
nearby OI equivalents
daily delivery notices
basis/spread
vault inflows.

Priority: S

## W49P-E18 — Silver Warrant Pressure

Specialize to SI.

CME regulatory filings explicitly distinguish daily registered/eligible stocks and have historically used conservative eligible discounts in deliverable-supply estimates.

Priority: S

## W49P-E19 — Copper Delivery Pressure

Specialize to HG:
warehouse stock
warrant state
nearby OI
delivery notices
calendar spread.

Priority: S-

## W49P-E20 — Futures-to-Physical Conversion Stress

When delivery demand rises:
measure whether new warrants are created fast enough to absorb notices.

Priority: S

## W49P-E21 — Delivery-Month Basis Distortion

Research:
calendar spread / spot-month premium
conditioned on effective deliverable scarcity.

Priority: S

## W49P-E22 — Backwardation × Low Deliverable Stock

Theory of storage predicts stronger convenience yield under scarce inventories.

Test whether exchange-deliverable inventory improves explanation beyond broad inventory proxies.

Priority: A+

## W49P-E23 — Exchange Inventory Surprise

Feature:
daily stock change
-
expected stock change given recent deliveries/import flows/seasonality.

Priority: A

## W49P-E24 — Inventory Data Revision / Timing State

Preserve publication time and revised/final states where applicable.

No backfilling.

Priority: Methodology/edge hybrid

## W49P-E25 — LME Live Warrant State

Primary source:
LME warehouse/stock reports.

Track live/open warranted stock by metal/location.

Priority: S-

## W49P-E26 — LME Cancelled Warrant State

LME reports canceled tonnage separately.

Canceled metal remains in warehouse but is generally treated as awaiting load-out rather than freely available live warrant stock.

Priority: S

## W49P-E27 — Cancelled-to-Scheduled Distinction

Where source data allow:
separate canceled-but-not-scheduled
from
metal actually scheduled/queued for load-out.

Priority: S

## W49P-E28 — LME Queue Pressure

LME publishes monthly warehouse queue data including waiting time for queued metal.

Feature:
queued tonnage / load-out capacity
and
reported waiting time.

Priority: S-

## W49P-E29 — LME Load-Out Capacity Constraint

Use LME warehouse minimum load-out rules to estimate the physical time required to remove queued metal.

Priority: A+

## W49P-E30 — LME Off-Warrant Inventory State

LME transitioned to daily off-warrant reporting in 2025, with public delayed access and faster licensed access.

Track separately from live/canceled warranted inventory.

Priority: A+

## W49P-E31 — Warrant Cancellation Without Load-Out

LME has explicitly noted that canceled warrants do not always imply immediate physical removal.

Research:
cancellation persistence
vs
actual delivered-out metal.

Priority: S

## W49P-E32 — Warehouse Location Scarcity

Aggregate by warehouse/location:
live stock,
canceled stock,
deliveries in/out,
queue time.

A global metal surplus can coexist with local delivery scarcity.

Priority: S-

## W49P-E33 — Cross-Exchange Inventory Divergence

Compare:
COMEX warrant state,
LME warehouse state,
other lawful exchange/public inventories.

Question:
does inventory migrate geographically before futures spreads normalize?

Priority: A+

## W49P-E34 — Import-to-Warehouse Conversion

Map verified customs/import flows to later exchange-vault receipts where geography/product timing makes sense.

Priority: A

## W49P-E35 — Delivery Pressure × Financing Cost

Inventory conversion depends partly on carrying/financing economics.

Fuse:
rates,
lease/borrow economics where public,
storage,
calendar spread.

Priority: A+

## W49P-E36 — Delivery Pressure × Position Limits

Spot-month position limits constrain how much one participant can carry into delivery absent exemption.

Model current rules point-in-time.

Priority: A

## W49P-E37 — Delivery Pressure × Short Constraint

Fuse W33 short-constraint state with physical deliverability.

Research whether borrow/short stress and warehouse scarcity amplify one another.

Priority: A+

## W49P-E38 — Physical Market Reality Gap

Compare:
futures price/basis narrative
vs
registered/live inventory,
actual deliveries,
load-out,
queue state.

Priority: S

## W49P-E39 — Effective Physical Coverage Ratio

EPCR =
effective deliverable supply
/
delivery-relevant open interest or expected delivery demand.

Use interval estimates, not false precision.

Priority: S

## W49P-E40 — Delivery Stress Truth Ladder

WAREHOUSE STOCK
-> DELIVERY-ELIGIBLE STATUS
-> WARRANT/LIVE STATUS
-> NOTICE/ASSIGNMENT
-> LOAD-OUT/TRANSFER
-> INVENTORY REPLENISHMENT
-> BASIS/PRICE RESPONSE.

Priority: S architecture

## Highest-priority W49P tests

1. W49P-E03 Registered-to-Eligible Conversion
2. W49P-E07 Eligible Conversion Probability
3. W49P-E09 Open Interest / Effective Deliverable Ratio
4. W49P-E10 First-Notice Compression
5. W49P-E11 Delivery Intention Acceleration
6. W49P-E20 Futures-to-Physical Conversion Stress
7. W49P-E26 LME Cancelled Warrant State
8. W49P-E28 LME Queue Pressure
9. W49P-E31 Warrant Cancellation Without Load-Out
10. W49P-E39 Effective Physical Coverage Ratio
