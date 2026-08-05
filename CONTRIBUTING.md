# Contributing to SHAQ Logistics MCP Server

First off, thanks for taking the time to contribute! 🎉

This document covers the most common ways to contribute. Anything not covered here, feel free to open an issue and ask.

## Code of Conduct

By participating, you agree to uphold our [Code of Conduct](CODE_OF_CONDUCT.md). Be kind, respectful, and constructive.

## Ways to Contribute

### 🐛 Reporting Bugs

Open a [Bug Report](https://github.com/shaqlog2-ops/shaq-mcp-server/issues/new?template=bug_report.md). Include:
- MCP client name and version (Claude Desktop, Cursor, etc.)
- Steps to reproduce
- Expected vs actual behavior
- Error output / logs

### 💡 Suggesting Enhancements

Open a [Feature Request](https://github.com/shaqlog2-ops/shaq-mcp-server/issues/new?template=feature_request.md). Describe:
- The problem you're trying to solve
- Your proposed solution
- Any alternatives you've considered

### 🚢 Adding a New Port / Route

Open a [Port Request](https://github.com/shaqlog2-ops/shaq-mcp-server/issues/new?template=port_request.md). Include:
- Origin / destination port
- Shipment type (LCL / FCL)
- Container types
- Why this route matters

### 🔧 Code Contributions

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-new-tool`
3. Make your changes — keep diffs focused
4. Test against the live endpoint: `https://search.shaq-logistics.com/sse`
5. Update `lhm.plugin.json` if adding/changing a tool
6. Update `README.md` if user-facing
7. Commit using [Conventional Commits](https://www.conventionalcommits.org/):
   - `feat: add air freight rate search tool`
   - `fix: handle empty origin port gracefully`
   - `docs: add Ningbo port examples to README`
8. Open a Pull Request against `main`

## Tool Manifest Format (`lhm.plugin.json`)

Each tool entry has:

```json
{
  "name": "snake_case_tool_name",
  "description": "One-sentence description of what it does.",
  "inputSchema": {
    "type": "object",
    "properties": { ... },
    "required": [ ... ]
  }
}
```

## Development Setup

The MCP server is a Python service using FastAPI + SSE transport. To run locally:

```bash
git clone https://github.com/shaqlog2-ops/shaq-mcp-server.git
cd shaq-mcp-server
# Server code is deployed at https://search.shaq-logistics.com
# The endpoint is publicly accessible — no auth required for testing
```

Test with any MCP-compatible client by pointing it at:

```
https://search.shaq-logistics.com/sse
```

## Questions?

Open a [Discussion](https://github.com/shaqlog2-ops/shaq-mcp-server/discussions) or email ayang@shaq-log.com.
