# Wave 46U — Utility Rate Recovery & Regulatory Economics

Namespace: **W46U**

Thesis: physical utility costs do not map one-for-one into shareholder loss. State commissions and FERC can authorize, defer, disallow, securitize, true-up, or shift costs between customers and shareholders. Rate cases and related orders create explicit economic state transitions in revenue requirement, authorized return, capital recovery and storm/wildfire burden.

The research target is **regulatory conversion of physical cost into recoverable earnings/cash flow**, not generic utility-regulation sentiment.

All candidates are research hypotheses only. Claude owns later implementation.

## W46U-E01 — General Rate Case Filing Pulse

Normalize public rate-case filing:
utility,
commission,
docket,
requested revenue increase,
requested ROE,
requested capital structure,
test year,
rate base,
proposed effective date.

Priority: S

## W46U-E02 — Requested-vs-Authorized Revenue Gap

Feature:
authorized annual revenue requirement
-
requested annual revenue requirement.

Priority: S

## W46U-E03 — Requested-vs-Authorized ROE Gap

Feature:
authorized ROE
-
requested ROE.

Use exact jurisdiction/rate base scope.

Priority: S

## W46U-E04 — Rate-Base Recognition Gap

Compare:
requested rate base
vs
recognized/authorized rate base.

Potential disallowance:
plant,
CWIP,
abandoned project,
prudence adjustment,
capitalization issue.

Priority: S-

## W46U-E05 — Interim Rate State

Some jurisdictions permit interim/temporary rates subject to refund.

State:
FILED
INTERIM_EFFECTIVE
FINAL_ORDER
REFUND/TRUE_UP.

Priority: A+

## W46U-E06 — Procedural Schedule Clock

Track public:
filing,
intervention,
testimony,
hearing,
settlement,
proposed decision,
final order,
effective date.

No universal state-PUC timeline; use docket-specific schedules.

Priority: S

## W46U-E07 — Settlement Probability

Estimate:
P(rate case resolves by settlement)
and economics relative to litigated outcome.

Priority: A

## W46U-E08 — Proposed-vs-Final Decision Gap

Where a proposed/ALJ decision precedes commission vote:
feature =
final economics - proposed economics.

Priority: S-

## W46U-E09 — Authorized Return Spread

authorized ROE
-
relevant market cost-of-equity / bond-yield benchmark.

Use only as valuation/funding context, not guaranteed realized return.

Priority: A+

## W46U-E10 — Regulatory Lag

Measure:
cost incurred
-> filing
-> authorization
-> rate collection.

Priority: S

## W46U-E11 — Cost Deferral State

Track regulatory assets/memorandum accounts:
DEFERRAL_ALLOWED
RECOVERY_UNDECIDED
RECOVERY_APPROVED
PARTIAL_DISALLOWANCE
FULL_DISALLOWANCE.

Priority: S

## W46U-E12 — Storm-Cost Recovery

Estimate:
storm restoration cost requested
vs
recoverable amount
vs
recovery period.

Priority: S

## W46U-E13 — Wildfire-Cost Recovery

Separate:
claims,
restoration,
mitigation,
vegetation management,
legal expenses,
insurance proceeds,
shareholder-funded amounts.

Priority: S

## W46U-E14 — Prudence Disallowance Ratio

PDR =
permanently disallowed cost
/
cost submitted for recovery.

Priority: S

## W46U-E15 — Shareholder Loss Transfer

Feature:
cost incurred
-
expected customer recovery
-
insurance/reinsurance recovery
-
other offsets.

Priority: S

## W46U-E16 — Securitization Approval State

State:
REQUESTED
APPROVED
DENIED
BOND_PENDING
BOND_ISSUED
TRUE_UP_ACTIVE.

Priority: S-

## W46U-E17 — Securitization Economics

Compare:
authorized securitized cost recovery
vs
traditional utility financing.

Track:
principal,
term,
fixed recovery charge,
estimated NPV customer savings,
shareholder balance-sheet relief.

Priority: A+

## W46U-E18 — Recovery-Bond True-Up

Where authorized:
track periodic true-up mechanisms for nonbypassable charges.

Priority: A

## W46U-E19 — Fuel / Purchased-Power Adjustment

Track automatic or periodic riders:
fuel,
purchased power,
gas,
transmission,
capacity.

Feature:
recoverable pass-through
vs
lag / prudence exposure.

Priority: S-

## W46U-E20 — Formula-Rate Annual Update

Primary source:
FERC eLibrary for jurisdictional transmission formula rates.

Track:
annual transmission revenue requirement,
rate-base inputs,
capital structure,
ROE,
true-up.

Priority: S

## W46U-E21 — Formula-Rate Challenge

State:
ANNUAL_UPDATE
INFORMAL_CHALLENGE
FORMAL_CHALLENGE
SETTLEMENT
FERC_ORDER
COMPLIANCE.

Priority: S-

## W46U-E22 — FERC Section 205 Filing State

Public utility files proposed rate/tariff change with requested effective date.

Track:
filed,
accepted,
suspended,
hearing/settlement,
effective.

Priority: A+

## W46U-E23 — FERC Section 206 Risk

Commission/complainant challenges existing rate as unjust/unreasonable.

Track:
complaint/order instituting proceeding,
refund effective date where applicable,
settlement/order.

Priority: S-

## W46U-E24 — Transmission ROE Reset

Estimate earnings/cash-flow impact of FERC-authorized ROE change on relevant transmission rate base.

Priority: S

## W46U-E25 — Abandoned-Plant Recovery

When a transmission/generation project is canceled:
track allowed recovery of prudently incurred costs and any incentive treatment.

Priority: A

## W46U-E26 — Cost Allocation Shock

Transmission project cost responsibility can shift across zones/customers.

Map:
project
-> allocated utility/zone share
-> recoverability mechanism.

Priority: A+

## W46U-E27 — Regulatory Asset Build

Feature:
growth in deferred/regulatory assets
relative to
equity/cash flow.

Question:
when does delayed recovery become a financing burden?

Priority: S-

## W46U-E28 — Rate Shock Affordability Feedback

Large authorized customer rate increases can create:
political pressure,
future disallowance risk,
arrearages,
demand response,
regulatory intervention.

Priority: A

## W46U-E29 — Physical Event × Recovery Probability

Fuse existing outage/wildfire/storm waves with jurisdiction-specific recovery rules.

Same physical loss can have different shareholder outcomes by jurisdiction.

Priority: S

## W46U-E30 — Utility Recovery Capacity Quotient

URCQ =
expected recoverable present value
/
physical + financing cost incurred.

Priority: S

## W46U-E31 — Regulatory-Earnings Reality Gap

Compare:
authorized recovery/ROE
vs
actual realized earnings/cash flow.

Possible causes:
lag,
volume,
cost overruns,
disallowance,
capital structure,
operational underperformance.

Priority: S

## W46U-E32 — Utility Regulatory Truth Ladder

PHYSICAL COST
-> DEFERRAL/FILING
-> PROCEDURAL STATE
-> AUTHORIZED ECONOMICS
-> RATE EFFECTIVE
-> CASH RECOVERY
-> REALIZED EARNINGS.

Priority: S architecture

## Highest-priority W46U tests

1. W46U-E02 Requested-vs-Authorized Revenue Gap
2. W46U-E03 Requested-vs-Authorized ROE Gap
3. W46U-E10 Regulatory Lag
4. W46U-E14 Prudence Disallowance Ratio
5. W46U-E15 Shareholder Loss Transfer
6. W46U-E16 Securitization Approval State
7. W46U-E20 Formula-Rate Annual Update
8. W46U-E24 Transmission ROE Reset
9. W46U-E29 Physical Event × Recovery Probability
10. W46U-E30 Utility Recovery Capacity Quotient
