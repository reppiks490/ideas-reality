# Wave 46U — Research Methods

Namespace: **W46U**

## W46U-M01 — Docket Identity
Use commission + docket number as case key; map utility/legal entity/ticker separately.

## W46U-M02 — Filing-vs-Order Public Clock
Store filed, posted, issued and effective dates separately.

## W46U-M03 — Requested vs Authorized
Never substitute company-requested economics for commission-approved economics.

## W46U-M04 — Jurisdiction Versioning
Retail/state, FERC transmission and other regulatory jurisdictions use different rules.

## W46U-M05 — Revenue Requirement Scope
Normalize whether amounts are:
annual,
multiyear,
electric,
gas,
distribution,
transmission,
specific rider.

## W46U-M06 — ROE Scope
Authorized ROE applies to defined equity rate base/capital structure, not total company equity.

## W46U-M07 — Settlement Parsing
Identify exact settlement economics and commission modifications.

## W46U-M08 — Proposed Decision Boundary
ALJ/proposed decisions are not final commission authorization.

## W46U-M09 — Cost-Incurred Vintage
Physical cost may be estimated/revised for years before final recovery order.

Archive vintages.

## W46U-M10 — Insurance/Offset Netting
Net insurance, grants, tax benefits, legal recoveries and other credits where ordered.

## W46U-M11 — Disallowance Classification
Separate timing deferral from permanent disallowance.

## W46U-M12 — Securitization Accounting Boundary
Financing approval, bond issuance and customer-charge commencement are separate events.

## W46U-M13 — Formula-Rate True-Up
Projected and actual ATRR can differ; preserve annual true-up mechanics.

## W46U-M14 — FERC eLibrary Timestamp
Use public filed/posted time and accession/docket identifiers.

## W46U-M15 — Rate Effective vs Cash Collection
Authorization date may differ from tariff/rider effective date and actual billing.

## W46U-M16 — Political/Event Endogeneity
Large disasters can simultaneously alter physical costs, policy and regulation.

Control the common event.

## W46U-M17 — Full Case Universe
Avoid selecting only controversial disallowances. Include resolved routine cases.

## W46U-M18 — Promotion Gate
Before equity alpha require OOS improvement in:
authorized revenue,
authorized ROE,
disallowance,
recovery timing,
securitization,
or realized cash recovery.
