# RDX01 — Defect Emergence & Recall Mechanics

Thesis: a recall is the end of a defect-emergence process. NHTSA exposes public layers with distinct clocks: daily complaints, manufacturer communications/TSBs, investigations, daily recall records, Part 573 chronology/remedy filings, foreign recalls and slower EWR/completion data.

## Edge candidates

### RDX01-E01 — Daily Complaint Defect Pulse
Normalize NHTSA complaint arrivals by model-year exposure, vehicle age, season and mileage.

### RDX01-E02 — Complaint Acceleration
Short-window complaint rate, first derivative and second derivative versus historical baseline.

### RDX01-E03 — Severity-Weighted Complaint Pulse
Use crash/fire/injury/death flags as severity dimensions without treating allegations as verified defects.

### RDX01-E04 — Narrative Cluster Emergence
Detect new failure-mode clusters from point-in-time complaint text/components.

### RDX01-E05 — Shared-Component Complaint Graph
Model/year -> component -> sibling platforms -> verified common supplier/architecture.

### RDX01-E06 — Manufacturer Communication / TSB Pulse
Track new dealer/owner communications by model, component and communication type.

### RDX01-E07 — Dealer Knowledge Before Recall
Measure communication date/public receipt relative to later recall publication.

### RDX01-E08 — Service Escalation Ladder
ROUTINE_TSB -> SERVICE_CAMPAIGN -> WARRANTY_EXTENSION -> STOP_SALE/HOLD -> SAFETY_RECALL.

### RDX01-E09 — Complaint × Communication Convergence
Increase defect confidence when independent layers converge on the same failure mode.

### RDX01-E10 — Complaint/TSB Reality Gap
States: complaints rising/no communication; communication/low complaints; both rising; both quiet.

### RDX01-E11 — Investigation Open Shock
Separate Defect Petition, Preliminary Evaluation, Recall Query and Engineering Analysis.

### RDX01-E12 — Investigation Escalation Hazard
Estimate transition probability/time from review/PE/EA/RQ toward recall or closure.

### RDX01-E13 — Investigation Duration Stress
Test whether prolonged investigation adds information about later recall severity/cost.

### RDX01-E14 — Part 573 Legal Commitment
Manufacturer safety-defect determination -> filing within five business days -> public legal commitment point.

### RDX01-E15 — Part 573 Chronology Extraction
Extract only public-at-filing facts: complaints, warranty claims, crashes, injuries, fatalities, supplier discussions and internal review dates.

### RDX01-E16 — Recall Population Surprise
Reported population minus point-in-time expected scope inferred from model-year/platform/component evidence.

### RDX01-E17 — Scope Expansion Hazard
Predict later amendments/superseding campaigns from post-recall complaints, common-component evidence and investigation state.

### RDX01-E18 — Remedy Availability State
RECALL_KNOWN / REMEDY_UNAVAILABLE / INTERIM / FINAL / REVISED.

### RDX01-E19 — Dealer Stop-Sale Exposure
Affected new unsold inventory × days until remedy × vehicle value/carrying cost, using campaign-specific evidence.

### RDX01-E20 — Unsellable Inventory Days
Recall-publication to remedy/release interval.

### RDX01-E21 — Remedy Parts Bottleneck
Affected population × parts availability × dealer service capacity; split OTA/software from hardware.

### RDX01-E22 — OTA Remedy Compression
Compare filing-to-remedy and completion behavior for software-addressable versus physical-service campaigns.

### RDX01-E23 — Recall Completion Velocity
Track repaired/completed share using point-in-time public status data.

### RDX01-E24 — Unresolved Safety Population
Affected population minus estimated completed/remedied/scrapped/exported units with uncertainty bands.

### RDX01-E25 — EWR Defect Pressure
Use public Early Warning Reporting aggregates only at actual quarterly availability.

### RDX01-E26 — Foreign Recall Lead
Foreign recall determination -> later U.S. campaign probability for verified substantially similar products.

### RDX01-E27 — Cross-Jurisdiction Propagation
Foreign campaign -> U.S. equivalent component/model -> domestic complaint/TSB state -> U.S. recall.

### RDX01-E28 — Supplier Defect Propagation
Supplier/component -> OEM programs -> common defect -> multi-OEM campaign probability.

### RDX01-E29 — Supplier Financial Spillover
Weight supplier exposure by disclosed customer dependence and component relevance.

### RDX01-E30 — Defect Cost Envelope
Repair + labor + parts/logistics + stop-sale inventory + warranty extension + compensation + regulatory/legal + production/rework.

### RDX01-E31 — Production Interruption Risk
FIELD_ONLY / DEALER_STOP_SALE / PRODUCTION_HOLD / SUPPLIER_CONTAINMENT / PLANT_STOP.

### RDX01-E32 — Defect-to-Production Propagation
Complaint/TSB/recall -> supplier containment -> shortage/rework -> assembly disruption -> dealer inventory.

### RDX01-E33 — Recall Severity Tensor
Population, hazard, crash/fire/injury evidence, remedy availability, stop-sale, production effect, age, supplier concentration, investigation duration.

### RDX01-E34 — Defect Emergence Hazard Model
Target P(Part 573 recall within N days) from point-in-time complaints, communications, investigation state, foreign recalls, EWR vintages and component graph.

### RDX01-E35 — Remedy Delay Hazard
Target P(final remedy unavailable after N days) from complexity, supplier, population and initial filing.

### RDX01-E36 — Recall Market-Reaction Residual
Actual equity reaction minus expected reaction conditioned on size, severity, investigation duration, remedy, age and prior information.

### RDX01-E37 — Recall Truth Ladder
COMPLAINT -> TSB/COMMUNICATION -> INVESTIGATION -> DEFECT DETERMINATION -> PART 573 -> STOP-SALE/REMEDY -> COMPLETION -> WARRANTY/PRODUCTION/CASH COST -> EARNINGS.

## Highest-priority tests
E02, E07, E09, E12, E15, E16, E19, E26, E34, E37.
