# Wave 76Q — Research Methods

Namespace: **W76Q**

## W76Q-M01 — Clock Contract and Time Zones
Store every timestamp as UTC plus source-local zone. Compute London/New York/Chicago offsets from IANA tzdata per date; never hard-code 14:28 ET = 19:28 London.

## W76Q-M02 — Exchange Window Versioning
Version CME/ICE settlement windows and TAS hours with capture date and URL hash; CME confluence pages change (Gold page revision 10 observed). Do not apply today's window to old history.

## W76Q-M03 — EIA Release Availability
Use schedule-page timestamp as expected release; use first_seen_time of data as actual. Hash the schedule daily (E03).

## W76Q-M04 — Vintage Storage for EIA Series
Store each weekly vintage and later revisions; weekly figures that blend monthly data must not be back-filled with revised values.

## W76Q-M05 — Expectation Construction Without Consensus
Analyst consensus is not primary/open; build expectation from seasonal AR plus 5-year averages using only data known before release. Mark consensus-based variants PROVENANCE_PENDING.

## W76Q-M06 — Placebo Clock Windows
Every window effect (release, settlement, fix) needs same-wall-clock placebo windows on non-event days and adjacent hours.

## W76Q-M07 — Matched Delivery Month Rule
Spread logic uses delivery-month matched legs; front-front is a diagnostic only (E26, E27).

## W76Q-M08 — Contract Roll Calendar
Compute CL expiry via 3-business-day-before-25th rule with NYMEX holiday table; GC/SI/NG per spec; unit tests on all expiry dates in sample.

## W76Q-M09 — Settlement Price vs Traded Price
Never mix settle prints (VWAP window, tiered back months) with last trade in the same feature without a tier flag.

## W76Q-M10 — TAS and Block Handling
Tag TAS and block trades; exclude from window-VWAP reconstruction unless the CME rule includes them; UNVERIFIED rule details stay PP.

## W76Q-M11 — DST Mismatch Calendar Test
Unit-test the number of mismatch weeks per year; include UK/US change dates.

## W76Q-M12 — Event Overlap Masks
For each minute store a set of overlapping events (EIA, FOMC, CPI, auctions); single-event inference only on isolated events.

## W76Q-M13 — Leakage in Fix Data
LBMA data is licensed and published after the auction; use only the lawful post-publication timestamp for features.

## W76Q-M14 — Licensing Gate
IBA benchmark data requires licence for real-time/historical use (verified on LBMA page); production features from it are blocked until licence is confirmed.

## W76Q-M15 — Minimum Sample Rules
Holiday-shifted release slots and expiry-collision cases are small-n; report as underpowered, never promote below n=30 events.

## W76Q-M16 — Sign Ambiguity Declaration
Every feature declares whether sign is predicted ex ante; surprise-signed edges are tested two-sided.

## W76Q-M17 — Cost Model
Window and release edges are evaluated with tick-normalised slippage (CL tick 0.01=$10, GC 0.10=$10, SI 0.005=$25, NG 0.001=$10, verified).

## W76Q-M18 — Multiple Testing
Edge family FDR control across all W76Q tests; priority list is a reading order, not a result.

## W76Q-M19 — Regime Splits
Report by backwardation/contango, vol tercile, DST aligned/misaligned, and pre/post structural change (e.g., USO roll change).

## W76Q-M20 — Negative Controls
Wrong-day (Thursday vs Wednesday), wrong-instrument (HG, ZC), shuffled surprise labels.

## W76Q-M21 — Source Kill Rule
A PP source that cannot be verified in 30 days is downgraded; dependent edges capped at B.

## W76Q-M22 — Immutable Event Log
Append-only event log with first_seen_time; no retroactive edits.

## W76Q-M23 — Promotion Gate
Intermediate-outcome promotion gate: calibration, placebo, cost-net uplift, stability across regimes, then shadow trading before any weight.

## W76Q-M24 — Execution Gate Verification
E10 and E23 gates are validated by slippage reduction only, not by signal PnL.

## W76Q-M25 — Provenance Language
Statements are VERIFIED (primary page read), SEARCH_VERIFIED (snippet only), or PP.
