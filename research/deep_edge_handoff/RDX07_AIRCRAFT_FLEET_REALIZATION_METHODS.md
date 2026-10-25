# RDX07 — Methods

1. FAA downloadable registry refreshes daily, but final processing can lag; source refresh is not underlying event latency.
2. Use Document Index receipt date as the early public document clock, not final master processing date.
3. Document Index includes many document types; classify registration/ownership events before interpreting.
4. N-number alone is not permanent aircraft identity; use manufacturer serial number.
5. Owner, lessor, trustee and operator are separate entities.
6. Valid registration is not always entry into commercial service.
7. For previously U.S.-registered aircraft, temporary authority can exist while registration is pending; for imported/newly unregistered aircraft, airworthiness/registration rules differ.
8. Archive daily FAA database vintages prospectively if used for event timing.
9. Respect FAA privacy-withholding changes for owner information; missing owner is not missing aircraft.
10. Deduplicate N-number changes and administrative renewals.
11. Separate new OEM deliveries from used imports/lessor transfers.
12. Deregistration for export is not an OEM delivery.
13. Map aircraft model/serial to OEM program and customer with sourced confidence.
14. Validate fleet entry with actual commercial operation/schedule data where lawful.
15. Adjust delivery counts for business-day registry update cadence.
16. Model document processing lag as censoring, not as delivery delay.
17. Use point-in-time OEM backlog/guidance for expectation.
18. Quarter-end event studies control known delivery seasonality.
19. Security agreement/lien records require separate financing semantics.
20. Before market alpha require OOS prediction of delivery, entry into service, fleet capacity, guidance miss/beat or utilization.
