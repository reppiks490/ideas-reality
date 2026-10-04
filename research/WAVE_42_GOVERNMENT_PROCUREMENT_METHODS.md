# Wave 42G — Research Methods

Namespace: **W42G**

## W42G-M01 — Procurement Identity Graph
Join solicitation number, award ID, PIID, task/delivery order, agency and public issuer identity with provenance.

## W42G-M02 — Announcement-vs-Award Clock
Public company press release, agency award, SAM notice and USAspending obligation can occur at different times.

Preserve each clock.

## W42G-M03 — Protest Filing-vs-Posting Clock
Store GAO filed date and public docket/posting availability separately where distinguishable.

## W42G-M04 — Stay Eligibility Is Not Stay Observation
Compute legal eligibility separately from confirmed agency suspension/termination/override.

## W42G-M05 — Debriefing Dependency
Automatic-stay timing can depend on required debriefing rules.

Do not infer debriefing dates unless publicly supported.

## W42G-M06 — FAR / DFARS Rule Versioning
Defense procurements can have supplemental protest-stay timing rules.

Version FAR/DFARS and procurement type historically.

## W42G-M07 — Ceiling vs Funded Value
IDIQ/BPA/option ceilings are not guaranteed revenue.

Separate:
ceiling,
minimum,
obligated,
funded,
exercised options.

## W42G-M08 — GAO Case-Family Deduplication
Group .1/.2/.3 supplemental/amended protests while preserving independent protesters/grounds.

## W42G-M09 — Corrective-Action Classification
Corrective action is relief but does not reveal final award winner.

## W42G-M10 — Public Grounds Limitation
Protective-order material is not public.

Do not invent protest merits from redacted dockets.

## W42G-M11 — Resolution Vintage
Use first-public decision/corrective-action/dismissal time, not later redacted opinion release, unless that is the first public evidence.

## W42G-M12 — USAspending Reporting Lag
Treat federal spending records as downstream administrative data; preserve action date and first-observed API date.

## W42G-M13 — Modification Netting
Separate new obligation, deobligation, option exercise, ceiling change and administrative modification.

## W42G-M14 — Revenue Recognition Boundary
Federal obligation/performance does not equal GAAP revenue.

Use company-specific contract accounting only if later tested.

## W42G-M15 — Incumbent Counterfactual
For bridge-contract hypothesis, verify incumbent identity and actual extension.

## W42G-M16 — Court vs GAO State
GAO automatic stay and COFC injunction are different legal mechanisms.

Never merge them into one binary "protest halt."

## W42G-M17 — Selection Bias Control
Most federal procurements are not protested.

Use full award universe, not only famous disputes.

## W42G-M18 — Financial Promotion Gate
Before equity testing, require OOS improvement in:
performance delay,
obligation timing,
award transfer,
backlog realization,
or bridge-contract extension.
