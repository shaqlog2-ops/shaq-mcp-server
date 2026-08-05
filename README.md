# SHAQ Logistics MCP Server

> Search 160,000+ freight rates, create bookings, and track shipments from China shipping ports — directly in Claude, Cursor, or any MCP-compatible AI client.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![MCP Compatible](https://img.shields.io/badge/MCP-compatible-blue.svg)](https://modelcontextprotocol.io)
[![Live](https://img.shields.io/endpoint?url=https://search.shaq-logistics.com/api/health&style=flat)](https://search.shaq-logistics.com)

## Overview

**SHAQ Logistics MCP Server** connects AI assistants to real-time international shipping freight rate data. It is the first Model Context Protocol server dedicated to international freight logistics, providing access to LCL (Less than Container Load) and FCL (Full Container Load) pricing from major Chinese ports to destinations worldwide.

### Why use this MCP server?

- **160,000+ live rate entries** — continuously updated
- **15+ Chinese origins** — Shenzhen, Ningbo, Shanghai, Qingdao, Guangzhou, and more
- **200+ destinations** — US, Europe, Southeast Asia, Middle East, Latin America, Africa
- **All container types** — 20GP, 40GP, 40HQ, 45HQ for FCL; per CBM/TON for LCL
- **No API key needed** — public SSE endpoint, plug-and-play with any MCP client
- **Bookings are quarantined for review** before confirmation

### Live Endpoint

```
SSE: https://search.shaq-logistics.com/sse
```

No authentication required. The server is publicly accessible.

## Tools

The MCP server exposes nine tools:

| Tool | Description | Required inputs |
|---|---|---|
| `search_freight_rates` | Search real-time LCL/FCL freight rates | `origin`, `destination` |
| `create_booking` | Create a freight booking | `contact_name/phone/email`, `supplier_name/phone/email`, `po_number` |
| `track_booking` | Track shipment status | `booking_number` |
| `list_ports` | List all supported ports + aliases | none |
| `get_freight_index` | Get freight market trends | optional `route`, `period` |
| `subscribe_rate_alert` | Subscribe to rate change alerts | `origin`, `destination`, `email` |
| `get_sailing_schedule` | Get vessel sailing schedules | `origin`, `destination` |
| `get_port_fees` | Get port fee types | `port` |
| `get_customs_info` | Get customs compliance info | `country` |

## Installation

### Claude Desktop

Add to `claude_desktop_config.json` (macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`, Windows: `%APPDATA%\Claude\claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "shaq-logistics": {
      "url": "https://search.shaq-logistics.com/sse"
    }
  }
}
```

### Cursor

Add to `.cursor/mcp.json` in your project root:

```json
{
  "mcpServers": {
    "shaq-logistics": {
      "url": "https://search.shaq-logistics.com/sse"
    }
  }
}
```

### Continue.dev

Add to `~/.continue/config.json`:

```json
{
  "mcpServers": {
    "shaq-logistics": {
      "url": "https://search.shaq-logistics.com/sse"
    }
  }
}
```

### Any MCP Client

Use the SSE endpoint: `https://search.shaq-logistics.com/sse`

The server follows the [Model Context Protocol](https://modelcontextprotocol.io) specification and works with any compliant client.

## Example Usage

Once connected, ask your AI assistant natural-language questions:

- "What's the current FCL rate from Shenzhen to Los Angeles for a 40GP container?"
- "Find LCL rates from Ningbo to Hamburg under $80/CBM"
- "Create a booking for shipping from Shanghai to Rotterdam, contact Aaron, PO#20260805"
- "Track booking SHAQ20260804001"
- "What ports are available in China for export?"
- "Show me the freight index trend for the China-US route over the last 30 days"
- "Subscribe me to rate alerts for Shenzhen to Long Beach, email alerts when prices move >5%"
- "What's the next sailing from Shenzhen to Sydney?"
- "What are the port fees at Shanghai?"
- "What customs documents do I need for imports to Australia?"

## Coverage

### Origins (China)
- Shenzhen (YANTIAN, SHEKOU)
- Ningbo
- Shanghai
- Qingdao
- Guangzhou
- Tianjin
- Xiamen
- Dalian
- And more

### Destinations (200+ worldwide)
- **North America:** Los Angeles, Long Beach, New York, Vancouver, Tacoma
- **Europe:** Rotterdam, Hamburg, Antwerp, Felixstowe, Le Havre, Genoa
- **Southeast Asia:** Singapore, Ho Chi Minh City, Manila, Bangkok, Port Klang
- **Middle East:** Jebel Ali (Dubai), Dammam, Jeddah
- **Latin America:** Manzanillo, Santos, Buenos Aires, Callao
- **Africa:** Durban, Mombasa, Alexandria
- **Oceania:** Sydney, Melbourne, Auckland

### Rate Types
- **LCL (Less than Container Load):** per CBM or per TON, whichever is greater
- **FCL (Full Container Load):** 20GP, 40GP, 40HQ, 45HQ

## Links

- **Platform:** [search.shaq-logistics.com](https://search.shaq-logistics.com)
- **MCP Guide:** [search.shaq-logistics.com/mcp-guide](https://search.shaq-logistics.com/mcp-guide)
- **API Docs (OpenAPI 3.0):** [search.shaq-logistics.com/openapi.json](https://search.shaq-logistics.com/openapi.json)
- **AI Crawler Guide:** [search.shaq-logistics.com/llms.txt](https://search.shaq-logistics.com/llms.txt)

## Roadmap

- [x] LCL + FCL rate search
- [x] Booking creation + tracking
- [x] Rate change alerts
- [x] Sailing schedules
- [x] Port fee lookup
- [x] Customs compliance info
- [ ] Air freight rates
- [ ] Rail freight (China-Europe Railway Express)
- [ ] Real-time container tracking (AIS integration)

See [CHANGELOG.md](CHANGELOG.md) for release history.

## License

MIT License — see [LICENSE](LICENSE).

## About SHAQ Logistics

[SHAQ Logistics](https://search.shaq-logistics.com) is a logistics technology company building the freight rate intelligence layer for AI assistants.

**Contact:** ayang@shaq-log.com
**WhatsApp:** +86 15818505125

---

**If this MCP server is useful, please star this repository — it helps others discover it.**
