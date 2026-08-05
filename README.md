# SHAQ Logistics MCP Server

> Search 160,000+ freight rates, create bookings, and track shipments from China shipping ports - directly in Claude, Cursor, or any MCP-compatible client.

## Overview

SHAQ Logistics MCP Server connects AI assistants to real-time international shipping freight rate data. It provides access to LCL (Less than Container Load) and FCL (Full Container Load) pricing from major Chinese ports including Shenzhen (YANTIAN/SHEKOU), Ningbo, Shanghai, and Qingdao to destinations worldwide.

### Live Endpoint

```
SSE: https://search.shaq-logistics.com/sse
```

No authentication required - the server is publicly accessible.

## Tools

### 1. search_freight_rates

Search real-time freight rates for LCL and FCL shipments.

Input: origin, destination, shipment_type (LCL/FCL), container_type (20GP/40GP/40HQ/45HQ)

Returns: Carrier rates, transit times, validity dates, and booking references.

### 2. create_booking

Create a freight booking with supplier and contact details.

Required: contact_name, contact_phone, contact_email, supplier_name, supplier_phone, supplier_email, po_number

Returns: Booking reference and status (pending_review by default).

### 3. track_booking

Track shipment status by booking number.

Input: booking_number

Returns: Current status, location history, ETA, and carrier tracking details.

### 4. list_ports

List all supported shipping ports with aliases.

Returns: Port codes, names, country, region, and alias mappings (e.g., YANTIAN/SHEKOU to Shenzhen).

### 5. get_freight_index

Get freight market index trends and statistics.

Input: route (optional), period (optional: 7d/30d/90d)

Returns: Price trends, market averages, and volatility indicators.

### 6. subscribe_rate_alert

Subscribe to rate change alerts for specific routes.

Input: origin, destination, email, threshold (optional)

Returns: Subscription confirmation and alert preferences.

## Installation

### Claude Desktop

Add to claude_desktop_config.json:

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

Add to .cursor/mcp.json:

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

Use the SSE endpoint: https://search.shaq-logistics.com/sse

## Example Usage

Ask your AI assistant:

- What is the current FCL rate from Shenzhen to Los Angeles for a 40GP container?
- Find LCL rates from Ningbo to Hamburg
- Create a booking for shipping from Shanghai to Rotterdam
- Track booking SHAQ20260804001
- What ports are available in China?
- Show me the freight index trend for the China-US route

## Coverage

- Origins: 15+ Chinese ports (Shenzhen, Ningbo, Shanghai, Qingdao, Guangzhou, etc.)
- Destinations: 200+ ports worldwide (US, Europe, Southeast Asia, Middle East, etc.)
- Rate types: LCL (per CBM/TON) and FCL (20GP/40GP/40HQ/45HQ)
- Data volume: 160,000+ live rate entries, updated hourly

## Links

- Platform: https://search.shaq-logistics.com
- API Docs: https://search.shaq-logistics.com/openapi.json
- AI Guide: https://search.shaq-logistics.com/llms.txt

## License

MIT License - see LICENSE file.

---

Maintained by SHAQ Logistics | Contact: ayang@shaq-log.com
