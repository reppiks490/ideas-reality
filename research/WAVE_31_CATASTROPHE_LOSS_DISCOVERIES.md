# Wave 31C — Catastrophe Loss Development & Financial Transmission

Namespace: **W31C**

Thesis: physical disaster severity is not the same thing as realized financial loss. Public assistance registrations, inspected damage, insurance claims, claim closure, insured-loss revisions and geographic asset exposure form a loss-development process that unfolds over days to months.

The useful signal is the revision of expected loss and who ultimately absorbs it—not a generic "hurricane bad" feature.

All candidates are research hypotheses only. Claude owns implementation.

## W31C-E01 — FEMA Registration Intake Velocity

Primary source:
OpenFEMA Registration Intake and Individuals Household Program (RI-IHP) v2.

Status:
DAILY public refresh.

Build by disaster/city/geography:
new valid registrations,
registration acceleration,
IHP eligibility,
housing assistance amount,
other-needs assistance amount.

Priority: S-

## W31C-E02 — Assistance Severity per Registration

Candidate:
IHP dollars / valid registration
and
housing assistance dollars / eligible registration.

Track daily vintage.

Priority: A+

## W31C-E03 — Damage-Registration Breadth

Use daily FEMA housing-assistance owner/renter aggregates by ZIP/county.

Features:
registrations,
inspections,
moderate/substantial/major/destroyed counts where available,
assistance.

Priority: S-

## W31C-E04 — FEMA Inspected Damage Development

Housing Assistance Owners includes total/average FEMA-inspected damage and damage buckets.

Build:
damage per inspected owner
× inspection completion share
× geographic exposure.

Priority: S

## W31C-E05 — Inspection Selection Adjustment

Early inspected homes may not be representative.

Model:
P(inspected | geography, event age, application cohort)
and uncertainty around extrapolated damage.

Priority: S methodology/edge hybrid

## W31C-E06 — Disaster Loss Nowcast Curve

At each post-event day:
estimate eventual housing/property loss distribution from available FEMA registration/inspection data.

Never train using future claim development without vintage reconstruction.

Priority: S

## W31C-E07 — Loss Revision Velocity

Feature:
today's eventual-loss estimate
-
yesterday's estimate.

Hypothesis:
revision speed may be more market-relevant than current cumulative loss level.

Priority: S

## W31C-E08 — Geographic Damage Concentration

Measure concentration by ZIP/county:
damaged registrations,
inspected damage,
destroyed homes,
assistance.

Map to:
public-company facilities,
banks,
insurers,
utilities,
REITs,
municipalities.

Priority: A+

## W31C-E09 — Business-Interruption Proxy

Residential FEMA data do not directly measure commercial interruption.

Build a separate proxy from:
communications outage,
power loss,
facility status,
mobility/logistics,
nighttime lights,
emergency declarations.

Use housing damage only as one local severity factor.

Priority: A

## W31C-E10 — NFIP Flood Claim Development

Primary source:
OpenFEMA NFIP Redacted Claims.

Status:
DELAYED; FEMA states claims/policy public data are generally refreshed every 30–60 days and can lag the system of record.

Use:
flood claim count,
building/content damage,
net payments,
water depth,
coverage,
geography.

Priority: A as delayed truth layer

## W31C-E11 — FEMA Assistance vs NFIP Claim Reality Gap

Compare early FEMA assistance/damage nowcast to later NFIP claims.

Target:
eventual NFIP claim count/payment.

This validates whether early public data can predict slower insured loss.

Priority: S

## W31C-E12 — Underinsurance / Assistance Gap

Estimate:
FEMA-verified/inspected loss
vs
NFIP coverage/payment
vs
assistance.

Purpose:
infer household/public-sector residual burden, with strict scope matching.

Priority: A

## W31C-E13 — Florida Catastrophe Claim Development

Primary source:
Florida Office of Insurance Regulation catastrophe claims reporting.

For covered events OIR compels insurer catastrophe reporting and publishes snapshots including:
claim counts,
open/closed with/without payment,
total estimated/incurred insured loss,
line of business.

Priority: S-

## W31C-E14 — Insured-Loss Revision Curve

For each OIR snapshot:
estimated incurred loss_t
claim count_t
closure rate_t
payment status_t.

Model eventual loss from early snapshots.

Priority: S

## W31C-E15 — Claims Closure Friction

Feature:
open claims without payment
/
total claims

plus closure velocity.

Possible interpretation:
complexity, disputed coverage, adjustment bottleneck, severity.

Priority: A

## W31C-E16 — Commercial vs Residential Loss Mix

OIR separates lines including residential/commercial property, private flood, business interruption and others.

Track changing mix.

Priority: A+

## W31C-E17 — Flood vs Wind Coverage Split

Standard homeowners coverage often excludes flood.

Fuse:
private/NFIP flood claims,
homeowner catastrophe claims,
hazard footprint.

Goal:
estimate which balance sheet absorbs the loss.

Priority: A+

## W31C-E18 — Insurer Exposure Attribution

Map catastrophe exposure to public insurers only where state regulatory filings or other point-in-time public data establish market/geographic exposure.

Do not allocate statewide losses by national premium share without evidence.

Priority: S-

## W31C-E19 — Reinsurance Loss Transmission

Graph:
primary insurer
-> reinsurance program/counterparty where public
-> attachment/exhaustion uncertainty
-> retained loss.

Use public statutory/company disclosures and Florida certified-reinsurer context where applicable.

Priority: A

## W31C-E20 — Catastrophe Capital Erosion

Estimate:
expected retained catastrophe loss
/
policyholder surplus or relevant capital base.

Priority: S-

## W31C-E21 — Regional Bank Collateral Damage Exposure

Map verified housing/business damage to:
mortgage/CRE geographic exposure,
branch/deposit footprint,
loan book where public.

Target intermediate:
delinquency/forbearance/credit loss later.

Priority: A

## W31C-E22 — Municipal Fiscal Loss Exposure

Damage can reduce tax base while increasing emergency/rebuild expenditure.

Graph:
damage geography
-> municipality/county
-> tax/property base
-> muni debt.

Fuse with W11C municipal trade stress.

Priority: A

## W31C-E23 — Utility Restoration Cost Nowcast

Fuse:
FEMA damage,
grid outage/restoration,
communications,
vegetation/storm footprint,
utility asset geography.

Target:
restoration duration/cost before quarterly earnings.

Priority: A+

## W31C-E24 — Catastrophe Loss Absorption Graph

Allocate estimated loss among:
household uninsured,
NFIP/private insurer,
reinsurer,
federal assistance,
state/local government,
corporate/business interruption.

Priority: S

## W31C-E25 — Physical Severity vs Financial Loss Gap

Feature:
observed physical disruption severity
-
current financial-loss estimate.

Large disagreement can signal under/overestimated economic impact.

Priority: S

## W31C-E26 — Loss-Development Truth Ladder

HAZARD
-> PHYSICAL DAMAGE
-> FEMA REGISTRATION/INSPECTION
-> CLAIM
-> INCURRED LOSS
-> PAID LOSS
-> CAPITAL/CREDIT EFFECT
-> RECOVERY.

No financial-market claim promotes without respecting this sequence and latency.

Priority: S architecture

## Highest-priority W31C tests

1. W31C-E01 FEMA Registration Intake Velocity
2. W31C-E04 FEMA Inspected Damage Development
3. W31C-E06 Disaster Loss Nowcast Curve
4. W31C-E07 Loss Revision Velocity
5. W31C-E11 FEMA Assistance vs NFIP Reality Gap
6. W31C-E13 Florida Catastrophe Claim Development
7. W31C-E14 Insured-Loss Revision Curve
8. W31C-E18 Insurer Exposure Attribution
9. W31C-E24 Catastrophe Loss Absorption Graph
10. W31C-E25 Physical Severity vs Financial Loss Gap
