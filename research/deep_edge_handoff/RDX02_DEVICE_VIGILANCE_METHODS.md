# RDX02 — Methods

1. Use FDA received/public date, not clinical event date, for historical availability.
2. MAUDE reports are signals/complaints, not proof of device causality.
3. Normalize event count by exposure/install-base proxy and product age.
4. Detect duplicate/supplemental MDRs and link them to parent events.
5. Version device names, UDI-DI, product codes, PMA/510(k) and manufacturer identity.
6. Preserve reporter type; manufacturer and user-facility reports are not independent by default.
7. Separate 5-day remedial-action MDRs from ordinary 30-day MDRs where report semantics support it.
8. Archive weekly openFDA/MAUDE vintages; do not backfill later corrections.
9. Treat Early Alert publication and confirmed recall classification as separate clocks.
10. Treat correction/removal initiation, 806 filing and FDA classification as separate clocks.
11. Use exact product/lot/serial scope; never map whole manufacturer from one recall without evidence.
12. Distinguish software, field correction, device replacement and market withdrawal.
13. Shortage-list updates are point-in-time revisions; archive every published state.
14. Discontinuance is not necessarily shortage; model substitution capacity.
15. Map clinical capacity only when device-to-procedure dependence is sourced.
16. Avoid double-counting component recalls appearing inside kits and finished devices.
17. FDA recall database update cadence differs from MAUDE/openFDA; source clocks remain separate.
18. Warning letters are delayed enforcement evidence, not an early trigger unless publication precedes outcome.
19. Use negative controls with unrelated product codes/manufacturers and lag permutations.
20. Before market alpha require OOS prediction of recall/correction, classification, scope expansion, remedy delay, shortage, clinical capacity loss or quantifiable cost.
