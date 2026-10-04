# Wave 33S — Short Constraint & Settlement Stress

Namespace: **W33S**

Thesis: short-sale pressure is not one variable. It is a state produced by outstanding short positions, new short-sale flow, borrow scarcity, settlement failures, Regulation SHO restrictions, options substitution and available lendable supply. The useful signal is the interaction between these layers, with each source kept inside its actual scope and publication latency.

2026 source gate: FINRA SLATE securities-lending transparency is not live. FINRA's current implementation page says SLATE has been extended to September 28, 2028. No 2026 edge may depend on SLATE data.

All candidates are research hypotheses only. Claude owns later implementation.

## W33S-E01 — FTD Balance Residual
Primary source: SEC Fails-to-Deliver.
Feature:
reported CNS fail balance - security-specific expected fail balance.
Priority: S-

## W33S-E02 — FTD Persistence
Count consecutive settlement dates with elevated fail balances after correcting for file/publication lag.
Priority: S

## W33S-E03 — FTD / Free-Float Quotient
FTDQ = outstanding fail shares / point-in-time free float.
Priority: S-

## W33S-E04 — FTD / Trading-Volume Quotient
Fail shares / recent ADTV.
Interpretation: settlement imbalance relative to normal turnover.
Priority: A+

## W33S-E05 — Reg SHO Threshold Entry
Detect first day a security appears on its listing SRO's threshold list.
Threshold requires five consecutive settlement days above the rule-defined fail thresholds.
Priority: S

## W33S-E06 — Threshold Age
Number of consecutive public threshold-list days.
Priority: S-

## W33S-E07 — Threshold Exit
Detect removal only after source confirms the security no longer meets threshold-list criteria.
Priority: A+

## W33S-E08 — Threshold Close-Out Pressure Envelope
Rule 203 imposes additional close-out requirements for participant fails that persist 13 consecutive settlement days.
Public threshold status does not reveal participant-level fail age.
Output a probability/range, never an exact forced-buy quantity.
Priority: S

## W33S-E09 — Rule 204 Pre-Borrow Constraint Risk
Rule 204 can impose pre-borrow requirements after unclosed settlement fails.
Public data cannot identify participant-specific obligation in real time.
Use as latent constraint state only.
Priority: A

## W33S-E10 — FINRA Short Interest Level
Primary source: FINRA twice-monthly aggregate short interest.
Normalize by shares outstanding/free float.
Priority: S

## W33S-E11 — Short Interest Acceleration
Change in reported short interest between designated settlement dates, adjusted for corporate actions.
Priority: S

## W33S-E12 — Days to Cover
Reported short interest / contemporaneous ADTV.
Priority: S-

## W33S-E13 — Short Interest / Free Float
SIFF = short interest / tradable free float.
Priority: S

## W33S-E14 — Short Interest × Passive Ownership
Passive owners can expand lendable supply while also attracting informed shorting.
Condition short-interest signals on passive ownership rather than assume one direction.
Priority: A+

## W33S-E15 — Off-Exchange Short-Sale Volume Ratio
Primary source: FINRA Daily Short Sale Volume.
ShortVolume / TotalVolume within the relevant TRF/ADF/ORF scope.
Priority: A+

## W33S-E16 — Short-Exempt Volume Surge
Track ShortExemptVolume relative to its own facility/security baseline.
Do not treat short-exempt volume as ordinary short selling.
Priority: A

## W33S-E17 — Off-Exchange Short-Flow Acceleration
Change in FINRA-reported short-sale share and notional activity across days.
Priority: A+

## W33S-E18 — Rule 201 × Short-Flow Suppression
Fuse W27V Rule 201 state with FINRA short-volume changes.
Research whether short flow shifts from aggressive to passive/exempt/derivative channels.
Priority: S-

## W33S-E19 — Option-Implied Borrow
Use put-call parity / synthetic-forward relationships, with dividends/rates/early-exercise handled correctly, to infer a borrow/rebate stress proxy.
Priority: S

## W33S-E20 — Parity Dispersion
Measure implied-borrow disagreement across strikes/expiries.
High dispersion can indicate bad quotes, early-exercise effects or segmented constraint.
Priority: A

## W33S-E21 — Implied Borrow Term Structure
Compare near-term vs longer-dated option-implied borrow scarcity.
Priority: A+

## W33S-E22 — Threshold × Implied-Borrow Collision
Threshold status plus worsening option-implied borrow may identify settlement stress where shorting constraints are actually binding.
Priority: S

## W33S-E23 — Threshold × High Short Interest
Combine persistent settlement failures with crowded aggregate short positioning.
Priority: S-

## W33S-E24 — Short-Squeeze Fragility Index
Inputs:
SI/free float,
days to cover,
implied borrow stress,
threshold age,
Rule 201 state,
options gamma,
issuer buyback/issuance state.
Output is squeeze fragility, not direction.
Priority: S

## W33S-E25 — Lendable-Supply Shock Proxy
Use point-in-time passive/index ownership changes, insider lockups, primary issuance and large holder exits as proxies for changes in potential lendable supply.
Priority: A

## W33S-E26 — Index Rebalance × Borrow Supply
Fuse W26R index changes with passive-ownership/lending-supply effects.
Question:
does benchmark migration change short capacity after index implementation?
Priority: A+

## W33S-E27 — Issuer Buyback × Short Constraint
Fuse W32I confirmed/estimated issuer demand with high SI/borrow/threshold stress.
Potential effect:
reduced float + incremental demand during constrained short supply.
Priority: S

## W33S-E28 — Primary Issuance Borrow Relief
New primary shares or ATM issuance can increase float/lendable supply and alter crowded-short constraints.
Priority: A+

## W33S-E29 — Corporate-Action Settlement Stress
Splits, mergers, distributions, symbol/CUSIP changes and conversions can create mechanical fail spikes.
Classify before interpreting FTD as informed short pressure.
Priority: S methodology/edge hybrid

## W33S-E30 — FTD Recovery Half-Life
After threshold exit or major fail spike:
measure decay of fail balance, implied borrow stress, short volume and liquidity dislocation.
Priority: A+

## W33S-E31 — SLATE Future Activation Gate
FINRA Rule 6500/6540 architecture can eventually provide loan-rate distributions, aggregate loan activity and delayed quantities.
Status in 2026:
DISABLED_FOR_RESEARCH_SIGNAL.
Re-evaluate only after verified public production launch.
Priority: Future infrastructure

## W33S-E32 — Short-Constraint Truth Ladder
SHORT FLOW
-> SHORT POSITION
-> BORROW SCARCITY
-> SETTLEMENT FAILURE
-> REGULATORY CONSTRAINT
-> COVERING/NEW SUPPLY
-> PRICE EFFECT.

Priority: S architecture

## Highest-priority W33S tests
1. W33S-E02 FTD Persistence
2. W33S-E05 Threshold Entry
3. W33S-E08 Threshold Close-Out Pressure Envelope
4. W33S-E11 Short Interest Acceleration
5. W33S-E13 Short Interest / Free Float
6. W33S-E19 Option-Implied Borrow
7. W33S-E22 Threshold × Implied-Borrow Collision
8. W33S-E24 Short-Squeeze Fragility Index
9. W33S-E27 Issuer Buyback × Short Constraint
10. W33S-E32 Short-Constraint Truth Ladder
