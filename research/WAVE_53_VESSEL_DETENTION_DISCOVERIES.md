# Wave 53V — Vessel Detention & Maritime Eligibility

Namespace: **W53V**

Thesis: a vessel may be physically seaworthy enough to exist, yet legally unavailable for commerce because Port State Control, flag-state action, safety deficiencies, denial-of-entry rules, or class/recognized-organization concerns prevent normal operation. These vessel-level legal states can remove cargo capacity independently of weather, port congestion or charter demand.

This wave complements W24M marine operability by modeling whether the **vessel itself** remains eligible to sail, call and carry cargo.

All candidates are research hypotheses only. Claude owns any later implementation.

## W53V-E01 — USCG Port State Detention Event

Primary source:
U.S. Coast Guard Port State Control detention list.

Track by IMO number:
detention date,
port,
flag,
ship type,
recognized organization,
deficiency summary,
validation status.

Priority: S

## W53V-E02 — Detention-to-Release Duration

Measure:
release time/date
-
detention time/date.

Where exact release time is unavailable in the public dataset, retain interval uncertainty.

Priority: S

## W53V-E03 — Detention Capacity Loss

Translate detained vessel into:
deadweight,
TEU,
LNG capacity,
tanker barrels,
bulk capacity,
vehicle capacity,
passenger capacity
as applicable.

Priority: S

## W53V-E04 — Cargo-on-Board Exposure

Where lawful/public:
detention while laden
vs
ballast/empty.

Priority: A+

## W53V-E05 — Port-Critical Vessel Detention

Weight by whether vessel is:
sole/specialized caller,
high-frequency service,
critical commodity carrier,
limited-substitute class.

Priority: A+

## W53V-E06 — Detainable Deficiency Severity

Classify deficiencies into:
fire safety,
lifesaving,
propulsion/steering,
structural,
pollution prevention,
ISM/safety management,
security,
navigation,
other.

Priority: S-

## W53V-E07 — Multi-Deficiency Interaction

Numerous minor deficiencies can escalate examination and contribute to detention.

Feature:
count × system breadth × severity.

Priority: A

## W53V-E08 — Deficiency Recurrence

Use PSIX closed-activity histories to identify repeated deficiency classes on same IMO vessel.

Priority: A+

## W53V-E09 — Owner/Manager Detention Breadth

Aggregate detentions by:
ISM manager,
operator,
owner
with entity-resolution confidence.

Priority: S-

## W53V-E10 — Targeted Ship Management State

USCG publishes managers associated with multiple IMO-reportable detentions within twelve months.

State:
NORMAL
TARGETED_MANAGER.

Priority: S

## W53V-E11 — Targeted Flag State

USCG targets flag administrations whose rolling detention ratios exceed stated thresholds and have multiple detentions.

State:
QUALIFIED
NORMAL
MEDIUM_RISK
HIGH_RISK.

Priority: S-

## W53V-E12 — Recognized Organization Targeting

Track classification/recognized organizations receiving USCG targeting points from detention performance.

Priority: A+

## W53V-E13 — QUALSHIP 21 State

Track vessel enrollment and expiration in QUALSHIP 21/E-Zero where public.

Use as a quality-state feature, not a guarantee against future deficiency.

Priority: A

## W53V-E14 — Detention Appeal State

State:
DETAINED
APPEAL_PENDING
APPEAL_GRANTED
APPEAL_DENIED
RELEASED.

USCG notes detention remains in force while appeal is pending.

Priority: A+

## W53V-E15 — Appeal-Reversal Signal

Historical feature:
share of manager/RO/flag detention appeals successfully reversed.

Use cautiously because appeal grounds vary.

Priority: B+

## W53V-E16 — U.S. Denial-of-Entry State

Primary source:
USCG foreign vessels denied entry into U.S. ports.

State:
ELIGIBLE
BANNED_US_PORTS
REINSTATED.

Priority: S

## W53V-E17 — Ban Network Capacity Loss

Estimate U.S.-trade capacity lost when a vessel is banned.

Priority: S-

## W53V-E18 — Ban Substitution Delay

Estimate time/cost to substitute:
same operator sister ship,
spot charter,
different vessel class,
alternate port.

Priority: A+

## W53V-E19 — Flag-State Domestic Detention

Use USCG flag-state detention list for U.S.-flag vessels separately from foreign PSC detention.

Priority: A

## W53V-E20 — Weekly PSIX Operational-Control Pulse

Primary source:
USCG PSIX bulk export.

Track weekly snapshot changes in:
vessel inspections,
operational controls,
deficiencies,
detention-related flags.

Priority: S-

## W53V-E21 — Closed-Case Availability Lag

PSIX excludes unclosed/pending privileged case information and is a weekly FOIA snapshot.

Treat it as delayed validation rather than complete live detention source.

Priority: S methodology/edge hybrid

## W53V-E22 — PSC Exam-to-Detention Hazard

Target:
P(detention | examination)
conditioned on:
flag,
manager,
RO,
vessel age/type,
prior deficiency,
port,
inspection history.

Priority: S

## W53V-E23 — Inspection Targeting Hazard

Estimate probability of expanded/priority PSC examination from:
flag risk,
manager risk,
RO risk,
prior deficiencies,
vessel history.

Priority: A+

## W53V-E24 — Class / RO Association Shock

When a detention is associated with a recognized organization:
measure whether sister vessels under same RO receive higher targeting or inspection probability.

Priority: A

## W53V-E25 — Vessel Age × Detention Risk

Condition detention hazard on:
build year,
ship type,
flag,
manager,
maintenance history.

Priority: B+

## W53V-E26 — Tanker Detention Supply Shock

Specialize to:
crude,
product,
chemical,
LPG/LNG tankers.

Map to relevant regional freight and commodity route.

Priority: S

## W53V-E27 — Dry-Bulk Detention Supply Shock

Specialize to:
Capesize,
Panamax/Kamsarmax,
Supramax/Handysize
where vessel class can be resolved.

Priority: S-

## W53V-E28 — Container Vessel Detention Supply Shock

Translate affected vessel into TEU-service capacity and alliance/service-string exposure.

Priority: A+

## W53V-E29 — Detention × Port Congestion

A detained ship can occupy berth/anchorage/terminal resources while unavailable.

Fuse with W24M queues and port operability.

Priority: A+

## W53V-E30 — Detention × Sanctions State

Fuse W47S.

A ship may simultaneously face safety detention and sanctions/ownership restrictions.

Keep causes distinct.

Priority: A

## W53V-E31 — Detention × Marine Weather Constraint

If detention release occurs during adverse port/sea conditions, actual departure can lag legal release.

Fuse W24M.

Priority: A

## W53V-E32 — Legal Release vs Actual Sailing Gap

Compare:
detention lifted
vs
AIS departure / next port call.

Priority: S

## W53V-E33 — Vessel Availability Shock Quotient

VASQ =
detained/banned economically relevant vessel capacity
/
credible substitute vessel capacity.

Priority: S

## W53V-E34 — Maritime Eligibility Truth Ladder

PSC EXAM
-> DEFICIENCY
-> DETENTION / BAN
-> REMEDIATION
-> LEGAL RELEASE
-> ACTUAL DEPARTURE
-> SERVICE/CARGO RECOVERY
-> FREIGHT/COMMODITY EFFECT.

Priority: S architecture

## Highest-priority W53V tests

1. W53V-E02 Detention-to-Release Duration
2. W53V-E03 Detention Capacity Loss
3. W53V-E06 Detainable Deficiency Severity
4. W53V-E10 Targeted Ship Management State
5. W53V-E16 U.S. Denial-of-Entry State
6. W53V-E22 PSC Exam-to-Detention Hazard
7. W53V-E26 Tanker Detention Supply Shock
8. W53V-E29 Detention × Port Congestion
9. W53V-E32 Legal Release vs Actual Sailing Gap
10. W53V-E33 Vessel Availability Shock Quotient
