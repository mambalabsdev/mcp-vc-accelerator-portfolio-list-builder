# VC and Accelerator Portfolio List Builder MCP Server

[![Smithery](https://smithery.ai/badge/mambabuilt/mcp-vc-accelerator-portfolio-list-builder)](https://smithery.ai/servers/mambabuilt/mcp-vc-accelerator-portfolio-list-builder) [![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-vc-accelerator-portfolio-list-builder/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-vc-accelerator-portfolio-list-builder) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-vc-accelerator-portfolio-list-builder%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-vc-accelerator-portfolio-list-builder&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-vc-accelerator-portfolio-list-builder)](https://www.npmjs.com/package/@mambalabsdev/mcp-vc-accelerator-portfolio-list-builder) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-vc-accelerator-portfolio-list-builder)](https://www.npmjs.com/package/@mambalabsdev/mcp-vc-accelerator-portfolio-list-builder) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-vc-accelerator-portfolio-list-builder)](https://github.com/mambalabsdev/mcp-vc-accelerator-portfolio-list-builder/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-vc-accelerator-portfolio-list-builder)

An MCP server for the Mamba Labs VC and Accelerator Portfolio List Builder actor on Apify. Give it investors or accelerators by name, or portfolio page URLs, and get one row per portfolio company with its name, domain, website, description, and stage, batch, or status where the source gives it.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Y Combinator is read from its public company directory and can be filtered by batch, industry, region, status, and search words. Andreessen Horowitz (a16z), Sequoia Capital, Accel, Index Ventures, Founders Fund, Greylock, Lightspeed Venture Partners, Khosla Ventures, First Round Capital, Techstars, and Antler are built in, and any other portfolio page works by URL. Each source also returns one free summary row with the count and the way it was read, or the reason it returned nothing. Pages are read from the investor's own site and robots.txt is obeyed.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-vc-accelerator-portfolio-list-builder": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-vc-accelerator-portfolio-list-builder"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `build_portfolio_list` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "List the Y Combinator W25 companies in fintech with their websites."
- "Which companies are in Accel's and Greylock's portfolios?"
- "Pull the portfolio of https://example.vc/portfolio into a table."

## Tool

`build_portfolio_list`. One tool. Example arguments:

```json
{
  "investors": ["Y Combinator"],
  "yc_batches": ["W25"],
  "max_companies_per_source": 100
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `investors` | array | no | Built in names or portfolio page URLs, up to 25. Default Y Combinator. |
| `yc_batches` | array | no | Y Combinator batches, for example S24, W25. |
| `yc_industries` | array | no | Y Combinator industries. |
| `yc_regions` | array | no | Y Combinator regions. |
| `yc_status` | array | no | active, acquired, public, inactive. |
| `yc_query` | string | no | Words to search the Y Combinator directory for. |
| `max_companies_per_source` | integer | no | Company rows per source. Default 500. |
| `open_company_pages` | boolean | no | Open per company pages when needed. Default true. |
| `max_detail_pages` | integer | no | Company pages opened per source. Default 200. |
| `only_new` | boolean | no | Skip companies an earlier run returned. Default false. |
| `state_key` | string | no | Name for the only new companies memory. |
| `max_charge_usd` | string | no | Optional cost cap for the run. |
| `proxy_mode` | string | no | auto or direct. Default auto. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `company-row`, per portfolio company with a domain | $0.007 | $0.00665 | $0.0063 | $0.00595 |
| `apify-actor-start`, per run start | $0.0025 | $0.0025 | $0.0025 | $0.0025 |

Rows with no domain, source summary rows, and already delivered companies are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/vc-accelerator-portfolio-list-builder](https://apify.com/mambalabs/vc-accelerator-portfolio-list-builder)

## License

MIT. See [LICENSE](LICENSE).
