# Wave 22G — Research Methods

Namespace: **W22G**

## W22G-M01 — Notice Lineage Archive
Every notice stores:
notice ID,
post time,
effective time,
end time,
status,
prior/superseded notice IDs.

Never overwrite superseded operational state.

## W22G-M02 — Gas-Day Clock Normalization
Normalize all operator timestamps to Central Clock Time and gas-day identity while preserving source timezone.

## W22G-M03 — Nomination-Cycle Alignment
Map each notice/revision to the next available Timely/Evening/Intraday scheduling cycle and effective-flow window.

## W22G-M04 — Planned-vs-Unplanned Split
Maintenance known beforehand and force majeure are different event populations.

## W22G-M05 — Directional Network Model
Capacity is indexed by segment + direction + cycle + service priority.

## W22G-M06 — Tariff-Semantics Versioning
OFO, penalty, priority and capacity-release rules are pipeline/tariff specific and can change.

Archive the effective tariff language.

## W22G-M07 — Linepack Level Normalization
Absolute linepack is pipeline-specific.

Use deviation from operator/system seasonal and recent operating ranges.

## W22G-M08 — Linepack Cause Parser
Only use operator-stated or independently validated cause categories.

No causal guess from linepack change alone.

## W22G-M09 — Scheduled-vs-Actual Boundary
Scheduled volume is an operational commitment, not confirmed physical flow.

Validate later with meter/actual-flow data where lawfully public.

## W22G-M10 — Capacity Denominator Discipline
Distinguish:
design capacity,
operational capacity,
available capacity,
firm contractual MDQ,
scheduled quantity.

Never substitute one denominator for another.

## W22G-M11 — Service-Priority Severity
Encode tariff priority ladder so interruptible cuts do not receive the same severity as primary-firm cuts.

## W22G-M12 — Maintenance Revision Ledger
Each maintenance schedule revision is its own availability-time event.

## W22G-M13 — Force-Majeure Recovery Survival Model
Model restoration-time distribution with right censoring and revision history.

## W22G-M14 — Capacity-Release Auction Reconstruction
Archive offers, bids/awards where public, term, path, rate, quantity, posting/award time and affiliate indicators where available.

## W22G-M15 — Release-Rate Comparable Set
Compare capacity-release pricing only across similar path, season, term and service quality.

## W22G-M16 — Public-Rights Gate
Some operator portals may require registration or have use restrictions.

Track PUBLIC_ANONYMOUS / PUBLIC_REGISTRATION / LICENSED / RESTRICTED separately.

## W22G-M17 — Gas-Electric Common-Weather Control
Weather jointly drives gas constraints and power prices.

Control for weather/load before claiming pipeline-to-power causality.

## W22G-M18 — Local-Basis First
Validate constraints against the nearest economically connected basis point before Henry Hub or equities.

## W22G-M19 — Alternate-Path Capacity
Estimate reroute feasibility from network topology and available capacity, not geographic proximity alone.

## W22G-M20 — Physical Promotion Gate
Promote only after showing incremental OOS prediction of:
scheduled/actual flow,
curtailment,
basis,
storage behavior,
LNG feedgas,
or power fuel availability.
