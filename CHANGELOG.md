# Changelog

All notable changes to the SHAQ Logistics MCP Server will be documented in this file.

## [Unreleased]

### Planned
- Air freight rate search
- Rail freight (China-Europe) rates
- Real-time container tracking (AIS integration)

## [1.2.0] - 2026-08-06

### Added
- `get_sailing_schedule` — query vessel sailing schedules
- `get_port_fees` — look up port fee types
- `get_customs_info` — get customs compliance information by country

## [1.1.0] - 2026-08-05

### Added
- Booking PIN verification for `create_booking`
- Global rate limiting (60 requests/minute)
- Rate result watermarking

## [1.0.0] - 2026-08-04

### Added
- `search_freight_rates` — search 160,000+ LCL/FCL rates from China ports
- `create_booking` — create freight bookings with customer + supplier details
- `track_booking` — track shipment status by booking number
- `list_ports` — list 15+ Chinese origins and 200+ worldwide destinations
- `get_freight_index` — freight market index trends and statistics
- `subscribe_rate_alert` — subscribe to rate change email alerts
- Public SSE endpoint at `https://search.shaq-logistics.com/sse`
- OpenAPI 3.0.3 spec at `/openapi.json`
- AI crawler guide at `/llms.txt` and `/llms-full.txt`
