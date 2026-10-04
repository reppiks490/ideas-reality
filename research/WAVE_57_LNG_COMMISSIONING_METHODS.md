# Wave 57L — Research Methods

Namespace: **W57L**

## W57L-M01 — Docket-Vintage Archive
Archive each FERC docket filing/order at first public availability.

## W57L-M02 — Filing vs Authorization
A developer request is not permission.
Encode REQUESTED and AUTHORIZED separately.

## W57L-M03 — Exact Equipment Scope
Parse each FERC authorization to the exact block/train/system affected.

## W57L-M04 — Train/Block Naming Crosswalk
Operators may call the same hardware Train, Block, Phase or Stage.
Maintain an explicit identity map.

## W57L-M05 — Capacity Denominator
Distinguish:
design,
nominal,
peak,
authorized,
commissioning,
substantially complete,
commercially available capacity.

## W57L-M06 — First-Gas Evidence Hierarchy
Priority:
meter/official filing
> FERC/operator statement
> reliable trade reporting.
Preserve source confidence.

## W57L-M07 — First Cargo != COD
Treat first cargo as commissioning evidence only unless source explicitly defines commercial operations.

## W57L-M08 — EPC Turnover Semantics
"Substantial Completion" is project/contract-specific.
Store exact operator definition.

## W57L-M09 — Schedule Vintage
Never overwrite older expected startup dates with latest guidance.

## W57L-M10 — Feedgas Meter Mapping
Map terminal feedgas to verified pipeline/meter combinations.
Avoid double counting multiple feeds.

## W57L-M11 — Scheduled vs Actual Gas
Pipeline scheduled volumes are not guaranteed actual burn.
Use actual/confirmed flow where lawful/public.

## W57L-M12 — Commissioning Fuel Loss
Feedgas is not identical to LNG export energy due to fuel, boil-off and commissioning inefficiency.

## W57L-M13 — Cargo-Lag Model
Liquefaction, tank accumulation and vessel scheduling create lag between feedgas increase and cargo departure.

## W57L-M14 — Weather Control
Cold/heat can move regional gas demand simultaneously with commissioning.

## W57L-M15 — Pipeline Constraint Control
Use W22G to distinguish terminal demand failure from upstream transport inability.

## W57L-M16 — Facility Outage Control
A commissioning pause may reflect terminal equipment, utility power, upstream gas or marine loading.
Do not infer cause without evidence.

## W57L-M17 — DOE Authorization Gate
Export authority is legal/commercial permission, not physical readiness.

## W57L-M18 — Contract Disclosure Vintage
Use DOE contract-registration public date, not contract-signing date unless already public.

## W57L-M19 — Train-Level Survival Model
Estimate time from milestone to next milestone with right censoring.

## W57L-M20 — Physical Promotion Gate
Before financial alpha require OOS improvement in:
next commissioning milestone,
feedgas,
cargo cadence,
storage balance,
or regional basis.
