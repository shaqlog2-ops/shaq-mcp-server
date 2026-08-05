# SHAQ Logistics MCP Server

> Search 160,000+ freight rates, create bookings, and track shipments from China shipping ports — directly in Claude, Cursor, or any MCP-compatible AI client.

[![CI](https://github.com/shaqlog2-ops/shaq-mcp-server/actions/workflows/ci.yml/badge.svg)](https://github.com/shaqlog2-ops/shaq-mcp-server/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![MCP Compatible](https://img.shields.io/badge/MCP-compatible-blue.svg)](https://modelcontextprotocol.io)
[![Live](https://img.shields.io/endpoint?url=https://search.shaq-logistics.com/api/health&style=flat)](https://search.shaq-logistics.com)

## 🚢 Overview

**SHAQ Logistics MCP Server** connects AI assistants to real-time international shipping freight rate data. It is the first Model Context Protocol server dedicated to international freight logistics, providing access to LCL (Less than Container Load) and FCL (Full Container Load) pricing from major Chinese ports to destinations worldwide.

### Why use this MCP server?

- 📊 **160,000+ live rate entries** — updated hourly from carrier feeds
- 🌏 **15+ Chinese origins** — Shenzhen (YANTIAN/SHEKOU), Ningbo, Shanghai, Qingdao, Guangzhou, and more
- 🌍 **200+ destinations** — US, Europe, Southeast Asia, Middle East, Latin America, Africa
- 📦 **All container types** — 20GP, 40GP, 40HQ, 45HQ for FCL; per CBM/TON for LCL
- 🤖 **No API key needed** — public SSE endpoint, plug-and-play with any MCP client
- 🔒 **Privacy by design** — carrier names are not exposed; bookings are quarantined for review

### Live Endpoint

```
SSE: https://search.shaq-logistics.com/sse
```

No authentication required. The server is publicly accessible.

## 🛠️ Tools

The MCP server exposes six tools:

| Tool | Description | Required inputs |
|---|---|---|
| `search_freight_rates` | Search real-time LCL/FCL freight rates | `origin`, `destination` |
| `create_booking` | Create a freight booking | `contact_name/phone/email`, `supplier_name/phone/email`, `po_number` |
| `track_booking` | Track shipment status | `booking_number` |
| `list_ports` | List all supported ports + aliases | none |
| `get_freight_index` | Get freight market trends | optional `route`, `period` |
| `subscribe_rate_alert` | Subscribe to rate change alerts | `origin`, `destination`, `email` |

### 1. `search_freight_rates`

Search real-time freight rates for LCL and FCL shipments.

**Input Schema:**
```json
{
  "origin": "Shenzhen",
  "destination": "Los Angeles",
  "shipment_type": "FCL",
  "container_type": "40GP"
}
```

**Returns:** Carrier rates, transit times, validity dates, and booking references.

---

### 2. `create_booking`

Create a freight booking with supplier and contact details.

**Required fields:**
- `contact_name`, `contact_phone`, `contact_email` (customer)
- `supplier_name`, `supplier_phone`, `supplier_email` (supplier)
- `po_number` (purchase order)

**Returns:** Booking reference and status (`pending_review` by default).

---

### 3. `track_booking`

Track shipment status by booking number.

**Input:** `booking_number`

**Returns:** Current status, location history, ETA, and carrier tracking details.

---

### 4. `list_ports`

List all supported shipping ports with aliases.

**Returns:** Port codes, names, country, region, and alias mappings (e.g., YANTIAN/SHEKOU → Shenzhen).

---

### 5. `get_freight_index`

Get freight market index trends and statistics.

**Input:** `route` (optional), `period` (optional)

**Returns:** Price trends, market averages, and volatility indicators.

---

### 6. `subscribe_rate_alert`

Subscribe to rate change alerts for specific routes.

**Input:** `origin`, `destination`, `email`, `threshold` (optional)

**Returns:** Subscription confirmation and alert preferences.

## 📦 Installation

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

## 💡 Example Usage

Once connected, ask your AI assistant natural-language questions:

- "What's the current FCL rate from Shenzhen to Los Angeles for a 40GP container?"
- "Find LCL rates from Ningbo to Hamburg under $80/CBM"
- "Create a booking for shipping from Shanghai to Rotterdam, contact Aaron, PO#20260805"
- "Track booking SHAQ20260804001"
- "What ports are available in China for export?"
- "Show me the freight index trend for the China-US route over the last 30 days"
- "Subscribe me to rate alerts for Shenzhen → Long Beach, email alerts when prices move >5%"

## 🌏 Coverage

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

## 🔗 Links

- **Platform:** [search.shaq-logistics.com](https://search.shaq-logistics.com)
- **API Docs (OpenAPI 3.0):** [search.shaq-logistics.com/openapi.json](https://search.shaq-logistics.com/openapi.json)
- **AI Crawler Guide:** [search.shaq-logistics.com/llms.txt](https://search.shaq-logistics.com/llms.txt)
- **Detailed AI Guide:** [search.shaq-logistics.com/llms-full.txt](https://search.shaq-logistics.com/llms-full.txt)
- **Schema.org Structured Data:** [search.shaq-logistics.com/structured-data.jsonld](https://search.shaq-logistics.com/structured-data.jsonld)
- **MCP Tutorial (Gist):** [gist.github.com/shaqlog2-ops/cbce468eb56fe69ecc76bf94d9253e78](https://gist.github.com/shaqlog2-ops/cbce468eb56fe69ecc76bf94d9253e78)

## 🏗️ Architecture

```
┌────────────────┐     SSE/HTTP      ┌──────────────────────────┐
│  MCP Client    │ ◄────────────────► │  SHAQ MCP Server         │
│  (Claude,      │   JSON-RPC 2.0     │  (FastAPI + SSE)         │
│   Cursor,      │                    │                          │
│   Continue)    │                    │  • search_freight_rates  │
└────────────────┘                    │  • create_booking        │
                                      │  • track_booking         │
                                      │  • list_ports            │
                                      │  • get_freight_index     │
                                      │  • subscribe_rate_alert  │
                                      └────────────┬─────────────┘
                                                   │
                                      ┌────────────▼─────────────┐
                                      │  SHAQ Data Layer         │
                                      │  • 160K+ carrier rates   │
                                      │  • LCL rates (per CBM)   │
                                      │  • Port aliases          │
                                      │  • Booking system        │
                                      └──────────────────────────┘
```

- **Backend:** Python + FastAPI + SSE transport
- **Server:** Gunicorn (8 workers) + nginx reverse proxy
- **Data:** SQLite (160K+ carrier rates, 287 LCL rates)
- **Deployment:** Tencent Cloud (43.129.193.124)

## 🤝 Contributing

Contributions are welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

Ways to contribute:
- 🐛 [Report bugs](https://github.com/shaqlog2-ops/shaq-mcp-server/issues/new?template=bug_report.md)
- 💡 [Suggest features](https://github.com/shaqlog2-ops/shaq-mcp-server/issues/new?template=feature_request.md)
- 🚢 [Request new ports/routes](https://github.com/shaqlog2-ops/shaq-mcp-server/issues/new?template=port_request.md)
- 💬 [Join discussions](https://github.com/shaqlog2-ops/shaq-mcp-server/discussions)
- 🔧 [Submit pull requests](https://github.com/shaqlog2-ops/shaq-mcp-server/compare)

## 📊 Roadmap

- [x] LCL + FCL rate search
- [x] Booking creation + tracking
- [x] Rate change alerts
- [x] MCP SSE endpoint (public, no auth)
- [x] OpenAPI 3.0 spec + llms.txt for AI discovery
- [ ] Air freight rates
- [ ] Rail freight (China-Europe Railway Express)
- [ ] Customs document lookup
- [ ] Multi-language port aliases (zh, es, fr, de, ar)
- [ ] Real-time container tracking (AIS integration)
- [ ] Rate prediction model (ML-based)

See [CHANGELOG.md](CHANGELOG.md) for release history.

## 📄 License

MIT License — see [LICENSE](LICENSE).

## 🏢 About SHAQ Logistics

[SHAQ Logistics](https://search.shaq-logistics.com) is a logistics technology company building the freight rate intelligence layer for AI assistants. We aggregate carrier rate sheets, normalize port mappings, and expose clean MCP tools so any AI agent can quote shipping rates, create bookings, and track shipments in natural language.

**Contact:** ayang@shaq-log.com  
**WhatsApp:** +86 15818505125

---

**If this MCP server is useful, please ⭐ star this repository — it helps others discover it.**
