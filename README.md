# ideas-reality

Research staging vault for ideas that may later be implemented by Claude in ICARUS.

This repository is intentionally separate from the ICARUS implementation repository.

## Purpose

Capture genuinely new or underused market-edge hypotheses, alternative data sources, composite signals, and research methods before implementation.

Nothing in this repository should be treated as a proven trading edge. Every item is a falsifiable research candidate.

## Current research package

- CLAUDE_HANDOFF.md — prioritized handoff and implementation-neutral requirements
- research/EDGE_ATLAS.md — edge hypotheses
- research/DATA_SOURCE_REGISTRY.md — source, latency, availability, licensing/status
- research/COMPOSITE_SYSTEM_CONCEPTS.md — higher-order multi-source inventions
- research/RESEARCH_PROTOCOL.md — discovery, falsification, promotion, and retirement protocol
- research/NEGATIVE_CONTROLS.md — anti-overfitting and anti-leakage tests
- research/research_index.json — machine-readable index

## Boundary

Claude owns ICARUS implementation, repo engineering, ML hardening, CI, integration, and repair.

This repository is a research inbox. It must not directly modify ICARUS.

## Research standard

A candidate is not an edge until it survives:
1. exact as-of timing,
2. realistic publication latency,
3. leakage checks,
4. transaction costs and execution assumptions,
5. purged/embargoed walk-forward tests,
6. multiple-testing control,
7. regime and market transfer tests,
8. negative controls/placebos,
9. terminal holdout,
10. live shadow validation.
