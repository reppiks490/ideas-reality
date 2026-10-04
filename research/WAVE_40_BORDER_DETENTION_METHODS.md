# Wave 40B — Research Methods

Namespace: **W40B**

## W40B-M01 — Prospective FDA Import-Alert Archive
FDA says alert databases update in real time, but historical end-dated/deactivated copies may require FOIA.

Archive complete snapshots prospectively and diff them.

## W40B-M02 — List-Semantics Engine
Red/Yellow List and Green List have opposite inclusion semantics.

Encode alert-specific list type before deciding eligibility.

## W40B-M03 — Alert Publish vs List Change
An alert's page publish/revision date may not uniquely identify every firm-list change.

Store first observed change timestamp separately.

## W40B-M04 — DWPE Is Conditional Detention
A DWPE listing does not prove every shipment is finally refused.

Model eligibility/release probability separately.

## W40B-M05 — Final Refusal Lag
FDA Import Refusal dashboard contains final actions and updates weekly.

Use it as delayed outcome validation, not instant detention.

## W40B-M06 — Refusal Entity Resolution
Manufacturer/importer/product names can vary.

Normalize with original-text retention and confidence.

## W40B-M07 — Product-Code Mapping
Map FDA product codes to economic product families and downstream uses point-in-time.

## W40B-M08 — CBP WRO Public-Time Archive
Archive each WRO/Finding addition, modification and removal as first public.

## W40B-M09 — WRO != Finding
WRO detention and Finding seizure have distinct legal states.

Never pool them as one severity.

## W40B-M10 — No Specific-Detention Inference
CBP states it does not generally publicize specific detentions/re-exportations/exclusions/seizures under WROs/Findings.

Do not invent shipment-level outcomes.

## W40B-M11 — UFLPA Entity Effective Time
Use Federal Register/DHS effective date and first-public time.

## W40B-M12 — UFLPA Aggregate-Only Gate
CBP dashboard sector/country statistics are aggregate.

No company attribution without separate public evidence.

## W40B-M13 — Pending Outcome Censoring
UFLPA pending reviews are right-censored outcomes.

Do not count pending as denied or released.

## W40B-M14 — Import Exposure Denominator
Use historical customs/import data to estimate supplier/product share at risk.

## W40B-M15 — Transshipment / Country-of-Origin Caution
Country of shipment may differ from upstream material origin.

Require sourced supply-chain lineage.

## W40B-M16 — Substitute-Capacity Validation
An alternative supplier counts only if:
qualified,
legally eligible,
capacity available,
product interchangeable.

## W40B-M17 — Inventory Buffer
Translate import loss through domestic inventory days before shortage claims.

## W40B-M18 — Cross-Event Deduplication
One underlying compliance event may generate:
alert revision,
warning letter,
refusal,
shortage notice,
company disclosure.

Parent under a common incident.

## W40B-M19 — Regulatory State vs Outcome
Restriction status is exposure; final import volume loss/shortage is outcome.

## W40B-M20 — Physical Promotion Gate
Before market alpha require OOS improvement in:
import volume loss,
refusal/denial realization,
inventory draw,
shortage,
or substitute flow.
