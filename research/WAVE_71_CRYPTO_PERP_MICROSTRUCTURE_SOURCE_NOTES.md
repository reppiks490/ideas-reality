# Wave 71K — Source Notes

Namespace: **W71K**
Status key: VERIFIED = primary page/endpoint read in this wave (2026-10-11); PARTIAL = read in part or via search excerpt; PROVENANCE_PENDING = not read from a primary page.

## W71K-D01 — Hyperliquid Docs: Funding, Robust Price Indices, Liquidations, ADL, Margining, Margin Tiers, Contract Specs, Hyperps
Primary URLs: https://hyperliquid.gitbook.io/hyperliquid-docs/trading/funding ; .../trading/robust-price-indices ; .../trading/liquidations ; .../trading/auto-deleveraging ; .../trading/margining ; .../trading/margin-tiers ; .../trading/contract-specifications ; .../trading/hyperps
Owner: Hyperliquid (docs on GitBook). Cadence: static docs, edited without changelog (pages show "Last updated"). Revision behavior: silent edits; snapshot and hash. Rights: public docs. Status: VERIFIED (text read; formulas, weights, 150s EMA, 20%/30s partial liquidation, 2/3 backstop, ADL sort index, tiers quoted from page).

## W71K-D02 — Hyperliquid Info and WebSocket API
Primary URLs: https://hyperliquid.gitbook.io/hyperliquid-docs/for-developers/api/info-endpoint/perpetuals ; .../for-developers/api/websocket/subscriptions
Owner: Hyperliquid. Latency class: PUBLIC_REALTIME (block-clocked; oracle ~3s). Endpoints seen: perpDexs, meta, metaAndAssetCtxs, clearinghouseState, fundingHistory, predictedFundings (HlPerp/BinPerp/BybitPerp), perpsAtOpenInterestCap; subscriptions l2Book, trades, bbo, activeAssetCtx, userEvents (includes liquidation), userFundings, allDexsAssetCtxs, fastAssetCtxs. Rate limits not read. Status: VERIFIED for names; response numeric precision/units for premium/impactPxs: example JSON not read (PARTIAL).

## W71K-D03 — Hyperliquid Historical Data (S3)
Primary URL: https://hyperliquid.gitbook.io/hyperliquid-docs/historical-data
Owner: Hyperliquid. Cadence: approximately monthly; no timeliness guarantee; requester pays. Revision: possible gaps. Status: VERIFIED (doc read; bucket contents not listed).

## W71K-D04 — Binance Funding Rate FAQ
Primary URL: https://www.binance.com/en/support/faq/detail/360033525031
Owner: Binance. Status: VERIFIED (formula, clamp, 0.01% interest default, premium index, IMN = 200 USDT / IMR, caps/floors, interval switch dates 2025-05-02 and 2026-01-02). Revision: rules changed in the past; version. Rights: public help page.

## W71K-D05 — Binance USDS-M Futures API Docs (market data)
Primary URLs: https://developers.binance.com/docs/derivatives/usds-margined-futures/market-data/rest-api/Open-Interest-Statistics ; .../Basis ; .../Long-Short-Ratio ; .../websocket-market-streams/Liquidation-Order-Streams ; .../trade/rest-api/Position-ADL-Quantile-Estimation
Owner: Binance. Notes: OI statistics, basis and long/short endpoints verified (periods 5m-12h; 30 days / 1 month history; IP weight 0, 1000 req/5min); liquidation stream behaviour (1000ms, latest event per symbol) confirmed only via search summary; ADL quantile fields not read; direct fapi.binance.com calls from my environment returned a geo-restriction error (so no live payload check). Docs are a JS app; direct HTML fetch returned empty. Status: PARTIAL; liquidation stream payload and ADL fields PROVENANCE_PENDING.

## W71K-D06 — Bybit V5 API Docs
Primary URLs: https://bybit-exchange.github.io/docs/v5/websocket/public/all-liquidation ; .../websocket/public/ticker ; .../market/history-fund-rate ; .../market/long-short-ratio ; Bybit ADL help article https://www.bybit.com/en/help-center/article/Auto-Deleveraging-ADL
Owner: Bybit. Verified: allLiquidation (500ms, snapshot, fields T,s,S,v,p), ticker (100ms delta/snapshot, funding/OI/mark fields), funding history (limit 200, per-symbol interval), account-ratio (periods 5min-1d, since 2020-07-20). ADL help article: search excerpts only (8h drawdown trigger; isolated pool update cadence) — PARTIAL, PROVENANCE_PENDING for full text.

## W71K-D07 — OKX API v5 Docs
Primary URL: https://www.okx.com/docs-v5/en/ (sections Public Data: Get funding rate, Get premium history, Funding rate channel, Mark price channel, Open interest channel, Liquidation orders channel, ADL warning channel)
Owner: OKX. Verified from page text: funding fields (fundingRate, settFundingRate, settState, min/maxFundingRate, premium, impactValue, formulaType), premium history 6 months, liquidation channel is non-exhaustive and unordered, adl-warning pushes once per second only in warning/adl state with listed fields (several deprecated). Rate limit for funding-rate: 10 req / 2 s per IP+instrument. Status: VERIFIED. Revision: fields get deprecated.

## W71K-D08 — Deribit API Docs and Support
Primary URLs: https://docs.deribit.com/api-reference/market-data/public-ticker ; .../public-get_funding_rate_value ; .../public-get_volatility_index_data ; https://support.deribit.com/hc/en-us/articles/31424954847133-Inverse-Perpetual
Owner: Deribit. Verified: ticker fields current_funding, funding_8h, mark/index, open_interest; funding value history endpoints. Funding damper/cap values: search excerpt only (support page returned 403) — PARTIAL / PROVENANCE_PENDING.

## W71K-D09 — CME Group Crypto: Contract Specs, 24/7 Trading Notice, BRR
Primary URLs: https://www.cmegroup.com/markets/cryptocurrencies/bitcoin/bitcoin.contractSpecs.html (503 on fetch) ; https://cmegroupinc.gcs-web.com/node/55391/pdf (found via search; not read) ; https://cmegroup.com/trading/files/bitcoin-reference-rate-methodology.pdf ; https://www.cfbenchmarks.com/data/indices/BRR (read; methodology not stated on page) ; https://docs.cfbenchmarks.com/BRR-suitability-analysis.pdf
Owner: CME Group / CF Benchmarks. Status: PROVENANCE_PENDING for 24/7 effective date details (secondary news: live 2026-05-29) and for current price-limit/contract specs (2017-era filing details only). BRR window 15:00-16:00 London, 12 partitions: from search summary of older docs.

## W71K-D10 — Academic: Perpetual Futures Pricing
Primary URLs: https://arxiv.org/abs/2212.06888 (He, Manela, Ross, von Wachter, "Fundamentals of Perpetual Futures"); https://arxiv.org/abs/2310.11771 (Ackerer, Hugonnier, Jermann, "Perpetual Futures Pricing"; Mathematical Finance DOI 10.1111/mafi.70018; NBER w32936)
Cadence: static, versions. Status: PARTIAL (abstract-level facts via search; full text not read).

## W71K-D11 — Academic: Price Discovery in Cryptocurrency Markets
Primary URL: https://arxiv.org/abs/2506.08718 (Binance vs Uniswap v2 for ETH; BTC spot vs CME futures). Status: PARTIAL (abstract-level via search; tables unread).

## W71K-D12 — Oct 10-11, 2025 Cascade Evidence
URLs: https://www.researchsquare.com/article/rs-9459584/v1 (cited in search as "Anatomy of the Oct 10-11, 2025 Crypto Liquidation Cascade"); secondary: coinshares.com insight, coingecko.com/learn/october-10-crypto-crash-explained. Status: PROVENANCE_PENDING (not read; figures like ~$19B OI erased, Hyperliquid ADL are secondary and disputed).

## W71K-D13 — Coinversa Pulse (Third-Party Hyperliquid Analytics MCP)
Source: MCP server description (liquidation heatmap, backstop events, cohort bias, builder dexes). Owner: Coinversa. Rights: terms and tier limits unknown; data coverage and methodology not independently verified. Status: PROVENANCE_PENDING; use only to prototype, replace by primary node data.
