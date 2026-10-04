# Wave 50T — Trade Remedy & Tariff State

Namespace: **W50T**

Thesis: import economics can change discontinuously when antidumping/countervailing duties, Section 232 tariffs, Section 301 tariffs, exclusions, quota rules or HTS classifications change. These are not generic macro tariff stories; they are exact legal state transitions that alter landed cost, cash-deposit requirements, sourcing viability and substitution incentives.

All candidates are research hypotheses only. Claude owns any later implementation.

## W50T-E01 — AD/CVD Case State Machine

Primary source:
U.S. Department of Commerce Enforcement & Compliance / ACCESS.

States:
PETITION
INITIATED
PRELIMINARY
FINAL
ORDER
ADMIN_REVIEW
SCOPE
SUNSET
REVOKED.

Priority: S

## W50T-E02 — Preliminary Cash-Deposit Shock

Commerce states affirmative preliminary AD/CVD determinations instruct CBP to require cash deposits at preliminary rates from Federal Register publication, subject to case/rule details.

Feature:
new cash-deposit rate
-
prior rate.

Priority: S

## W50T-E03 — Producer-Specific Duty Dispersion

Many cases assign different exporter/producer rates.

Track:
company-specific
combination rate
all-others/countrywide rate.

Priority: S-

## W50T-E04 — AD + CVD Combined Landed-Cost Burden

Where concurrent AD and CVD apply:
combine legally applicable deposit obligations without double-counting subsidy offsets.

Priority: S

## W50T-E05 — Preliminary-to-Final Rate Revision

Feature:
final duty/deposit rate
-
preliminary rate.

Priority: S

## W50T-E06 — Critical-Circumstances Retroactivity

Where Commerce/ITC findings permit:
model potential retroactive suspension/cash-deposit exposure for entries before preliminary determination, according to exact statute/order.

Priority: A+

## W50T-E07 — Negative-to-Affirmative Injury Transition

USITC injury determinations are required for many AD/CVD orders.

Track:
preliminary injury
final injury
termination.

Priority: S-

## W50T-E08 — Investigation Calendar Risk

Commerce/USITC publish expected announcement/vote dates.

Feature:
days to next statutory decision
× expected duty exposure.

Priority: A+

## W50T-E09 — Scope Boundary Risk

An order applies to merchandise scope, not merely an HTS code.

Track scope language and later scope rulings separately.

Priority: S

## W50T-E10 — Scope-Ruling Shock

A Commerce scope ruling can bring a product within or outside an existing order.

Feature:
transaction set newly covered/relieved.

Priority: S

## W50T-E11 — Circumvention Determination Shock

Where Commerce finds circumvention:
map third-country processing/assembly routes newly pulled into order coverage.

Priority: S-

## W50T-E12 — Administrative Review Rate Reset

Annual/periodic administrative reviews can alter exporter-specific rates and liquidation liability.

Separate:
cash deposit rate
from
final assessed duty for prior entries.

Priority: A+

## W50T-E13 — Cash Deposit vs Final Liability Gap

Feature:
current cash deposit
-
expected/final assessment.

Important for importer working-capital and contingent liability.

Priority: A

## W50T-E14 — Suspension Agreement State

Some cases use suspension agreements instead of standard order path.

State:
AGREEMENT_ACTIVE
VIOLATION_REVIEW
TERMINATED
ORDER_RESUMED.

Priority: B+

## W50T-E15 — Section 232 Tariff State

Track by product/country:
base tariff
Section 232 additional duty
quota/TRQ state
exclusion.

Priority: S-

## W50T-E16 — Section 232 Product Exclusion Window

For approved/existing exclusions:
effective start
remaining quantity where applicable
expiration.

Priority: A

## W50T-E17 — Section 232 Country Substitution

When one origin becomes relatively more/less burdened:
estimate substitution to exempt/lower-duty origin subject to product compatibility/capacity.

Priority: A+

## W50T-E18 — Section 301 Additional Duty State

Track USTR Section 301 action by:
HTS subheading
country/origin rule
additional rate
effective date.

Priority: S

## W50T-E19 — Section 301 Exclusion Expiry Clock

USTR exclusions can have exact expiration dates.

Feature:
days/hours to exclusion expiry
× import exposure.

Priority: S

## W50T-E20 — Section 301 Exclusion Extension Relief

Track extensions/reinstatements as new legal states.

Do not assume extension until official publication.

Priority: S-

## W50T-E21 — HTS Revision Delta

Primary source:
USITC Harmonized Tariff Schedule revision archive.

Diff successive revisions:
rates,
Chapter 99 provisions,
statistical breakouts,
special notes.

Priority: S

## W50T-E22 — Chapter 99 Overlay Resolver

Additional duties/exclusions often operate through Chapter 99 in addition to ordinary HTS classification.

Build exact multi-line entry requirement state.

Priority: S

## W50T-E23 — Product Classification Uncertainty

If product-to-HTS mapping is uncertain:
represent alternate classifications and landed-cost range.

Priority: S methodology/edge hybrid

## W50T-E24 — Tariff Stack Calculator

For an import transaction estimate:
ordinary duty
+ Section 232
+ Section 301
+ AD/CVD deposit
+ other applicable special duties
subject to exclusion/offset rules.

Priority: S

## W50T-E25 — Landed-Cost Shock

Candidate:
new legal tariff stack
-
old legal tariff stack

× customs value.

Priority: S

## W50T-E26 — Direct Importer Exposure

Map public company to affected imports only with verified:
HTS,
origin,
importer/entity relationship,
volume/value.

Priority: S-

## W50T-E27 — Supplier Pass-Through Exposure

Domestic firms can face higher input cost through suppliers importing tariffed goods.

Map one-hop/two-hop exposure with evidence and uncertainty.

Priority: A+

## W50T-E28 — Domestic Producer Protection State

Tariffs can improve relative pricing for domestic substitutes.

Estimate:
affected import share
× domestic spare capacity
× product substitutability.

Priority: S-

## W50T-E29 — Import Front-Loading Before Effective Date

If future tariff increase is announced before legal effectiveness:
research acceleration of entries/imports before cutoff.

Priority: S

## W50T-E30 — Post-Tariff Inventory Overhang

Front-loaded imports can create temporary domestic inventory surplus after tariff starts.

Priority: A+

## W50T-E31 — Tariff Evasion / Route Substitution Risk

Track verified changes in:
country of origin
transshipment
minor processing
classification.

Do not label evasion without enforcement evidence.

Priority: A

## W50T-E32 — Trade Remedy × Border Detention

Fuse W40 border-detention state with tariff/trade-remedy exposure.

Question:
do compliance/enforcement frictions amplify legal duty shock?

Priority: A+

## W50T-E33 — Trade Remedy × Sanctions Eligibility

Fuse W47S.

A nominally tariff-attractive substitute may be legally unavailable under sanctions/export controls.

Priority: S-

## W50T-E34 — Commodity Import-Cost Shock

Specialize to:
steel,
aluminum,
copper products,
solar inputs,
chemicals,
agricultural/food items
where active cases exist.

Priority: S-

## W50T-E35 — Semiconductor / Tech Input Tariff Exposure

Map NQ-relevant hardware inputs only with verified HTS and sourcing.

Priority: A+

## W50T-E36 — Tariff Shock Quotient

TSQ =
tariff-induced cost on economically exposed imports
/
credible substitute supply + pricing power buffer.

Priority: S

## W50T-E37 — Tariff Reality Gap

Compare legal landed-cost change to:
actual import volume,
supplier prices,
inventory,
company margins.

Priority: S

## W50T-E38 — Trade Remedy Truth Ladder

PETITION/ANNOUNCEMENT
-> LEGAL PUBLICATION
-> DUTY/DEPOSIT EFFECT
-> ENTRY/ORDER CHANGE
-> IMPORT FLOW
-> INVENTORY/PRICE
-> CORPORATE MARGIN
-> MARKET.

Priority: S architecture

## Highest-priority W50T tests

1. W50T-E02 Preliminary Cash-Deposit Shock
2. W50T-E05 Preliminary-to-Final Rate Revision
3. W50T-E09 Scope Boundary Risk
4. W50T-E10 Scope-Ruling Shock
5. W50T-E19 Section 301 Exclusion Expiry Clock
6. W50T-E21 HTS Revision Delta
7. W50T-E24 Tariff Stack Calculator
8. W50T-E29 Import Front-Loading Before Effective Date
9. W50T-E36 Tariff Shock Quotient
10. W50T-E37 Tariff Reality Gap
