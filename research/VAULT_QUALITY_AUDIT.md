# Vault Quality Audit

Audit opened: 2026-10-04
Scope: entire `research/` vault through W41M plus legacy W1/W2.

## Standard

The audit checks:
- exact primary provenance
- public-time semantics
- source cadence/latency class
- point-in-time revisions/vintages
- rule/schema effective-date versioning
- access/rights separation
- mechanism and intermediate target
- falsification and negative controls
- dependency/double-counting
- no direct leap from interesting data to alpha

## Initial findings

The vault's research protocol and negative controls are strong, but the source layer was not uniform.

Structural lint found multiple source-note sections that named a primary source generically rather than pinning an exact primary artifact. Those defects are being repaired wave by wave.

Timing audit also found cases where wording such as LIVE, "first alert", or a statutory reporting deadline could be read more strongly than the primary documentation supports. These are being converted to explicit availability classes.

Legacy W1/W2 predated the source-note convention and are being brought under the same contract.

## Completion criteria

This audit is not complete until:
1. all source-note Primary blocks resolve to an exact primary artifact or are explicitly downgraded;
2. W1/W2 have source-note files;
3. no statutory deadline is used as public availability;
4. known delayed sources are quarantined from shorter horizons;
5. current 2025–2026 rule changes are versioned where material;
6. a second structural lint finds no hidden generic Primary blocks;
7. repaired tree is committed and re-read from main.

Until then, do not describe the vault as fully audited.
