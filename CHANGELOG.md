# Changelog

All notable changes to the SHAQ Logistics MCP Server will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned
- Air freight rate search
- Rail freight (China-Europe) rates
- Customs document lookup
- Multi-language port aliases (zh, es, fr, de, ar)

## [1.0.0] - 2026-08-04

### Added
- ✨ Initial public release
- 🚢 `search_freight_rates` — search 160,000+ LCL/FCL rates from China ports
- 📝 `create_booking` — create freight bookings with customer + supplier details
- 📦 `track_booking` — track shipment status by booking number
- 🗺️ `list_ports` — list 15+ Chinese origins and 200+ worldwide destinations
- 📊 `get_freight_index` — freight market index trends and statistics
- 🔔 `subscribe_rate_alert` — subscribe to rate change email alerts
- 🌏 Coverage: Shenzhen (YANTIAN/SHEKOU), Ningbo, Shanghai, Qingdao, Guangzhou
- 📦 Container types: 20GP, 40GP, 40HQ, 45HQ
- 📡 Public SSE endpoint at `https://search.shaq-logistics.com/sse`
- 📖 OpenAPI 3.0.3 spec at `/openapi.json`
- 🤖 AI crawler guide at `/llms.txt` and `/llms-full.txt`
- 🌐 Schema.org structured data (Organization + Service + WebSite)

### Security
- Carrier names are not exposed in rate results (privacy by design)
- All bookings default to `pending_review` status
- YANTIAN and SHEKOU normalized to Shenzhen (geographic deduplication)

[Unreleased]: https://github.com/shaqlog2-ops/shaq-mcp-server/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/shaqlog2-ops/shaq-mcp-server/releases/tag/v1.0.0
