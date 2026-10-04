# Canonical Research ID Registry

## Purpose

Multiple research processes are contributing to this repository concurrently. Early research used global-looking IDs such as `E81`. A later concurrent wave reused `E81-E100` while Wave 3 already contained `E81-E90`. No research content was lost, but those legacy IDs are ambiguous outside their source file.

From this point forward, **wave-scoped IDs are canonical**. Legacy IDs remain historical aliases only.

## Canonical scheme

`<namespace>-<type><number>`

Examples:
- `W1-E03`
- `W2-E01`
- `W3-E21`
- `W4F-E01`
- `W5P-E01`
- `W6N-E01`

Types:
- E = edge / hypothesis
- M = research method
- D = data source
- C = composite concept
- N = negative control
- W = future watchlist item

## Namespace map

### W1 — Core Edge Atlas
Sources:
- `research/EDGE_ATLAS.md`
- `research/WAVE_1_SOURCE_NOTES.md`

- Legacy E01-E40 -> W1-E01 through W1-E40
- Legacy W01-W03 -> W1-W01 through W1-W03

### W2 — Regulatory / short-pressure wave
Sources:
- `research/WAVE_2_DISCOVERIES.md`
- `research/WAVE_2_METHODS.md`
- `research/WAVE_2_SOURCE_NOTES.md`

- Legacy E41-E60 -> W2-E01 through W2-E20
- Legacy M21-M40 -> W2-M01 through W2-M20

### W3 — Crypto / physical-energy / innovation wave
Sources:
- `research/WAVE_3_DISCOVERIES.md`
- `research/WAVE_3_METHODS.md`

- Legacy E61-E90 -> W3-E01 through W3-E30
- Legacy M41-M55 -> W3-M01 through W3-M15

### W4F — Funding / Treasury / procurement / ownership wave
Sources:
- `research/WAVE_4_DISCOVERIES.md`
- `research/WAVE_4_METHODS.md`

- Legacy E81-E100 -> W4F-E01 through W4F-E20
- Legacy M56-M70 -> W4F-M01 through W4F-M15

**Collision note:** legacy W4F E81-E90 overlaps legacy W3 E81-E90. Never join or refer across files using those legacy IDs alone.

### W5P — Physical-delivery / sanctions / cyber / port / tariff wave
Sources:
- `research/WAVE_5_DISCOVERIES.md`
- `research/WAVE_5_METHODS.md`

- Legacy E101-E122 -> W5P-E01 through W5P-E22
- Legacy M71-M90 -> W5P-M01 through W5P-M20

### W6N — NQ / gold / credit / procurement / policy wave
Sources:
- `research/WAVE_6_NQ_GOLD_DISCOVERIES.md`
- `research/WAVE_6_NQ_GOLD_METHODS.md`
- `research/WAVE_6_NQ_GOLD_SOURCE_NOTES.md`

W6N uses canonical IDs directly.

### W7T — Physical network telemetry wave
Sources:
- `research/WAVE_7_TELEMETRY_DISCOVERIES.md`
- `research/WAVE_7_TELEMETRY_METHODS.md`
- `research/WAVE_7_TELEMETRY_SOURCE_NOTES.md`

W7T uses canonical IDs directly:
- edges W7T-E01 through W7T-E23
- methods W7T-M01 through W7T-M20
- sources W7T-D01 through W7T-D12

### W8M — Mechanical flow / pre-trade intent wave
Sources:
- `research/WAVE_8_MECHANICAL_FLOWS_DISCOVERIES.md`
- `research/WAVE_8_MECHANICAL_FLOWS_METHODS.md`
- `research/WAVE_8_MECHANICAL_FLOWS_SOURCE_NOTES.md`

W8M uses canonical IDs directly:
- edges W8M-E01 through W8M-E24
- methods W8M-M01 through W8M-M20
- sources W8M-D01 through W8M-D08

### W9O — Hidden operational exhaust wave
Sources:
- `research/WAVE_9_OPERATIONAL_EXHAUST_DISCOVERIES.md`
- `research/WAVE_9_OPERATIONAL_EXHAUST_METHODS.md`
- `research/WAVE_9_OPERATIONAL_EXHAUST_SOURCE_NOTES.md`

W9O uses canonical IDs directly:
- edges W9O-E01 through W9O-E23
- methods W9O-M01 through W9O-M22
- sources W9O-D01 through W9O-D11

### W10B — Dealer balance-sheet / funding-plumbing wave
Sources:
- `research/WAVE_10_BALANCE_SHEET_DISCOVERIES.md`
- `research/WAVE_10_BALANCE_SHEET_METHODS.md`
- `research/WAVE_10_BALANCE_SHEET_SOURCE_NOTES.md`

W10B uses canonical IDs directly:
- edges W10B-E01 through W10B-E22
- methods W10B-M01 through W10B-M20
- sources W10B-D01 through W10B-D08

### W11S — Future physical supply pipeline wave
Sources:
- `research/WAVE_11_FUTURE_SUPPLY_DISCOVERIES.md`
- `research/WAVE_11_FUTURE_SUPPLY_METHODS.md`
- `research/WAVE_11_FUTURE_SUPPLY_SOURCE_NOTES.md`

W11S uses canonical IDs directly:
- edges W11S-E01 through W11S-E23
- methods W11S-M01 through W11S-M20
- sources W11S-D01 through W11S-D08

### W12C — Clearing / margin / delivery mechanics wave
Sources:
- `research/WAVE_12_CLEARING_MARGIN_DISCOVERIES.md`
- `research/WAVE_12_CLEARING_MARGIN_METHODS.md`
- `research/WAVE_12_CLEARING_MARGIN_SOURCE_NOTES.md`

W12C uses canonical IDs directly:
- edges W12C-E01 through W12C-E24
- methods W12C-M01 through W12C-M22
- sources W12C-D01 through W12C-D08

## Durable identity

The durable machine key should be:

`canonical_id + source_file + content_hash`

Titles are allowed to evolve without changing identity. If an idea is materially redefined rather than refined, allocate a new canonical ID and link it as a successor.

## Rules for Claude

When importing or discussing a candidate:
1. Use the canonical ID.
2. Preserve its source file and content hash.
3. Preserve a legacy ID only as an alias.
4. Never join records on a legacy ID alone.
5. If two candidates overlap conceptually, keep both provenance records and explicitly merge them in a new synthesis record rather than silently deleting one.

## Rules for future contributors

1. Never allocate new unscoped global `E###` or `M###` IDs.
2. Create a unique namespace before adding a wave.
3. Do not rewrite another contributor's historical source file merely to renumber it.
4. Add mappings here instead.
5. No force-pushing to resolve concurrent contributions.


### W8R — Pre-regulatory warning / safety lifecycle wave
Sources:
- `research/WAVE_8_REGULATORY_DISCOVERIES.md`
- `research/WAVE_8_REGULATORY_METHODS.md`
- `research/WAVE_8_REGULATORY_SOURCE_NOTES.md`

W8R uses canonical IDs directly:
- edges W8R-E01 through W8R-E20
- methods W8R-M01 through W8R-M20
- sources W8R-D01 through W8R-D10


### W9C — Capacity rights before reality wave
Sources:
- `research/WAVE_9_CAPACITY_RIGHTS_DISCOVERIES.md`
- `research/WAVE_9_CAPACITY_RIGHTS_METHODS.md`
- `research/WAVE_9_CAPACITY_RIGHTS_SOURCE_NOTES.md`

W9C uses canonical IDs directly:
- edges W9C-E01 through W9C-E20
- methods W9C-M01 through W9C-M20
- sources W9C-D01 through W9C-D10


### W11C — Mandatory commitments / convexity wave
Sources:
- `research/WAVE_11_COMMITMENT_CONVEXITY_DISCOVERIES.md`
- `research/WAVE_11_COMMITMENT_CONVEXITY_METHODS.md`
- `research/WAVE_11_COMMITMENT_CONVEXITY_SOURCE_NOTES.md`

W11C uses canonical IDs directly:
- edges W11C-E01 through W11C-E22
- methods W11C-M01 through W11C-M20
- sources W11C-D01 through W11C-D10


### W12F — Freight / livestock / exchange rule-state wave
Sources:
- `research/WAVE_12_FREIGHT_RULESTATE_DISCOVERIES.md`
- `research/WAVE_12_FREIGHT_RULESTATE_METHODS.md`
- `research/WAVE_12_FREIGHT_RULESTATE_SOURCE_NOTES.md`

W12F uses canonical IDs directly:
- edges W12F-E01 through W12F-E22
- methods W12F-M01 through W12F-M20
- sources W12F-D01 through W12F-D10


### W13H — Human capacity / communications resilience wave
Sources:
- `research/WAVE_13_HUMAN_CAPACITY_DISCOVERIES.md`
- `research/WAVE_13_HUMAN_CAPACITY_METHODS.md`
- `research/WAVE_13_HUMAN_CAPACITY_SOURCE_NOTES.md`

W13H uses canonical IDs directly:
- edges W13H-E01 through W13H-E24
- methods W13H-M01 through W13H-M20
- sources W13H-D01 through W13H-D10


### W14I — Critical infrastructure / chokepoints wave
Sources:
- `research/WAVE_14_INFRASTRUCTURE_CHOKEPOINTS_DISCOVERIES.md`
- `research/WAVE_14_INFRASTRUCTURE_CHOKEPOINTS_METHODS.md`
- `research/WAVE_14_INFRASTRUCTURE_CHOKEPOINTS_SOURCE_NOTES.md`

W14I uses canonical IDs directly:
- edges W14I-E01 through W14I-E25
- methods W14I-M01 through W14I-M20
- sources W14I-D01 through W14I-D10


### W15X — Industrial upset / thermal telemetry wave
Sources:
- `research/WAVE_15_INDUSTRIAL_THERMAL_DISCOVERIES.md`
- `research/WAVE_15_INDUSTRIAL_THERMAL_METHODS.md`
- `research/WAVE_15_INDUSTRIAL_THERMAL_SOURCE_NOTES.md`

W15X uses canonical IDs directly:
- edges W15X-E01 through W15X-E25
- methods W15X-M01 through W15X-M20
- sources W15X-D01 through W15X-D10


### W16S — Service degradation / administrative throughput wave
Sources:
- `research/WAVE_16_SERVICE_DEGRADATION_DISCOVERIES.md`
- `research/WAVE_16_SERVICE_DEGRADATION_METHODS.md`
- `research/WAVE_16_SERVICE_DEGRADATION_SOURCE_NOTES.md`

W16S uses canonical IDs directly:
- edges W16S-E01 through W16S-E27
- methods W16S-M01 through W16S-M20
- sources W16S-D01 through W16S-D10


### W17P — Market plumbing / operational integrity wave
Sources:
- `research/WAVE_17_MARKET_PLUMBING_DISCOVERIES.md`
- `research/WAVE_17_MARKET_PLUMBING_METHODS.md`
- `research/WAVE_17_MARKET_PLUMBING_SOURCE_NOTES.md`

W17P uses canonical IDs directly:
- edges W17P-E01 through W17P-E24
- methods W17P-M01 through W17P-M20
- sources W17P-D01 through W17P-D10


### W18G — Geophysical / space-weather exposure wave
Sources:
- `research/WAVE_18_GEOPHYSICAL_SPACE_WEATHER_DISCOVERIES.md`
- `research/WAVE_18_GEOPHYSICAL_SPACE_WEATHER_METHODS.md`
- `research/WAVE_18_GEOPHYSICAL_SPACE_WEATHER_SOURCE_NOTES.md`

W18G uses canonical IDs directly:
- edges W18G-E01 through W18G-E28
- methods W18G-M01 through W18G-M20
- sources W18G-D01 through W18G-D10


### W19B — Biological supply / quarantine wave
Sources:
- `research/WAVE_19_BIOLOGICAL_SUPPLY_DISCOVERIES.md`
- `research/WAVE_19_BIOLOGICAL_SUPPLY_METHODS.md`
- `research/WAVE_19_BIOLOGICAL_SUPPLY_SOURCE_NOTES.md`

W19B uses canonical IDs directly:
- edges W19B-E01 through W19B-E28
- methods W19B-M01 through W19B-M20
- sources W19B-D01 through W19B-D10


### W20E — Emergency constraint-release wave
Sources:
- `research/WAVE_20_EMERGENCY_CONSTRAINT_RELEASE_DISCOVERIES.md`
- `research/WAVE_20_EMERGENCY_CONSTRAINT_RELEASE_METHODS.md`
- `research/WAVE_20_EMERGENCY_CONSTRAINT_RELEASE_SOURCE_NOTES.md`

W20E uses canonical IDs directly:
- edges W20E-E01 through W20E-E26
- methods W20E-M01 through W20E-M20
- sources W20E-D01 through W20E-D10


### W21D — Fleet defect / mandatory remediation wave
Sources:
- `research/WAVE_21_FLEET_DEFECT_DISCOVERIES.md`
- `research/WAVE_21_FLEET_DEFECT_METHODS.md`
- `research/WAVE_21_FLEET_DEFECT_SOURCE_NOTES.md`

W21D uses canonical IDs directly:
- edges W21D-E01 through W21D-E26
- methods W21D-M01 through W21D-M20
- sources W21D-D01 through W21D-D10


### W22G — Gas transport / nomination exhaust wave
Sources:
- `research/WAVE_22_GAS_TRANSPORT_DISCOVERIES.md`
- `research/WAVE_22_GAS_TRANSPORT_METHODS.md`
- `research/WAVE_22_GAS_TRANSPORT_SOURCE_NOTES.md`

W22G uses canonical IDs directly:
- edges W22G-E01 through W22G-E31
- methods W22G-M01 through W22G-M20
- sources W22G-D01 through W22G-D10


### W23T — Transmission topology / congestion mechanics wave
Sources:
- `research/WAVE_23_TRANSMISSION_TOPOLOGY_DISCOVERIES.md`
- `research/WAVE_23_TRANSMISSION_TOPOLOGY_METHODS.md`
- `research/WAVE_23_TRANSMISSION_TOPOLOGY_SOURCE_NOTES.md`

W23T uses canonical IDs directly:
- edges W23T-E01 through W23T-E32
- methods W23T-M01 through W23T-M20
- sources W23T-D01 through W23T-D10


### W24A — Generation availability / forced-outage scarcity wave
Sources:
- `research/WAVE_24_GENERATION_AVAILABILITY_DISCOVERIES.md`
- `research/WAVE_24_GENERATION_AVAILABILITY_METHODS.md`
- `research/WAVE_24_GENERATION_AVAILABILITY_SOURCE_NOTES.md`

W24A uses canonical IDs directly:
- edges W24A-E01 through W24A-E32
- methods W24A-M01 through W24A-M20
- sources W24A-D01 through W24A-D10


### W24M — Marine operability / navigable capacity wave
Sources:
- `research/WAVE_24_MARINE_OPERABILITY_DISCOVERIES.md`
- `research/WAVE_24_MARINE_OPERABILITY_METHODS.md`
- `research/WAVE_24_MARINE_OPERABILITY_SOURCE_NOTES.md`

W24M uses canonical IDs directly:
- edges W24M-E01 through W24M-E30
- methods W24M-M01 through W24M-M20
- sources W24M-D01 through W24M-D10


### W25R — Reserve / ramp / flexibility scarcity wave
Sources:
- `research/WAVE_25_RESERVE_RAMP_DISCOVERIES.md`
- `research/WAVE_25_RESERVE_RAMP_METHODS.md`
- `research/WAVE_25_RESERVE_RAMP_SOURCE_NOTES.md`

W25R uses canonical IDs directly:
- edges W25R-E01 through W25R-E32
- methods W25R-M01 through W25R-M20
- sources W25R-D01 through W25R-D10


### W25C — Credit lead / distress transmission wave
Sources:
- `research/WAVE_25_CREDIT_LEAD_DISCOVERIES.md`
- `research/WAVE_25_CREDIT_LEAD_METHODS.md`
- `research/WAVE_25_CREDIT_LEAD_SOURCE_NOTES.md`

W25C uses canonical IDs directly:
- edges W25C-E01 through W25C-E28
- methods W25C-M01 through W25C-M20
- sources W25C-D01 through W25C-D10


### W26R — Benchmark rebalance / forced-flow wave
Sources:
- `research/WAVE_26_REBALANCE_FORCED_FLOW_DISCOVERIES.md`
- `research/WAVE_26_REBALANCE_FORCED_FLOW_METHODS.md`
- `research/WAVE_26_REBALANCE_FORCED_FLOW_SOURCE_NOTES.md`

W26R uses canonical IDs directly:
- edges W26R-E01 through W26R-E32
- methods W26R-M01 through W26R-M20
- sources W26R-D01 through W26R-D10


### W27V — Volatility constraint / reopening mechanics wave
Sources:
- `research/WAVE_27_VOLATILITY_CONSTRAINT_DISCOVERIES.md`
- `research/WAVE_27_VOLATILITY_CONSTRAINT_METHODS.md`
- `research/WAVE_27_VOLATILITY_CONSTRAINT_SOURCE_NOTES.md`

W27V uses canonical IDs directly:
- edges W27V-E01 through W27V-E35
- methods W27V-M01 through W27V-M20
- sources W27V-D01 through W27V-D10


### W28M — Mine withdrawal / forced capacity-loss wave
Sources:
- `research/WAVE_28_MINE_WITHDRAWAL_DISCOVERIES.md`
- `research/WAVE_28_MINE_WITHDRAWAL_METHODS.md`
- `research/WAVE_28_MINE_WITHDRAWAL_SOURCE_NOTES.md`

W28M uses canonical IDs directly:
- edges W28M-E01 through W28M-E25
- methods W28M-M01 through W28M-M20
- sources W28M-D01 through W28M-D10


### W29L — Labor dispute clocks / capacity-risk wave
Sources:
- `research/WAVE_29_LABOR_DISPUTE_DISCOVERIES.md`
- `research/WAVE_29_LABOR_DISPUTE_METHODS.md`
- `research/WAVE_29_LABOR_DISPUTE_SOURCE_NOTES.md`

W29L uses canonical IDs directly:
- edges W29L-E01 through W29L-E28
- methods W29L-M01 through W29L-M20
- sources W29L-D01 through W29L-D10


### W30W — Industrial water / thermal capacity wave
Sources:
- `research/WAVE_30_INDUSTRIAL_WATER_DISCOVERIES.md`
- `research/WAVE_30_INDUSTRIAL_WATER_METHODS.md`
- `research/WAVE_30_INDUSTRIAL_WATER_SOURCE_NOTES.md`

W30W uses canonical IDs directly:
- edges W30W-E01 through W30W-E28
- methods W30W-M01 through W30W-M20
- sources W30W-D01 through W30W-D10


### W31C — Catastrophe loss-development wave
Sources:
- `research/WAVE_31_CATASTROPHE_LOSS_DISCOVERIES.md`
- `research/WAVE_31_CATASTROPHE_LOSS_METHODS.md`
- `research/WAVE_31_CATASTROPHE_LOSS_SOURCE_NOTES.md`

W31C uses canonical IDs directly:
- edges W31C-E01 through W31C-E26
- methods W31C-M01 through W31C-M20
- sources W31C-D01 through W31C-D10


### W31F — Animal processing / protein supply-capacity wave
Sources:
- `research/WAVE_31_ANIMAL_PROCESSING_DISCOVERIES.md`
- `research/WAVE_31_ANIMAL_PROCESSING_METHODS.md`
- `research/WAVE_31_ANIMAL_PROCESSING_SOURCE_NOTES.md`

W31F uses canonical IDs directly:
- edges W31F-E01 through W31F-E32
- methods W31F-M01 through W31F-M20
- sources W31F-D01 through W31F-D10


### W32R — Reality gap / cross-layer contradiction wave
Sources:
- `research/WAVE_32_REALITY_GAP_DISCOVERIES.md`
- `research/WAVE_32_REALITY_GAP_METHODS.md`
- `research/WAVE_32_REALITY_GAP_SOURCE_NOTES.md`

W32R uses canonical IDs directly:
- edges W32R-E01 through W32R-E36
- methods W32R-M01 through W32R-M20
- sources W32R-D01 through W32R-D10


### W32I — Issuer mechanical-flow wave
Sources:
- `research/WAVE_32_ISSUER_FLOW_DISCOVERIES.md`
- `research/WAVE_32_ISSUER_FLOW_METHODS.md`
- `research/WAVE_32_ISSUER_FLOW_SOURCE_NOTES.md`

W32I uses canonical IDs directly:
- edges W32I-E01 through W32I-E34
- methods W32I-M01 through W32I-M20
- sources W32I-D01 through W32I-D10


### W33S — Short constraint / settlement-stress wave
Sources:
- `research/WAVE_33_SHORT_CONSTRAINT_DISCOVERIES.md`
- `research/WAVE_33_SHORT_CONSTRAINT_METHODS.md`
- `research/WAVE_33_SHORT_CONSTRAINT_SOURCE_NOTES.md`

W33S uses canonical IDs directly:
- edges W33S-E01 through W33S-E32
- methods W33S-M01 through W33S-M20
- sources W33S-D01 through W33S-D10


### W34D — Digital infrastructure outage / dependency-propagation wave
Sources:
- `research/WAVE_34_DIGITAL_INFRASTRUCTURE_DISCOVERIES.md`
- `research/WAVE_34_DIGITAL_INFRASTRUCTURE_METHODS.md`
- `research/WAVE_34_DIGITAL_INFRASTRUCTURE_SOURCE_NOTES.md`

W34D uses canonical IDs directly:
- edges W34D-E01 through W34D-E34
- methods W34D-M01 through W34D-M20
- sources W34D-D01 through W34D-D10


### W35C — Subsea connectivity / repair-capacity wave
Sources:
- `research/WAVE_35_SUBSEA_CONNECTIVITY_DISCOVERIES.md`
- `research/WAVE_35_SUBSEA_CONNECTIVITY_METHODS.md`
- `research/WAVE_35_SUBSEA_CONNECTIVITY_SOURCE_NOTES.md`

W35C uses canonical IDs directly:
- edges W35C-E01 through W35C-E30
- methods W35C-M01 through W35C-M20
- sources W35C-D01 through W35C-D10


### W36P — Pharmaceutical manufacturing / drug-availability wave
Sources:
- `research/WAVE_36_PHARMA_SUPPLY_DISCOVERIES.md`
- `research/WAVE_36_PHARMA_SUPPLY_METHODS.md`
- `research/WAVE_36_PHARMA_SUPPLY_SOURCE_NOTES.md`

W36P uses canonical IDs directly:
- edges W36P-E01 through W36P-E30
- methods W36P-M01 through W36P-M20
- sources W36P-D01 through W36P-D10


### W37O — Insider / beneficial-owner flow wave
Sources:
- `research/WAVE_37_OWNERSHIP_FLOW_DISCOVERIES.md`
- `research/WAVE_37_OWNERSHIP_FLOW_METHODS.md`
- `research/WAVE_37_OWNERSHIP_FLOW_SOURCE_NOTES.md`

W37O uses canonical IDs directly:
- edges W37O-E01 through W37O-E34
- methods W37O-M01 through W37O-M20
- sources W37O-D01 through W37O-D10


### W38O — OTC derivatives risk-transfer wave
Sources:
- `research/WAVE_38_OTC_DERIVATIVES_DISCOVERIES.md`
- `research/WAVE_38_OTC_DERIVATIVES_METHODS.md`
- `research/WAVE_38_OTC_DERIVATIVES_SOURCE_NOTES.md`

W38O uses canonical IDs directly:
- edges W38O-E01 through W38O-E34
- methods W38O-M01 through W38O-M20
- sources W38O-D01 through W38O-D10


### W39F — Fund fragility / fire-sale transmission wave
Sources:
- `research/WAVE_39_FUND_FRAGILITY_DISCOVERIES.md`
- `research/WAVE_39_FUND_FRAGILITY_METHODS.md`
- `research/WAVE_39_FUND_FRAGILITY_SOURCE_NOTES.md`

W39F uses canonical IDs directly:
- edges W39F-E01 through W39F-E34
- methods W39F-M01 through W39F-M20
- sources W39F-D01 through W39F-D10


### W40B — Border detention / import-release wave
Sources:
- `research/WAVE_40_BORDER_DETENTION_DISCOVERIES.md`
- `research/WAVE_40_BORDER_DETENTION_METHODS.md`
- `research/WAVE_40_BORDER_DETENTION_SOURCE_NOTES.md`

W40B uses canonical IDs directly:
- edges W40B-E01 through W40B-E34
- methods W40B-M01 through W40B-M20
- sources W40B-D01 through W40B-D10


### W41M — Deal completion / regulatory-clocks wave
Sources:
- `research/WAVE_41_DEAL_COMPLETION_DISCOVERIES.md`
- `research/WAVE_41_DEAL_COMPLETION_METHODS.md`
- `research/WAVE_41_DEAL_COMPLETION_SOURCE_NOTES.md`

W41M uses canonical IDs directly:
- edges W41M-E01 through W41M-E44
- methods W41M-M01 through W41M-M20
- sources W41M-D01 through W41M-D10


### W42G — Government procurement award / protest-state wave
Sources:
- `research/WAVE_42_GOVERNMENT_PROCUREMENT_DISCOVERIES.md`
- `research/WAVE_42_GOVERNMENT_PROCUREMENT_METHODS.md`
- `research/WAVE_42_GOVERNMENT_PROCUREMENT_SOURCE_NOTES.md`

W42G uses canonical IDs directly:
- edges W42G-E01 through W42G-E32
- methods W42G-M01 through W42G-M18
- sources W42G-D01 through W42G-D10


### W43B — Bank regulatory constraint / capital-state wave
Sources:
- `research/WAVE_43_BANK_REGULATORY_DISCOVERIES.md`
- `research/WAVE_43_BANK_REGULATORY_METHODS.md`
- `research/WAVE_43_BANK_REGULATORY_SOURCE_NOTES.md`

W43B uses canonical IDs directly:
- edges W43B-E01 through W43B-E32
- methods W43B-M01 through W43B-M18
- sources W43B-D01 through W43B-D10


### W44I — IP exclusion / import-access wave
Sources:
- `research/WAVE_44_IP_EXCLUSION_DISCOVERIES.md`
- `research/WAVE_44_IP_EXCLUSION_METHODS.md`
- `research/WAVE_44_IP_EXCLUSION_SOURCE_NOTES.md`

W44I uses canonical IDs directly:
- edges W44I-E01 through W44I-E32
- methods W44I-M01 through W44I-M18
- sources W44I-D01 through W44I-D10


### W45F — FDA review / market-entry clock wave
Sources:
- `research/WAVE_45_FDA_MARKET_ENTRY_DISCOVERIES.md`
- `research/WAVE_45_FDA_MARKET_ENTRY_METHODS.md`
- `research/WAVE_45_FDA_MARKET_ENTRY_SOURCE_NOTES.md`

W45F uses canonical IDs directly:
- edges W45F-E01 through W45F-E30
- methods W45F-M01 through W45F-M18
- sources W45F-D01 through W45F-D10


### W46U — Utility rate recovery / regulatory-economics wave
Sources:
- `research/WAVE_46_UTILITY_RATE_RECOVERY_DISCOVERIES.md`
- `research/WAVE_46_UTILITY_RATE_RECOVERY_METHODS.md`
- `research/WAVE_46_UTILITY_RATE_RECOVERY_SOURCE_NOTES.md`

W46U uses canonical IDs directly:
- edges W46U-E01 through W46U-E32
- methods W46U-M01 through W46U-M18
- sources W46U-D01 through W46U-D10


### W47S — Sanctions / export-control transaction-eligibility wave
Sources:
- `research/WAVE_47_SANCTIONS_EXPORT_CONTROL_DISCOVERIES.md`
- `research/WAVE_47_SANCTIONS_EXPORT_CONTROL_METHODS.md`
- `research/WAVE_47_SANCTIONS_EXPORT_CONTROL_SOURCE_NOTES.md`

W47S uses canonical IDs directly:
- edges W47S-E01 through W47S-E38
- methods W47S-M01 through W47S-M20
- sources W47S-D01 through W47S-D10


### W48A — Airworthiness / fleet-availability wave
Sources:
- `research/WAVE_48_AIRWORTHINESS_DISCOVERIES.md`
- `research/WAVE_48_AIRWORTHINESS_METHODS.md`
- `research/WAVE_48_AIRWORTHINESS_SOURCE_NOTES.md`

W48A uses canonical IDs directly:
- edges W48A-E01 through W48A-E35
- methods W48A-M01 through W48A-M20
- sources W48A-D01 through W48A-D10


### W49P — Physical inventory / delivery-pressure wave
Sources:
- `research/WAVE_49_PHYSICAL_DELIVERY_DISCOVERIES.md`
- `research/WAVE_49_PHYSICAL_DELIVERY_METHODS.md`
- `research/WAVE_49_PHYSICAL_DELIVERY_SOURCE_NOTES.md`

W49P uses canonical IDs directly:
- edges W49P-E01 through W49P-E40
- methods W49P-M01 through W49P-M20
- sources W49P-D01 through W49P-D10


### W50T — Trade-remedy / tariff-state wave
Sources:
- `research/WAVE_50_TRADE_REMEDY_DISCOVERIES.md`
- `research/WAVE_50_TRADE_REMEDY_METHODS.md`
- `research/WAVE_50_TRADE_REMEDY_SOURCE_NOTES.md`

W50T uses canonical IDs directly:
- edges W50T-E01 through W50T-E38
- methods W50T-M01 through W50T-M20
- sources W50T-D01 through W50T-D10


### W51B — Bankruptcy / court-controlled restructuring wave
Sources:
- `research/WAVE_51_BANKRUPTCY_RESTRUCTURING_DISCOVERIES.md`
- `research/WAVE_51_BANKRUPTCY_RESTRUCTURING_METHODS.md`
- `research/WAVE_51_BANKRUPTCY_RESTRUCTURING_SOURCE_NOTES.md`

W51B uses canonical IDs directly:
- edges W51B-E01 through W51B-E40
- methods W51B-M01 through W51B-M20
- sources W51B-D01 through W51B-D10


### W52P — Pipeline integrity enforcement / forced-capacity wave
Sources:
- `research/WAVE_52_PIPELINE_INTEGRITY_DISCOVERIES.md`
- `research/WAVE_52_PIPELINE_INTEGRITY_METHODS.md`
- `research/WAVE_52_PIPELINE_INTEGRITY_SOURCE_NOTES.md`

W52P uses canonical IDs directly:
- edges W52P-E01 through W52P-E36
- methods W52P-M01 through W52P-M20
- sources W52P-D01 through W52P-D10


### W53V — Vessel detention / maritime-eligibility wave
Sources:
- `research/WAVE_53_VESSEL_DETENTION_DISCOVERIES.md`
- `research/WAVE_53_VESSEL_DETENTION_METHODS.md`
- `research/WAVE_53_VESSEL_DETENTION_SOURCE_NOTES.md`

W53V uses canonical IDs directly:
- edges W53V-E01 through W53V-E34
- methods W53V-M01 through W53V-M20
- sources W53V-D01 through W53V-D10


### W54C — Medicare coverage / coding / reimbursement wave
Sources:
- `research/WAVE_54_MEDICARE_REIMBURSEMENT_DISCOVERIES.md`
- `research/WAVE_54_MEDICARE_REIMBURSEMENT_METHODS.md`
- `research/WAVE_54_MEDICARE_REIMBURSEMENT_SOURCE_NOTES.md`

W54C uses canonical IDs directly:
- edges W54C-E01 through W54C-E56
- methods W54C-M01 through W54C-M30
- sources W54C-D01 through W54C-D15


### W55T — Treasury financing / settlement-liquidity wave
Sources:
- `research/WAVE_55_TREASURY_FINANCING_DISCOVERIES.md`
- `research/WAVE_55_TREASURY_FINANCING_METHODS.md`
- `research/WAVE_55_TREASURY_FINANCING_SOURCE_NOTES.md`

W55T uses canonical IDs directly:
- edges W55T-E01 through W55T-E58
- methods W55T-M01 through W55T-M25
- sources W55T-D01 through W55T-D12


### W56G — Global bullion geography / fungibility wave
Sources:
- `research/WAVE_56_GLOBAL_BULLION_DISCOVERIES.md`
- `research/WAVE_56_GLOBAL_BULLION_METHODS.md`
- `research/WAVE_56_GLOBAL_BULLION_SOURCE_NOTES.md`

W56G uses canonical IDs directly:
- edges W56G-E01 through W56G-E58
- methods W56G-M01 through W56G-M30
- sources W56G-D01 through W56G-D15


### W57L — LNG commissioning / feedgas step-change wave
Sources:
- `research/WAVE_57_LNG_COMMISSIONING_DISCOVERIES.md`
- `research/WAVE_57_LNG_COMMISSIONING_METHODS.md`
- `research/WAVE_57_LNG_COMMISSIONING_SOURCE_NOTES.md`

W57L uses canonical IDs directly:
- edges W57L-E01 through W57L-E32
- methods W57L-M01 through W57L-M20
- sources W57L-D01 through W57L-D10


### W58A — Animal disease / biological capacity-loss wave
Sources:
- `research/WAVE_58_ANIMAL_DISEASE_DISCOVERIES.md`
- `research/WAVE_58_ANIMAL_DISEASE_METHODS.md`
- `research/WAVE_58_ANIMAL_DISEASE_SOURCE_NOTES.md`

W58A uses canonical IDs directly:
- edges W58A-E01 through W58A-E32
- methods W58A-M01 through W58A-M20
- sources W58A-D01 through W58A-D10


### W59P — Plant pest / quarantine / crop-capacity wave
Sources:
- `research/WAVE_59_PLANT_QUARANTINE_DISCOVERIES.md`
- `research/WAVE_59_PLANT_QUARANTINE_METHODS.md`
- `research/WAVE_59_PLANT_QUARANTINE_SOURCE_NOTES.md`

W59P uses canonical IDs directly:
- edges W59P-E01 through W59P-E25
- methods W59P-M01 through W59P-M20
- sources W59P-D01 through W59P-D10


### W60V — Vehicle defect / recall / production-spillover wave
Sources:
- `research/WAVE_60_VEHICLE_RECALL_DISCOVERIES.md`
- `research/WAVE_60_VEHICLE_RECALL_METHODS.md`
- `research/WAVE_60_VEHICLE_RECALL_SOURCE_NOTES.md`

W60V uses canonical IDs directly:
- edges W60V-E01 through W60V-E32
- methods W60V-M01 through W60V-M20
- sources W60V-D01 through W60V-D10


### W61F — Airspace flow / airport-capacity wave
Sources:
- `research/WAVE_61_AIRSPACE_FLOW_DISCOVERIES.md`
- `research/WAVE_61_AIRSPACE_FLOW_METHODS.md`
- `research/WAVE_61_AIRSPACE_FLOW_SOURCE_NOTES.md`

W61F uses canonical IDs directly:
- edges W61F-E01 through W61F-E29
- methods W61F-M01 through W61F-M20
- sources W61F-D01 through W61F-D10


### W62C — Futures positioning / crowding / concentration wave
Sources:
- `research/WAVE_62_CFTC_POSITIONING_DISCOVERIES.md`
- `research/WAVE_62_CFTC_POSITIONING_METHODS.md`
- `research/WAVE_62_CFTC_POSITIONING_SOURCE_NOTES.md`

W62C uses canonical IDs directly:
- edges W62C-E01 through W62C-E34
- methods W62C-M01 through W62C-M20
- sources W62C-D01 through W62C-D10


### W63M — Clearing margin / forced-deleveraging wave
Sources:
- `research/WAVE_63_CLEARING_MARGIN_DISCOVERIES.md`
- `research/WAVE_63_CLEARING_MARGIN_METHODS.md`
- `research/WAVE_63_CLEARING_MARGIN_SOURCE_NOTES.md`

W63M uses canonical IDs directly:
- edges W63M-E01 through W63M-E36
- methods W63M-M01 through W63M-M20
- sources W63M-D01 through W63M-D10


### W64F — Food safety enforcement / processing-capacity wave
Sources:
- `research/WAVE_64_FOOD_SAFETY_CAPACITY_DISCOVERIES.md`
- `research/WAVE_64_FOOD_SAFETY_CAPACITY_METHODS.md`
- `research/WAVE_64_FOOD_SAFETY_CAPACITY_SOURCE_NOTES.md`

W64F uses canonical IDs directly:
- edges W64F-E01 through W64F-E32
- methods W64F-M01 through W64F-M20
- sources W64F-D01 through W64F-D10


### W65D — Debt market access / refinancing-state wave
Sources:
- `research/WAVE_65_DEBT_MARKET_ACCESS_DISCOVERIES.md`
- `research/WAVE_65_DEBT_MARKET_ACCESS_METHODS.md`
- `research/WAVE_65_DEBT_MARKET_ACCESS_SOURCE_NOTES.md`

W65D uses canonical IDs directly:
- edges W65D-E01 through W65D-E36
- methods W65D-M01 through W65D-M20
- sources W65D-D01 through W65D-D10


### W66D — Medical device safety / recall / procedure-capacity wave
Sources:
- `research/WAVE_66_MEDICAL_DEVICE_SAFETY_DISCOVERIES.md`
- `research/WAVE_66_MEDICAL_DEVICE_SAFETY_METHODS.md`
- `research/WAVE_66_MEDICAL_DEVICE_SAFETY_SOURCE_NOTES.md`

W66D uses canonical IDs directly:
- edges W66D-E01 through W66D-E32
- methods W66D-M01 through W66D-M20
- sources W66D-D01 through W66D-D10


### W67N — Nuclear reactor operational / regulatory-state wave
Sources:
- `research/WAVE_67_NUCLEAR_REACTOR_STATE_DISCOVERIES.md`
- `research/WAVE_67_NUCLEAR_REACTOR_STATE_METHODS.md`
- `research/WAVE_67_NUCLEAR_REACTOR_STATE_SOURCE_NOTES.md`

W67N uses canonical IDs directly:
- edges W67N-E01 through W67N-E32
- methods W67N-M01 through W67N-M20
- sources W67N-D01 through W67N-D10
