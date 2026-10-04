# Canonical Source Catalog

Status: CANONICAL GOVERNANCE
Effective: 2026-10-04

The authoritative detailed source records live in each wave's `*_SOURCE_NOTES.md`. This file defines the repository-wide catalog contract and indexes those records.

## Source record contract

Every canonical source ID must contain or inherit:
1. canonical source ID
2. exact primary URL/document/feed when available
3. source owner
4. dataset/feed/rule name
5. availability class from DATA_AVAILABILITY_CONTRACTS.md
6. native cadence
7. public latency semantics
8. revision/version behavior
9. access/rights status
10. fields required by the candidate
11. historical archive/vintage plan
12. source-health failure behavior
13. known coverage/selection limitations

If an exact primary artifact cannot be pinned, the source must be explicitly marked PROVENANCE_PENDING and is not DATA_VERIFIED.

## Wave source-note index

- W1: WAVE_1_SOURCE_NOTES.md
- W2: WAVE_2_SOURCE_NOTES.md
- W3: WAVE_3_SOURCE_NOTES.md
- W4F: WAVE_4_SOURCE_NOTES.md
- W5P: WAVE_5_SOURCE_NOTES.md
- W6 / W6N: WAVE_6_SOURCE_NOTES.md / WAVE_6_NQ_GOLD_SOURCE_NOTES.md
- W7 / W7T: WAVE_7_SOURCE_NOTES.md / WAVE_7_TELEMETRY_SOURCE_NOTES.md
- W8M/W8R through W41M: use the matching WAVE_*_SOURCE_NOTES.md files referenced by CANONICAL_ID_REGISTRY.md.

## Global source quality states

- SOURCE_VERIFIED: exact primary provenance and timing contract exist.
- TIMING_PENDING: provenance is exact but live-public latency is not yet established.
- RIGHTS_PENDING: data semantics are valid but production access/redistribution needs confirmation.
- PROVENANCE_PENDING: exact primary artifact not yet pinned.
- RETROSPECTIVE_ONLY: intentionally delayed source used only for labels/validation.
- WATCH_NOT_LIVE: future/not-yet-live source.
- RETIRED: rejected for current research use.

## Non-negotiable rules

- Never upgrade a source because a secondary article quotes an official.
- Never infer public latency from statutory reporter deadlines.
- Never treat an event-driven feed's silence as a zero.
- Never treat a current webpage as proof of historical availability.
- Never use a later correction before its publication time.
