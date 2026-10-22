# Wall Street Motor — forensic architecture-donor dossier

**Record:** WSM-D01  
**Status:** RESEARCH ONLY — architecture donor; no trading edge certified  
**Reviewed:** 2026-10-22  
**Source:** https://github.com/recinosr/wall-street-motor  
**License:** MIT; preserve the upstream copyright and license notice if any source code is later reused.

## Executive decision

Wall Street Motor is valuable to ICARUS primarily as a compact **research-integrity and prospective-evidence control plane**, not as a proven alpha engine. Its strongest ideas constrain how experiments are opened, how forecasts are committed, how later prices may qualify as fills, how failed attempts count, and how models earn or lose authority.

The recommended transfer is selective and implementation-neutral:

1. Single-use sealed-trial protocol bound to a frozen experiment identity.
2. Future-poison / prefix-invariance tests for temporal causality.
3. Lifetime research-debt accounting for every attempted, failed, abandoned, and previously tested hypothesis family.
4. One-shot LLM forecast reservation before model invocation.
5. Causal intent → successful-run receipt → later observation → fill custody.
6. Hash-chained event ledger with genesis-to-tip audit.
7. Mature-label expert weighting with a nonzero exploration floor.
8. Family-balanced ensemble voting so cloned agents cannot manufacture extra authority.
9. Whole-universe fail-closed behavior when a required source or asset is absent.
10. Frozen cohort rankings scored only at predeclared future horizons.
11. Runtime admission and deterministic scheduler recovery.
12. Behavior-matched null models and frozen external-strategy adversaries.
13. Capability graduation, quarantine, and delayed promotion.
14. Frozen-anchor versus rolling-update evaluation.
15. Adversarial capital-risk simulations.
16. Deterministic context separation: explanation, prediction, learning, and execution remain distinct.
17. Point-in-time source-availability manifests, adopted only after source semantics are independently verified.

Do **not** import the entire codebase, result archive, or trading rules wholesale. Build Icarus-native contracts and tests around the reusable principles, then compare against Icarus's existing DAEDALUS, AION, evidence, research, scheduler, and execution controls before implementing anything.

## Provenance and repository archaeology

### Origin and chronology

- The earliest surviving main commit is [a33659d506787ff5f3b73da319d51b46d756997f](https://github.com/recinosr/wall-street-motor/commit/a33659d506787ff5f3b73da319d51b46d756997f), authored 2026-10-08 21:27 UTC, with no parent. It arrived as a working automated research system rather than an empty repository.
- The separate data branch began later and stores a BTC/ETH one-minute archive. It does not predate the main-code root.
- The surviving codex/tarea22-diario-meses branch is an old ancestor of main: comparison reported zero commits ahead and roughly 10,400 behind. It is not an undiscovered newer implementation.
- The main branch has no branch-protection flag enabled in the inspected branch listing. Some commits are unsigned. Hashes and GitHub receipts are therefore **tamper-evident evidence, not an external immutable timestamp or an absolute defense against privileged history rewriting**.

### Current tree shape observed

The inspected main tree contained 28,206 blob files: 52 files under lab, 29 test modules, 22 GitHub Actions workflow files, and 28,016 files under resultados. The result files alone total approximately 498.8 MB uncompressed. The large displayed commit count is heavily inflated by automated state/result publications; it must not be interpreted as thousands of independent engineering changes.

The public repository is MIT-licensed. It has no broker connection and its demo accounts are fictitious. No source code or historical output from this repository has been copied into ICARUS by this research pass.

### Architectural timeline

| Period | Evolution | Transfer significance |
|---|---|---|
| Oct 8, 2026 — root | Causal BTC/ETH research factory, incremental learner, daily archiver, gym and school workflows already present. | Search control and automated research existed from day one. |
| Oct 8–9 | Forecast marker/scoreboard, write-once forecasts, durable receipts, deterministic diary, and paper crypto simulation. | Forecast-before-outcome and causal execution custody are ancestral primitives, not late cleanup. |
| Oct 9–10 | VITA attempt reservation and Bóveda code/config freeze; the sealed reserve is consumed only through an explicit receipt. | A research attempt becomes a state transition that cannot be silently retried. |
| Oct 10–11 | Bóveda examination rounds, fixed training/validation/reserve windows, global search-family accounting, and post-measurement sensitivity audit. | Promotion and audit are separated; audit may add evidence but may not select a new winner. |
| Oct 10 onward | Vigilante heartbeat, missed-cycle accounting, serialized workflow slots, retries and self-relay. | GitHub Actions is used as a control plane, not merely a cron runner. |
| Oct 16 | Hedge weighting correction and Oráculo point-in-time/capability work. | Expert arbitration was corrected after a concrete weighting mistake; PIT capability remains partial. |
| Oct 18–22 | Oráculo levels 6–7, frozen monthly cohorts, continuing prospective logs and explicit negative-result summaries. | The repo publishes failed promotions rather than claiming a successful capability because the code exists. |

## Donor methods and Icarus-native destination

Evidence grades:
- **A — source + tests:** implementation and specific regression tests inspected.
- **B — source/results with caveats:** mechanism exists, but performance or production-grade guarantees are not established.
- **C — documentation/incomplete implementation:** useful design clue; obtain missing source or evidence before adoption.

### WSM-M01 — Single-use sealed-trial protocol
**Priority: P0 · Evidence: A/B**

Bóveda fixes train, validation, reserve, horizon, method rounds, stop rule and multiplicity accounting. It writes a receipt before reserve download/sampling; repeat attempts are refused. A failed attempt is not erased just because it produced no score. The winning record explicitly says the reserve has already been consumed and cannot be reopened.

**Icarus destination:** DAEDALUS Research OS, Icarus-engine ResearchWorkspace, AION evidence contracts, and the shared research-campaign registry.

**Strengthen before reuse:** bind the entire Git tree/commit, test suite, workflow definitions, dependency lock, data manifest/vintages, split/cutoff, cost model, seeds and protocol to a canonical manifest. The Bóveda signature inspected hashes six code modules plus config; it is not, by itself, a complete signature over tests, workflows, dependencies and source-data vintages.

### WSM-M02 — Future-poison / prefix-invariance tests
**Priority: P0 · Evidence: A**

Bóveda tests mutate all data strictly after decision time T (including a 10× transformation and NaN) and require the serialized prediction at T to remain identical. It also asserts that fitted labels end before the allowed cutoff. This is stronger than checking that a feature happens to use a shift.

**Icarus destination:** DAEDALUS temporal-causality suite, Icarus-engine feature tests, AION frozen-frame reconstruction, and CSV Evidence Lab.

**Extension:** poison future bars, revised macro vintages, future event fields, universe membership, external-provider rows, labels and cached summaries. Compare canonical prediction/evidence hashes, not only floating-point values. Existing Icarus-engine work already discusses future-garbage invariance for market-structure features; the donor opportunity is to generalize that invariant to every predictive artifact and source boundary.

### WSM-M03 — Lifetime research debt
**Priority: P0 · Evidence: A**

The exam reports 70 variants attempted, 88 designed, 1,014 calculated contrasts, and a conservative family of 4,584 that includes prior contrasts and variants not opened. A later sensitivity audit adds its own five contrasts and expands the family to 4,589. The ICT extension preserves the previous family instead of resetting the research counter.

**Icarus destination:** DAEDALUS corpus-level FDR, causal-router search registry, GA generation ledger and the canonical hypothesis registry.

**Contract:** every candidate must carry campaign ID, parent hypothesis, method family, variants designed/attempted/evaluated, failed or skipped status, prior-family reference, and adjustment scope. No new run gets to declare itself statistically fresh merely because it has a new filename, branch, agent or month.

### WSM-M04 — One-shot LLM forecast reservation
**Priority: P0 · Evidence: A for the protocol; no LLM alpha evidence**

VITA's monthly pilot reserves one request for a specific date, GitHub run and run attempt. The reservation must be committed and visible in origin/main before the network call. A 429, timeout, non-200 response, invalid JSON, or late answer consumes the attempt; a rerun under another attempt ID is rejected. Prompt/config are hashed and the output is scored only after its future label matures.

**Icarus destination:** AION forecast commitment, VITA/agent invocation ledger, DAEDALUS prospective studies, and any agent that produces a scored prediction.

**Important limitation:** the public report says the Gemini monthly pilot was prepared but not activated for a validated performance trial. This proves the commitment design exists; it does not prove the LLM predicts markets. The inspected signature covers prompt/config, not the full executable tree, provider model revision, environment and all data context. Icarus should bind those too.

### WSM-M05 — Causal execution custody
**Priority: P0 · Evidence: A**

The paper crypto simulator separates intent and fill across distinct successful workflow runs. A fill requires a prior successful Actions receipt and a fresh quote timestamped after the decision and receipt. Missed openings are not replayed at old prices. Stops and targets are evaluated against observed future quotes, not reconstructed after the fact. Coinbase and Kraken must agree within a fixed tolerance.

**Icarus destination:** Icarus-engine paper execution, AION's prediction/outcome timeline, execution sentinel and the audit trail that joins intent, fill, position, exit and P&L.

**Acceptance invariant:** no decision may fill in the same run that created it; quote time must exceed both decision time and receipt completion; stale, absent or discordant sources must abstain.

### WSM-M06 — Hash-chained event ledger
**Priority: P0 · Evidence: A**

VITA Opera chains each event to the prior event hash. Before new activity, it replays the JSONL ledger from genesis and verifies sequence, predecessor hash, event hash, total count and terminal summary state. Tampering or inconsistency stops execution.

**Icarus destination:** AION EventStore and paper-trading evidence ledger.

**Security caveat:** a hash chain detects mutation relative to the retained chain; it does not stop a privileged owner from rewriting an unprotected Git history and regenerating the chain. Add signed attestations, protected branches, required checks, and an independent append-only/WORM or transparency receipt if the goal is stronger non-repudiation.

### WSM-M07 — Mature-label Hedge weighting with exploration floor
**Priority: P1 · Evidence: A/B**

The forecast ensemble weights experts by average matured Brier loss, partitioned by asset and horizon. The correction moved away from cumulative-loss weighting, which unfairly punished experts with more matured labels. A nonzero weight floor prevents an expert from disappearing forever. Neutral probability 0.5 is treated as abstention, not a bet.

**Icarus destination:** Pi/agent arbitration and Apex Council, partitioned by asset × horizon × decision type.

**Guardrails:** weight only on labels that have matured before the decision; separate prediction quality from trade utility; track sample count and calibration; do not let an agent win authority by producing more predictions; preserve an exploration floor only in research/shadow mode unless a separate policy approves it.

### WSM-M08 — Family-balanced ensemble voting
**Priority: P1 · Evidence: A/B**

The exam ensemble gives equal weight to methodology families before averaging members inside each family. This limits clone-count dominance: adding ten near-identical momentum agents should not outweigh one genuinely independent macro or volatility family.

**Icarus destination:** Apex Council, specialist quorum, evidence-dependence graph and ensemble design.

**Acceptance test:** duplicating a member within an existing family must not change the family-level vote; adding a new family requires explicit provenance and evidence, not merely another agent name.

### WSM-M09 — Fail closed on incomplete universe/source coverage
**Priority: P0 · Evidence: A**

The exam refuses to select only the assets whose downloads succeeded. Missing external predictors abstain; incomplete target paths are unqualified rather than silently filled. Missing minutes are preserved as gaps. This prevents data availability from selecting a convenient subset.

**Icarus destination:** CSV Evidence Lab, source-ingestion contracts, cross-asset panel construction and candidate qualification.

**Acceptance invariant:** if a required member, time path, timestamp, schema, vintage or source receipt is missing, either fail the whole declared experiment or apply a predeclared abstention rule. Never shrink the universe after seeing coverage or results.

### WSM-M10 — Frozen cohort and delayed ranking score
**Priority: P1 · Evidence: B**

The scanner freezes the date's eligible cohort/ranking with a hash, then grades the same cohort at predeclared 5- and 21-session horizons against a benchmark. It reports current-index survivorship bias rather than pretending a current list is a historical universe.

**Icarus destination:** cross-asset ranking, regime ranking, source ranking and daily opportunity-selection agents.

**Extension:** retain delisted/expired assets and point-in-time universe membership; never score only the survivors. A cohort score is an evaluation object, not an immediate trade authorization.

### WSM-M11 — Runtime admission gate and deterministic scheduler recovery
**Priority: P1 · Evidence: A/B**

A weekly task was admitted to the shared supervisor only after a cloud run demonstrated a 34-second completion. Vigilante tracks expected slots, missed cycles and heartbeat state, retries the same publication after a race, and can self-relay while cron remains a backup.

**Icarus destination:** Omega scheduler and workflow assurance.

**Do not replace Icarus's existing watchdog/backlog plane.** Extract measured admission SLOs, expected-cycle coverage and same-state retry semantics only where absent. Retry the same idempotency key and payload; never regenerate a new truth to hide a failed publication.

### WSM-M12 — Behavior-matched nulls and frozen adversary zoo
**Priority: P1 · Evidence: A/B**

External strategy candidates are pinned to an upstream Git revision and evaluated under identical data/cost assumptions. Comparators preserve operation count and holding-duration distribution where applicable. Gaps and ambiguous same-candle exits are handled conservatively; failed experiments remain in the multiplicity family. Some portfolio comparisons are descriptive and not proof of tradable alpha.

**Icarus destination:** APEX qualification and DAEDALUS adversarial testing.

**Extension:** nulls should preserve trade count, duration, side mix, time-of-day, turnover, volatility targeting and regime exposure. Strategy clones are frozen by source commit; do not tune the adversary after observing results.

### WSM-M13 — Capability graduation and quarantine
**Priority: P1 · Evidence: B**

Oráculo has preregistered capability levels. A level is not considered real merely because code exists. A candidate that passes a retrospective test still cannot immediately change the live plan; a later version imposed a 90-day wait/prospective period. A contaminated or reopened holdout demotes the result to exploratory.

**Icarus destination:** DAEDALUS candidate lifecycle, AION capability status, and execution authorization gates.

**Suggested states:** IDEA → SOURCE_VERIFIED → MECHANISM_VERIFIED → OOS_SIGNAL → ROBUST_SIGNAL → TERMINAL_HOLDOUT_PASS → LIVE_SHADOW → PAPER_ELIGIBLE → IMPLEMENTATION_CANDIDATE → RETIRED. Keep implementation state distinct from evidence state.

### WSM-M14 — Frozen-anchor versus rolling-update evaluation
**Priority: P1 · Evidence: A/B**

The monthly experiment compares a mode whose features are frozen at the start of the month against a mode that updates using the previous day's close. The prediction range remains frozen at the initial anchor. This isolates the value of refresh frequency from the value of the original signal.

**Icarus destination:** multi-agent refresh cadence, macro/event context updates, daily vs intraday signal persistence and execution timing.

**Test:** compare both policies on the same cohort, targets, costs and start dates; never let the rolling policy see the current target interval.

### WSM-M15 — Adversarial capital-risk simulation
**Priority: P2 · Evidence: B**

The portfolio simulator explicitly admits short historical coverage, adds conservative drift scenarios and fees/spread/TER assumptions, and reports path drawdown and recovery rather than only expected return. It does not make the underlying proxies equivalent to the target strategy.

**Icarus destination:** independent capital-risk lab, not the alpha engine.

**Extension:** block-bootstrap cross-asset returns to preserve dependence, then stress drift, volatility, correlation, fees, slippage, capacity, gaps and source outages. Report distributions of ruin, drawdown depth/duration and recovery time.

### WSM-M16 — Separate explanation, prediction, learning and execution
**Priority: P1 · Evidence: B/C**

The documented VITA architecture uses a deterministic journal as its source of figures; the chat can explain published state but must not invent today's measurements or mutate strategy weights/accounts. Market alerts are explicitly analytical, not orders. Missing model/API evidence defaults to neutral. Some chat-provider/quota implementation is described in docs but is not fully present in the public source tree, so do not treat the undocumented pieces as verified implementation.

**Icarus destination:** all LLM agents, especially AION, Pi, Apex Council and user-facing command interfaces.

**Contract:** explanation cannot create evidence; model output cannot mutate a research ledger; research approval cannot place orders; an execution permission must be independently granted by the execution policy.

### WSM-M17 — Point-in-time availability manifests (adopt the contract, not the claims)
**Priority: P1 · Evidence: B with explicit caveats**

Oráculo PIT carries source/payload hashes and availability timestamps and filters observations by available_at. But the project report itself says the PIT layer is partial: Yahoo's current price history lacks true historical vintages, EDGAR's recent endpoint does not cover the entire past, GDELT's seen date is not always original publication time, and FOMC/CPI revision/publication archives were not verified.

**Icarus destination:** CSV Evidence Lab, ingestion manifest and AION source-time ledger.

**Rule:** copy the schema discipline, not the assumption that the dataset is PIT-correct. Require event_time, published/available_time, ingested_time, source timezone, vintage/revision, raw-payload hash, schema version and availability confidence; mark source limitations explicitly.

## What the actual results say

The repo's discipline is valuable, but its reported results do not establish an edge.

| Published artifact | Observed result | Interpretation |
|---|---|---|
| Bóveda examination, seed 20261011 | 1,000 unique asset/date pairs; 3,515 qualified questions; 485 unqualified; 70 variants attempted, 88 designed, 1,014 contrasts calculated; conservative search family 4,584. | Strong audit trail and search accounting; small/overlapping samples remain a limitation. |
| Bóveda champion | base_5a retained; validation Brier skill about -0.09%, descriptive 95% interval -1.64% to +1.50%; all reported q-BH values 1.0. | No demonstrated improvement over baseline. It is not authorized for deployment; the reserve is marked consumed and cannot be reopened. |
| Bóveda sensitivity audit | Five EEM 60-day cells looked significant under the original bootstrap, but all failed the added sign-flip/block sensitivity family (adjusted p = 1.0). | Excellent example of a seductive apparent result failing a robustness check; the sensitivity audit correctly did not pick a new winner. |
| Oráculo level 6 | Three intermarket hypotheses failed. Test-period hit rates were approximately 54.3%, 47.1%, and 57.1%, versus a reported 66.4% baseline; adjusted q values were about 0.98. | Do not promote intuitive macro stories without evidence. |
| Oráculo level 7 | Tested allocation rules underperformed the fixed baseline in the reported test period; p/q were 1.0 and no rule was approved. | Capability ladder works by refusing promotion. |
| Daily diary as of 2026-10-21 | 85 patterns, zero passing all criteria after costs; three robots across 24 cases, zero beating both buy-and-hold and random after multiplicity correction. Paper BTC demo was below its hold comparator at the reported cutoff. | No verified alpha claim. |
| Monthly Bóveda report | 13.7 million overlapping daily probabilities, but explicitly not independent tests; no calendar effect survived BH and no method showed adjusted Brier improvement against the coin baseline. | Volume of predictions is not independent evidence. |
| PIT report | Several sources lack historical publication vintages or complete source archives; some curriculum levels were not evaluated or had contaminated/reopened reserve periods. | PIT must be certified per source; do not describe this corpus as fully PIT. |

The 2024–2026 reserve had already been exposed by an earlier task, so later analyses are exploratory and cannot be sold as a fresh independent final test. The exam uses retrospective Yahoo price history without verified historical vintages, adjusted closes/dividends or a full execution-cost model. It is a methodological case study, not a clean causal market-performance certification.

## Trust and implementation gaps to preserve in the record

1. **Hashing is not signing.** A SHA-256 digest proves equality to a supplied digest; it does not establish who authorized the digest.
2. **The Git history is not an independent timestamp authority.** Main was listed as unprotected. Add protected branches, required CI, signed release tags/attestations, and a separately retained append-only receipt if tamper resistance matters.
3. **The Bóveda signature scope is narrower than a full experiment identity.** It hashes config and selected source modules; it does not by itself bind tests, workflows, dependency lock, data vintages or external source snapshots.
4. **VITA's prompt/config signature is not a complete model-run signature.** Add code commit, provider/model revision, schema, environment, data-context hash, run attempt and response hash.
5. **The PIT implementation is explicitly partial.** Current Yahoo historical prices are not true historical vintages; some macro/event timestamps are not verified availability timestamps.
6. **The strategy evidence is negative or exploratory.** No candidate from this dossier may be labeled a proven trading edge.
7. **The result archive is huge and highly automated.** Do not import the 28,000+ result files into Icarus. Store the donor manifest, selected result summaries, provenance hashes and source links; fetch raw artifacts only when a specific study needs them.
8. **The pilot LLM forecast was documented as prepared but not performance-validated.** The reservation protocol may be reused as a design pattern; the LLM itself receives no predictive authority from this dossier.

## Icarus integration architecture

Use an Icarus-native evidence contract rather than transplanting the motor's package:

**Candidate → preregistered StudyManifest → code/environment/data/split/cost hashes → one-use reservation receipt → prediction artifact → matured labels → independent robustness audit → lifetime research-debt/FDR update → prospective shadow cohort → promotion or rejection.**

For any paper execution path:

**Decision → Intent → successful prior-run receipt → fresh post-receipt quote → independent price corroboration → simulated/approved fill → hash-chained event → independent ledger audit.**

Authority boundaries:
- DAEDALUS owns experiment design, causal tests, adversarial validation and retirement evidence.
- AION owns decision-time state, immutable forecast/context snapshots and later outcome attachment.
- Icarus-engine owns the local research service, provider contracts, scheduler/runtime supervision and paper mechanics.
- Apex Council / Pi may arbitrate among evidence-qualified families, but must account for common provenance and correlation.
- CSV Evidence Lab validates data structure, byte hashes, timestamps and source contracts; it does not certify alpha.
- Icarus canonical runtime receives only revision-pinned, evidence-qualified handoffs. This donor package grants **no** paper or live execution authority.
- Owner Actions tracks review and approval; it does not convert a research note into authorization.

## Acceptance test matrix before any implementation is promoted

1. Poison every value strictly after T across all source tables; canonical prediction/evidence hash at T remains unchanged.
2. Attempt to open the same reserve twice; second attempt fails before download, scoring or network I/O.
3. Simulate timeout, 429, invalid schema, partial response and late response; the one-shot attempt is consumed and no reroll occurs.
4. Change code, tests, workflow, dependency lock, source manifest or split; the frozen experiment signature must fail.
5. Mutate, reorder, truncate or fork a ledger event; audit must stop before processing new events.
6. Try a same-run fill, stale quote, quote earlier than receipt, missing second provider, or out-of-tolerance price; execution is rejected.
7. Delete a required asset/source/date; the declared experiment fails closed or follows a predeclared abstention policy without shrinking to survivors.
8. Duplicate an expert within a family; family-level vote/weight remains invariant.
9. Add failed and abandoned variants; the lifetime research-family count cannot decrease.
10. Run behavior-matched nulls and frozen external challengers under identical costs/data; candidate must beat predeclared controls after global correction.
11. Compare frozen-anchor and rolling-update policies on identical targets and cohorts.
12. Stress cost, latency, drift and correlation; worsening assumptions must not improve net performance without a logged, explained simulator mechanism.
13. Require prospective shadow evidence and a quarantine period before any change in production authority.
14. Verify branch protection, signed attestation and external append-only receipt for any claim described as immutable.

## Source map

- Main/root history: https://github.com/recinosr/wall-street-motor/commit/a33659d506787ff5f3b73da319d51b46d756997f
- Bóveda exam implementation: https://github.com/recinosr/wall-street-motor/blob/main/lab/boveda_examen.py
- Bóveda exam model layer: https://github.com/recinosr/wall-street-motor/blob/main/lab/boveda_examen_modelos.py
- Bóveda test suite: https://github.com/recinosr/wall-street-motor/blob/main/tests/test_boveda_examen.py
- Prospective LLM pilot: https://github.com/recinosr/wall-street-motor/blob/main/lab/vita_meses.py
- One-shot LLM workflow: https://github.com/recinosr/wall-street-motor/blob/main/.github/workflows/vita-meses.yml
- Prospective forecast ledger and Hedge weighting: https://github.com/recinosr/wall-street-motor/blob/main/lab/pronostico.py
- Paper crypto causal custody: https://github.com/recinosr/wall-street-motor/blob/main/lab/demo_cripto.py
- VITA Opera hash-chain ledger: https://github.com/recinosr/wall-street-motor/blob/main/lab/vita_opera.py
- Scheduler supervisor: https://github.com/recinosr/wall-street-motor/blob/main/scripts/vigilante.py
- PIT limitations/results: https://github.com/recinosr/wall-street-motor/blob/main/docs/reporte_tarea32.md
- Bóveda result report: https://github.com/recinosr/wall-street-motor/blob/main/docs/reporte_tarea21b.md
- Monthly cohort and multiplicity report: https://github.com/recinosr/wall-street-motor/blob/main/docs/reporte_tarea22.md
- License: https://github.com/recinosr/wall-street-motor/blob/main/LICENSE

**Final disposition:** high-value architecture donor; no proven alpha; research-only until an Icarus-native design review, implementation, adversarial tests and prospective qualification are complete.
