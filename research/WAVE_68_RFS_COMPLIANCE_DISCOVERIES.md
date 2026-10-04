# Wave 68R — Renewable Fuel Compliance & RIN Balance

Namespace: **W68R**

Thesis: the Renewable Fuel Standard is a compliance-credit system layered on top of physical biofuel production. Annual obligations, nested D-code substitution, RIN generation/separation/retirement, carryover inventory, small-refinery exemptions, compliance-date changes and rule revisions can change the marginal demand for ethanol, biomass-based diesel and their feedstocks without any change in crude-oil fundamentals.

W20E owns emergency fuel-specification waivers. W68R owns **RFS compliance-credit supply/demand and its physical biofuel/feedstock transmission**.

All candidates are research hypotheses only. Claude owns later implementation.

## W68R-E01 — Annual RVO Rule State
Primary source:
EPA RFS annual rules.

Track by compliance year:
cellulosic,
biomass-based diesel,
advanced,
total renewable
volume and percentage standards.

Priority: S

## W68R-E02 — RVO Revision Surprise
Feature:
final applicable obligation
-
prior public proposal / prior official guidance expectation.

Priority: S

## W68R-E03 — SRE Petition Decision Event
Primary source:
EPA Small Refinery Exemption decisions.

Normalize:
FULL_EXEMPTION
PARTIAL_EXEMPTION
DENIED
INELIGIBLE
PENDING.

Priority: S

## W68R-E04 — Exempted-RIN Volume Shock
Translate SRE decisions into RIN-equivalent obligation relief where EPA publishes aggregate volumes.

Priority: S

## W68R-E05 — SRE Decision Breadth
Track:
petition count,
full/partial/denied share,
affected compliance years,
aggregate exempted RINs.

Do not infer confidential refinery identities.

Priority: A+

## W68R-E06 — SRE Reallocation State
EPA can reallocate exempted volume into later/current-year standards under specific rulemaking.

Track:
PROJECTED_REALLOCATION
PROPOSED
FINAL
IMPLEMENTED.

Priority: S

## W68R-E07 — Reallocation Delta
Feature:
new applicable RVO after reallocation
-
pre-reallocation obligation.

Priority: S

## W68R-E08 — Compliance Deadline State
Track exact annual compliance date and extensions.

State:
NORMAL
EXTENDED
NEAR_DEADLINE
COMPLETED.

Priority: S-

## W68R-E09 — Deadline Compression
Feature:
days remaining to compliance
× outstanding estimated RIN need.

Priority: S

## W68R-E10 — D3/D7 Cellulosic RIN Generation
Primary source:
EPA EMTS aggregated monthly data.

Compare generated cellulosic RINs to applicable cellulosic obligation path.

Priority: S

## W68R-E11 — D4 Biomass-Based Diesel RIN Generation
Track monthly/rolling D4 generation and physical renewable-fuel volume.

Priority: S

## W68R-E12 — D5 Advanced RIN Generation
Track non-BBD advanced fuel generation.

Priority: A+

## W68R-E13 — D6 Conventional RIN Generation
Track conventional renewable-fuel generation, dominated structurally by qualifying ethanol pathways.

Priority: S-

## W68R-E14 — Monthly RIN Generation Surprise
Feature:
actual monthly RIN generation
-
seasonal/pathway-specific expectation.

Priority: S

## W68R-E15 — RIN Separation Velocity
Primary source:
EPA RIN Separation data.

Feature:
newly separated RINs
by D-code/vintage.

Priority: A+

## W68R-E16 — RIN Retirement Velocity
Primary source:
EPA RIN Retirement data.

Separate compliance retirement from other retirement reasons where public fields permit.

Priority: S

## W68R-E17 — Available-RIN Inventory
Primary source:
EPA Available RINs.

Track:
generated,
retired,
locked,
unlocked,
available
by D-code/vintage where source supports.

Priority: S

## W68R-E18 — Carryover-Bank Pressure
Estimate usable prior-year/current-year RIN inventory relative to forward obligation.

Use exact regulatory vintage eligibility.

Priority: S

## W68R-E19 — RIN Deficit / Excess
For each nested obligation:
available eligible RIN supply
-
expected remaining obligation.

Output as range because obligated-party holdings and future generation are uncertain.

Priority: S

## W68R-E20 — Nested D-Code Substitution Pressure
EPA's standards are nested:
D3/D7 can satisfy cellulosic and broader categories under applicable rules,
D4 can satisfy BBD and broader advanced/total obligations,
D5 can satisfy advanced/total,
D6 total only.

Model marginal substitution value rather than isolated D-code deficits.

Priority: S

## W68R-E21 — Marginal Compliance RIN
Estimate which D-code is likely setting the marginal compliance constraint.

Priority: S

## W68R-E22 — Equivalence-Value Translation
One physical gallon can generate more or less than one RIN depending on fuel/pathway equivalence value.

Convert RIN obligations into physical-gallon demand using exact approved pathway/equivalence rules.

Priority: S methodology/edge hybrid

## W68R-E23 — BBD Physical-Gallon Demand
Translate D4 obligation/generation gap into required biodiesel/renewable-diesel-equivalent gallons under pathway assumptions.

Priority: S

## W68R-E24 — Feedstock Demand Envelope
Map incremental BBD production need to:
soybean oil,
canola oil,
distillers corn oil,
tallow/grease,
used cooking oil,
other approved feedstocks.

Use a range based on pathway mix.

Priority: S

## W68R-E25 — Soybean-Oil RFS Pressure
Feature:
marginal BBD RIN deficit
× expected soybean-oil share of incremental feedstock demand
/
available domestic/import supply.

Priority: S-

## W68R-E26 — Renewable-Diesel / Biodiesel Substitution
Same D4 obligation can be met by different eligible BBD fuels.

Estimate marginal production economics by plant/fuel/feedstock where public.

Priority: A+

## W68R-E27 — D6 Ethanol Compliance Pressure
Translate total-renewable residual after higher D-codes into conventional D6 need.

Priority: S-

## W68R-E28 — Ethanol Blend-Wall Constraint
Compare implied ethanol/RIN requirement to feasible domestic blend demand:
E10,
E15/E85,
exports,
other qualifying pathways.

Priority: S

## W68R-E29 — RIN Bank × Blend-Wall Interaction
A large bank can cushion a near-term physical blending constraint; a thin bank can force higher marginal compliance cost.

Priority: S

## W68R-E30 — RIN Price Constraint State
Using lawful market data:
D3/D4/D5/D6 prices and spreads.

Treat price as market-implied scarcity, not as ground truth about physical supply.

Priority: S

## W68R-E31 — D4-D6 Spread State
D4 minus D6 can reflect incremental value of advanced/BBD eligibility.

Research relation to feedstock and renewable-diesel economics.

Priority: A+

## W68R-E32 — Refinery Compliance Burden
Estimate:
RIN requirement
× marginal RIN price
relative to:
refining margin,
throughput,
RIN generation/blending capability.

Priority: S

## W68R-E33 — Merchant Refiner vs Integrated Blender Divergence
Refiners with different blending/RIN-generation positions face different compliance economics.

Require public exposure evidence.

Priority: A+

## W68R-E34 — SRE Relief Distribution
SRE relief can create asymmetric compliance changes among small refiners versus non-exempt obligated parties.

Do not assign relief to a named refinery unless EPA/public filings identify it.

Priority: A+

## W68R-E35 — RIN Generation vs Physical Production Gap
Compare EPA RIN generation with EIA/USDA physical ethanol/biodiesel/renewable-diesel output.

Large disagreement can indicate pathway/equivalence, timing or data-quality effects.

Priority: S-

## W68R-E36 — RIN Bank vs Physical Tightness Reality Gap
A physically tight feedstock/biofuel market can coexist with a large credit bank, or vice versa.

State:
PHYSICAL_TIGHT_RIN_LOOSE
PHYSICAL_LOOSE_RIN_TIGHT
BOTH_TIGHT
BOTH_LOOSE.

Priority: S

## W68R-E37 — Compliance-Demand Revision Momentum
Track sequential changes from:
proposal,
final rule,
SRE decisions,
reallocation,
deadline extensions,
monthly generation/retirements.

Priority: S

## W68R-E38 — Cellulosic Waiver Credit State
Where applicable:
track EPA cellulosic waiver credit availability/price and interaction with D3 compliance.

Priority: A

## W68R-E39 — eRIN Regime Break
EPA's 2026/2027 final rule removed renewable electricity as a qualifying RFS renewable fuel.

Treat prior proposed eRIN architecture as non-operative after the final rule unless later law/rule changes it.

Priority: A+

## W68R-E40 — Renewable-Fuel Compliance Quotient
RFCQ =
remaining RIN-equivalent obligation
/
expected eligible RIN generation + usable bank.

Compute by nested category with uncertainty.

Priority: S

## W68R-E41 — Physical Biofuel Requirement Quotient
PBRQ =
RIN deficit translated to physical renewable-fuel demand
/
available production + import + inventory + blending/export absorption capacity.

Priority: S

## W68R-E42 — RFS Truth Ladder
RULE / RVO
-> SRE / REALLOCATION
-> RIN GENERATION
-> SEPARATION / BANK
-> RETIREMENT / COMPLIANCE
-> PHYSICAL BIOFUEL PRODUCTION
-> FEEDSTOCK DEMAND
-> REFINERY / AGRICULTURAL ECONOMICS
-> PRICE RESPONSE.

Priority: S architecture

## Highest-priority W68R tests

1. W68R-E04 Exempted-RIN Volume Shock
2. W68R-E06 SRE Reallocation State
3. W68R-E09 Deadline Compression
4. W68R-E14 Monthly RIN Generation Surprise
5. W68R-E18 Carryover-Bank Pressure
6. W68R-E20 Nested D-Code Substitution Pressure
7. W68R-E23 BBD Physical-Gallon Demand
8. W68R-E28 Ethanol Blend-Wall Constraint
9. W68R-E36 RIN Bank vs Physical Tightness Reality Gap
10. W68R-E40 Renewable-Fuel Compliance Quotient
