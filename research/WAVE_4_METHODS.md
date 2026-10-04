# Wave 4 Research Methods

## M56 — Expected-vs-Actual Event Surprise
Estimate expectations from pre-event information; research residual surprise, not raw realization.

Applications:
contract awards, buyback acceptance, auctions, regulatory severity, insider trade materiality.

## M57 — Lifecycle State Models
Use state-transition/survival models for procurement, regulation, capital raising and permits instead of isolated event dummies.

## M58 — Materiality Normalization
Normalize event magnitude to the economic object:
contract/revenue, buyback/eligible float, ATM/float, outage/regional load, procurement/sector revenue.

## M59 — Known Mechanical vs New Information
For scheduled operations split:
preannounced mechanics
+ eligible-set revisions
+ participation/tender surprise
+ allocation/result surprise.

Do not label preannounced flow as new information.

## M60 — Reporting-Lag Surface
Learn action_date -> first_public_seen_time by source, agency, event type and period.

Backtests key to availability time.

## M61 — Docket/Document Graph Reconstruction
Link amendments, corrections, responses and predecessor filings so restatements are not double-counted as independent events.

## M62 — Entity Resolution Confidence
Store legal-entity and public-issuer mappings with IDs, source, effective dates and confidence.

Low-confidence mappings cannot promote signals.

## M63 — Exposure Graph Before Sentiment
Map product/NAICS/PSC/geography/revenue/facility/supplier exposure before attaching text sentiment or severity.

## M64 — Event Competition Control
Model overlapping events. Do not assign a CPI-day Treasury move entirely to a concurrent buyback or auction.

## M65 — Preannouncement Efficiency Test
Measure behavior at:
schedule announcement -> pre-operation -> start -> close -> result -> settlement.

Determines when information enters price.

## M66 — Point-in-Time Legal Capacity
For dilution research reconstruct what issuance capacity was legally effective at each historical timestamp.

## M67 — Planned-vs-Discretionary Insider Classification
Control for 10b5-1, compensation grants/exercises, tax withholding, routine sale history and role.

## M68 — Multi-Source Scarcity Confirmation
Require incremental information from independent scarcity channels before promoting a composite.

## M69 — Process Mining for Public Events
Use timestamped process logs to learn normal lifecycle paths and detect unusual transitions in procurement, dockets and capital raises.

## M70 — Administrative-Data Reconciliation
Maintain differences in source definitions, first-public timestamps and revision histories instead of silently selecting a preferred value.
