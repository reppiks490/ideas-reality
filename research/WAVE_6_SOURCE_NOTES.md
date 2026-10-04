# Wave 6 Source Notes

## GitHub
Official:
https://docs.github.com/en/rest/activity/events
https://docs.github.com/en/rest/metrics/statistics

Public event endpoints have limited history and variable latency. Repository traffic views/clones are available only with write access and are not valid external public-company signals for arbitrary repos.

## PyPI
Official packaging guide:
https://packaging.python.org/en/latest/guides/analyzing-pypi-package-downloads/

The public BigQuery dataset records timestamped downloads. Historical caveats and automated-download contamination must be handled.

## Hugging Face
Official:
https://huggingface.co/docs/hub/api

Hub APIs expose downloads, likes, modified times, trending score and related metadata, subject to rate limits.

## Steam
Official Steamworks:
https://partner.steamgames.com/doc/webapi/ISteamUserStats

GetNumberOfCurrentPlayers exposes current connected player count by app. Historical archive must be built prospectively unless a licensed/history source is used.

## DOE Strategic Petroleum Reserve
Official:
https://www.spr.doe.gov/

Solicitations and contracts can include target quantity, quality, delivery windows and later awards/exchange terms.

## EIA Petroleum
Official:
https://www.eia.gov/petroleum/supply/weekly

Weekly Petroleum Status Report includes SPR inventory and broader crude/product balances.

## FINRA TRACE
Official:
https://www.finra.org/finra-data/fixed-income/about-trade-activity
https://www.finra.org/finra-data/fixed-income/corp-and-agency/trade

FINRA states eligible corporate/agency and several securitized transactions are publicly disseminated with execution time, quantity, price and yield. Corporate/agency reporting generally has a 15-minute requirement; many reports arrive faster. Size caps and late/as-of reports require careful handling.

## MSRB / Municipal
Official:
https://www.msrb.org/
https://emma.msrb.org/

Real-time/subscription data rights and public delayed/free access must be reviewed before production. Do not assume all municipal transaction feeds have the same licensing.

## USDA AMS
Official:
https://mymarketnews.ams.usda.gov/viewReport/3208

Daily Livestock and Poultry Slaughter reports provide high-frequency physical throughput estimates. Preserve initial estimates and revisions.

## EIA Natural Gas
Official:
https://www.eia.gov/naturalgas/
https://www.eia.gov/opendata/

Use component-specific publication timing. Do not mix monthly production series with weekly/daily proxies as if contemporaneous.

## Important boundaries

- GitHub views/clones are not generally public for arbitrary third-party repos.
- GitHub public events can lag and have limited history.
- package downloads are not equivalent to humans or paid users.
- Hugging Face downloads are not equivalent to inference revenue.
- Steam current players require prospective history for clean backtests unless licensed history is obtained.
- TRACE public size fields can be capped/censored.
- municipal data licensing/access must be encoded.
- government commodity headline volume must be converted to actual delivery flow.
