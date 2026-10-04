# Wave 47S — Sanctions & Export-Control Transaction Eligibility

Namespace: **W47S**

Thesis: sanctions and export controls change the legal eligibility of counterparties, goods, technology, vessels, aircraft and supply-chain relationships. These state changes can instantly invalidate transactions or force wind-downs before ordinary trade, revenue or production statistics reflect the disruption.

The research target is not geopolitical sentiment. It is the exact, point-in-time transition in legal transaction eligibility and the resulting physical/supply-chain response.

All candidates are research hypotheses only. Claude owns any later implementation.

## W47S-E01 — OFAC SDN State Transition

Primary source:
OFAC Sanctions List Service.

Track:
ADDED
MODIFIED
REMOVED

for persons, entities, vessels and aircraft.

Priority: S

## W47S-E02 — OFAC Non-SDN Restriction State

Use OFAC Consolidated Non-SDN lists separately from SDN.

Different lists impose different restrictions.

Never collapse all sanctions-list membership into one blocked/not-blocked bit.

Priority: S-

## W47S-E03 — 50 Percent Rule Ownership Propagation

OFAC guidance blocks entities owned 50% or more in aggregate by one or more blocked persons, even if the owned entity is not itself named on the SDN list.

Build:
blocked-owner graph
-> aggregate ownership
-> inferred blocked subsidiaries.

Priority: S

## W47S-E04 — Sanctions Ownership Cascade Depth

Measure how far newly blocked ownership propagates through corporate structures.

Output:
directly listed
first-order 50% block
second-order block
uncertain control-only exposure.

Priority: A+

## W47S-E05 — OFAC General License Window

Track exact authorization state:
NOT_AUTHORIZED
AUTHORIZED
WIND_DOWN_ONLY
EXPIRED
SUSPENDED.

General Licenses can create legally defined transaction windows.

Priority: S

## W47S-E06 — General License Time-to-Expiry

Feature:
minutes/hours/days until authorization expires.

Use exact timezone and official text.

Priority: S

## W47S-E07 — Wind-Down Compression Pressure

When OFAC authorizes only a finite wind-down period:
estimate transactions/shipments/payment obligations that must be completed before expiry.

Priority: S-

## W47S-E08 — OFAC Delisting Relief

Removal or authorization can restore transaction eligibility.

Track whether:
banking,
shipping,
insurance,
trade,
settlement
actually recover after legal relief.

Priority: A+

## W47S-E09 — Sanctioned Vessel State

OFAC SDN data can include vessel identifiers such as IMO number, MMSI, call sign and flag.

Map newly designated vessel
-> cargo
-> owner/operator
-> route
-> terminal exposure.

Priority: S

## W47S-E10 — Sanctioned Fleet Capacity Loss

Estimate:
designated vessel deadweight/capacity
/
relevant trade-lane fleet capacity.

Priority: S-

## W47S-E11 — Maritime Reflag / Rename Evasion State

Track aliases, prior names, flags, IMO identity and ownership changes.

IMO identity dominates name-based matching where available.

Priority: A+

## W47S-E12 — Sanctioned Aircraft State

OFAC can identify aircraft/tail/serial details.

Map to:
operator,
fleet role,
route/cargo exposure,
maintenance/support eligibility.

Priority: A

## W47S-E13 — BIS Entity List Addition Shock

Primary source:
BIS Entity List / Federal Register / CSL.

For each added party:
effective date/time,
country/address,
license requirements,
license-review policy,
license-exception availability,
footnotes.

Priority: S

## W47S-E14 — Entity List Removal / Modification Relief

Track:
REMOVED
LICENSE_POLICY_EASED
REQUIREMENT_BROADENED
FOOTNOTE_CHANGED.

Priority: S-

## W47S-E15 — Entity-List Address Risk

BIS can list addresses associated with risky transshipment activity.

Research exposure of exporters/suppliers to newly restricted addresses even where legal entity resolution is uncertain.

Priority: A

## W47S-E16 — BIS Denied Persons State

Denied Persons List entries include effective/expiration dates and denial type.

State:
ACTIVE_DENIAL
PARTIALLY_SUSPENDED
EXPIRING
EXPIRED
MODIFIED.

Priority: S-

## W47S-E17 — Temporary Denial Order Clock

BIS Temporary Denial Orders can deny export privileges for up to 180 days, with renewal procedures.

Feature:
time to expiration
renewal filing
renewal outcome.

Priority: S

## W47S-E18 — TDO Counterparty Contagion

Map firms that transact with a TDO subject where the order terms prohibit participation.

Do not assume every commercial relationship is prohibited; parse order scope.

Priority: A+

## W47S-E19 — Unverified List Escalation State

BIS Unverified List imposes enhanced transaction requirements and removes license-exception availability for affected transactions.

State:
NORMAL
UVL
REMOVED
ESCALATED_TO_ENTITY_LIST.

Priority: A+

## W47S-E20 — End-Use-Check Escalation Clock

Where public policy makes timing relevant:
failed/delayed end-use verification
-> UVL
-> possible Entity List escalation.

Use only explicit current BIS rules/policies.

Priority: A

## W47S-E21 — Consolidated Screening List Delta

Primary source:
trade.gov Consolidated Screening List API/download.

Build a normalized delta across Commerce, State and Treasury restricted-party lists.

Priority: S infrastructure/edge hybrid

## W47S-E22 — Legal-Eligibility Matrix

For each counterparty/product transaction:
party state
country state
item/ECCN state
end-use state
license-exception state
general-license state.

Output:
ALLOWED
LICENSE_REQUIRED
WIND_DOWN_ONLY
PROHIBITED
UNKNOWN.

Priority: S

## W47S-E23 — Export-Control Product Exposure

Map public companies/products to controlled technology categories only where ECCN/product evidence is sourced.

Potential high-value sectors:
advanced computing,
semiconductor manufacturing equipment,
aerospace,
telecom,
encryption,
sensors,
machine tools.

Priority: S-

## W47S-E24 — Customer Revenue at Eligibility Risk

For U.S./allied suppliers:
verified revenue/customer relationship
× new restricted-party state
× product subject-to-control probability.

Priority: S

## W47S-E25 — Supplier Substitution Opportunity

A restricted customer may substitute toward:
domestic supplier,
non-U.S. supplier,
uncontrolled technology,
licensed alternative.

Map beneficiaries separately from impaired suppliers.

Priority: A+

## W47S-E26 — Foreign Direct Product Rule Exposure

Entity-list footnotes and EAR rules can extend controls to certain foreign-produced items.

Model only when:
applicable rule version,
product lineage,
technology/equipment origin,
party footnote
are known.

Priority: S methodology/edge hybrid

## W47S-E27 — License-Policy Severity Score

Different listed parties face different review policies:
presumption of denial,
case-by-case,
other rule-specific treatment.

Encode exact policy rather than generic blacklist severity.

Priority: A+

## W47S-E28 — Sanctions Payment-Rail Interruption

Map newly blocked entities to:
banks,
correspondent relationships,
trade finance,
insurance,
shipping payment dependencies.

Use public evidence, not speculative banking relationships.

Priority: A

## W47S-E29 — Export-Control Supply-Chain Propagation

Graph:
restricted customer
-> direct supplier
-> supplier's supplier
-> substitute vendor
-> logistics/financing node.

Target:
physical order cancellation,
shipment diversion,
revenue exposure,
inventory buildup.

Priority: S

## W47S-E30 — Restriction-to-Trade-Flow Lag

Measure time from legal effective date to:
export-license change,
shipment decline,
customs detentions,
inventory adjustment,
supplier revenue effect.

Priority: S

## W47S-E31 — Pre-Effective Announcement Gap

Some rule text/press reports may become public before formal legal effectiveness.

Separate:
first public information time
from
effective legal time.

Priority: S

## W47S-E32 — Rule Revision Shock

Compare old vs new rule:
affected products
affected parties
country scope
license policy
exceptions.

Feature:
incremental transaction set newly restricted or newly authorized.

Priority: S

## W47S-E33 — Restriction Breadth by Index

Aggregate public-company exposure by:
NDX,
SPX,
SOX,
sector,
country revenue.

Priority: S-

## W47S-E34 — NQ Semiconductor Control Exposure

Specialize to NQ/SOX:
advanced computing,
GPU,
EDA,
semicap equipment,
networking,
memory/foundry supplier exposure.

Require direct product/customer evidence.

Priority: S

## W47S-E35 — Sanctions / Freight Reality Gap

Legal transaction becomes restricted but physical vessel/trade flow initially continues.

Track:
legal state
vs
AIS/customs/port reality.

Priority: S

## W47S-E36 — Delisting / Physical Recovery Gap

Legal relief may not immediately restore:
banking,
insurance,
shipping,
customer trust,
supply contracts.

Measure recovery half-life.

Priority: A+

## W47S-E37 — Transaction Eligibility Shock Quotient

TESQ =
economically exposed transaction value newly made unavailable
/
credible substitute transaction capacity.

Priority: S

## W47S-E38 — Sanctions Truth Ladder

PUBLIC ACTION
-> LEGAL EFFECT
-> COUNTERPARTY/PRODUCT ELIGIBILITY
-> ORDER/SHIPMENT/PAYMENT CHANGE
-> PHYSICAL FLOW CHANGE
-> REVENUE/INVENTORY EFFECT
-> MARKET.

Priority: S architecture

## Highest-priority W47S tests

1. W47S-E03 50 Percent Rule Ownership Propagation
2. W47S-E05 OFAC General License Window
3. W47S-E09 Sanctioned Vessel State
4. W47S-E13 BIS Entity List Addition Shock
5. W47S-E17 Temporary Denial Order Clock
6. W47S-E22 Legal-Eligibility Matrix
7. W47S-E24 Customer Revenue at Eligibility Risk
8. W47S-E29 Export-Control Supply-Chain Propagation
9. W47S-E34 NQ Semiconductor Control Exposure
10. W47S-E37 Transaction Eligibility Shock Quotient
