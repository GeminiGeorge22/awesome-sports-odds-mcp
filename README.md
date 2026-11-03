# Awesome Sports Odds MCP [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated, all-in-one list of the best MCP servers for sports betting odds: one entry per sportsbook, book network, exchange, or aggregator.

[Model Context Protocol (MCP)](https://modelcontextprotocol.io) servers let AI assistants such as Claude, Cursor, VS Code and ChatGPT pull live odds, player props, line movement and prediction-market prices as tools. This list is deliberately short. Every entry is a real MCP server or hosted MCP endpoint, was checked on the day it was added, and is the single strongest option for its data source. If two servers cover the same book or the same aggregator, only the better one is listed.

**Other languages:**
- Español: lista seleccionada de servidores MCP de cuotas deportivas, un proveedor por casa de apuestas.
- 简体中文：精选体育赔率 MCP 服务器列表，每个博彩公司只收录一个提供方。
- Русский: подборка MCP-серверов спортивных коэффициентов — один провайдер на каждого букмекера.
- 日本語：スポーツオッズ MCP サーバーの厳選リスト。ブックメーカーごとに提供元は 1 つだけ。

## Contents

- [Multi-book odds aggregators](#multi-book-odds-aggregators)
- [Sportsbook networks and single books](#sportsbook-networks-and-single-books)
- [Regional bookmakers](#regional-bookmakers)
- [Prediction markets and exchanges](#prediction-markets-and-exchanges)
- [Documentation MCPs for builders](#documentation-mcps-for-builders)
- [How to connect](#how-to-connect)
- [Contributing](#contributing)
- [License](#license)

## Multi-book odds aggregators

One entry per aggregator. Each one normalizes many books into a single schema.

| Name | Type | Coverage | Description |
|---|---|---|---|
| [OpticOdds MCP](https://developer.opticodds.com/docs/opticodds-mcp-integration-guide) | Official, hosted | US and global sportsbooks; odds, player props, futures, injuries, results, line history | Hosted MCP endpoint for real-time odds with best-price, outlier and cross-book line comparison tools. |
| [Odds-API.io MCP Server](https://github.com/odds-api-io/odds-api-mcp-server) | Official, open source | Global bookmakers across many sports; historical odds, value bets, arbitrage, dropping odds, settlement | Official MCP server giving Claude, Cursor and VS Code direct access to the Odds-API.io v3 surface. |
| [SportsGameOdds MCP Server](https://github.com/SportsGameOdds/sports-odds-api-typescript/tree/main/packages/mcp-server) | Official, npm | US sportsbooks; live game odds and sportsbook data | Official MCP server for the Sports Game Odds API, run with `npx sports-odds-api-mcp`. |
| [TheRundown Data MCP](https://github.com/TheRundown/data-mcp) | Official, hosted + open source | US books, exchanges and prediction markets; main lines, futures, events, scores | Official read-only MCP for TheRundown's Product API, hosted at `mcp.therundown.io`. |
| [PropLine MCP](https://github.com/proplineapi/propline-mcp) | Official, hosted + npm | Player props across books and DFS apps; +EV, prop resolution, scores, box scores | MCP server for the PropLine player-props odds API, listed in the official MCP Registry. |
| [Sports Betting Stats MCP](https://github.com/GeminiGeorge22/sports-betting-stats-mcp) (maintained by us) | Hosted on Apify + open-source stdio proxy | Kambi books, DraftKings, Pinnacle and Bovada odds; PrizePicks props; ESPN scores; Understat xG; soccer closing lines; Equibase racing; Polymarket vs Kalshi | One endpoint that bundles odds, props, scores, advanced stats and historical closing lines from independent Apify Actors, one per job. |

## Sportsbook networks and single books

One entry per book or book network.

| Name | Type | Coverage | Description |
|---|---|---|---|
| [Sports Odds API MCP](https://github.com/GeminiGeorge22/sports-odds-mcp) (maintained by us) | Hosted on Apify | Kambi network: BetRivers, Unibet, Paf, Svenska Spel, ATG | Live odds from Kambi-powered sportsbooks in one call: one row per game with every book's price and the best price per outcome. |
| [PinnWire](https://pinnwire.com) | Official, hosted | Pinnacle; live and prematch odds, price drops | Read-only hosted MCP for current Pinnacle odds and recent price drops. |
| [OddiWire](https://oddiwire.com) | Official, hosted | ODDIN.GG esports odds: League of Legends, CS2, Dota 2, Valorant and more | Hosted MCP endpoint for esports odds from ODDIN.GG on the same key as the REST API. |

## Regional bookmakers

| Name | Type | Coverage | Description |
|---|---|---|---|
| [PuntersEdge](https://puntersedge.online/api) | Official, hosted + PyPI | Australian bookmakers; AU/NZ racing odds and Australian sports odds | Official MCP server with per-bookmaker prices, the change feed, results, form and a closing-line archive. |

## Prediction markets and exchanges

| Name | Type | Coverage | Description |
|---|---|---|---|
| [Polymarket MCP Server](https://github.com/caiovicentino/polymarket-mcp-server) | Community, open source | Polymarket markets, prices, order books, positions | MCP server for analysing and trading Polymarket prediction markets, with real-time WebSocket monitoring and safety controls. |
| [kalshi-mcp-server](https://github.com/cejor6/kalshi-mcp-server) | Community, open source | Kalshi markets over REST and WebSocket | Self-hosted MCP server for Kalshi with native RSA-PSS auth, rate limiting and a prepare/confirm order flow, listed in the official MCP Registry. |

## Documentation MCPs for builders

These return documentation and API schemas, not live prices. Use them while writing an integration.

| Name | Type | Coverage | Description |
|---|---|---|---|
| [Sportradar MCP Server](https://developer.sportradar.com/getting-started/docs/mcp-server) | Official, docs-only | Sportradar APIs including the Odds Comparison, Probabilities and Betting Splits APIs | Gives AI code editors access to Sportradar API docs, endpoint listings and schemas. |
| [OddsPapi Docs MCP](https://docs.oddspapi.io) | Official, docs-only | OddsPapi API: sharps, soft books, exchanges and prediction markets | Hosted docs MCP so an agent can read the OddsPapi docs and OpenAPI spec and write the REST and WebSocket calls. |

## How to connect

Most entries here are remote (Streamable HTTP) MCP servers. Add the URL to your client; the provider's page says whether it wants an API key header or OAuth.

**Claude Code**

```sh
claude mcp add --transport http sports-odds "https://mcp.apify.com?tools=publicrecords/sports-odds-api"
```

**Cursor** (`~/.cursor/mcp.json`) or **VS Code** (`.vscode/mcp.json`, use `"servers"` and add `"type": "http"`)

```json
{
  "mcpServers": {
    "sports-odds": {
      "url": "https://mcp.apify.com?tools=publicrecords/sports-odds-api"
    },
    "pinnacle": {
      "url": "https://pinnwire.com/mcp"
    }
  }
}
```

Swap in any other entry's endpoint from its own docs. Local servers run with `npx` or `uvx` as shown in each README.

## Contributing

Pull requests are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) first. The key rule is **one provider per sportsbook**: a new entry must cover a book, book network, exchange or aggregator that is not already listed, or be clearly better than the current entry for it (in which case the PR replaces it).

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the contributors have waived all copyright and related rights to this list. See [LICENSE](LICENSE).

---

Disclosure: entries marked "(maintained by us)" are ours. Everything else is independent and is listed on merit. This list provides odds data sources only; nothing here accepts bets on your behalf unless its own docs say so. Follow the laws where you live.
