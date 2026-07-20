# Other MCP Clients — Robinhood Trading MCP Setup

> **Connect any MCP-compatible client to Robinhood Agentic Trading via Dregwise**
>
> **MCP Endpoint:** `https://agent.robinhood.com/mcp/trading`  
> **Dregwise X:** [@_DregwiseRh](https://x.com/_DregwiseRh)  
> **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`

---

## Universal MCP Configuration

The Robinhood Trading MCP server is accessible at:

```
URL: https://agent.robinhood.com/mcp/trading
Transport: Streamable HTTP (recommended) / HTTP
Authentication: OAuth 2.0 (handled by client)
Capabilities: tools/list, tools/call, resources/list, prompts/list
```

**Test endpoint:**
```bash
curl -v https://agent.robinhood.com/mcp/trading
```

---

## Client-Specific Setup

### Continue (VS Code / JetBrains Extension)

**Config:** `.continue/config.json`
```json
{
  "mcpServers": {
    "robinhood-trading": {
      "transport": "streamable-http",
      "url": "https://agent.robinhood.com/mcp/trading"
    }
  }
}
```
Restart IDE → Continue sidebar → MCP → Connect.

---

### Windsurf (Codeium)

**Config:** `~/.codeium/windsurf/mcp_config.json`
```json
{
  "mcpServers": {
    "robinhood-trading": {
      "url": "https://agent.robinhood.com/mcp/trading",
      "transport": "streamable-http"
    }
  }
}
```
Windsurf → Settings → MCP → Add Server.

---

### VS Code (GitHub Copilot Chat)

**Config:** `.vscode/mcp.json` (workspace) or User settings
```json
{
  "mcp": {
    "servers": {
      "robinhood-trading": {
        "url": "https://agent.robinhood.com/mcp/trading",
        "type": "streamable-http"
      }
    }
  }
}
```
VS Code → Copilot Chat → MCP Servers → Refresh.

---

### Custom Python Agent

```python
#!/usr/bin/env python3
"""Minimal Robinhood Trading MCP Client"""
import asyncio
from mcp import ClientSession, StdioServerParameters
from mcp.client.streamable_http import streamablehttp_client

async def main():
    # Connect to Robinhood Trading MCP
    async with streamablehttp_client("https://agent.robinhood.com/mcp/trading") as (read, write):
        async with ClientSession(read, write) as session:
            await session.initialize()
            
            # List available tools
            tools = await session.list_tools()
            print("Available tools:", [t.name for t in tools.tools])
            
            # Get portfolio
            result = await session.call_tool("get_positions", {})
            print("Positions:", result)
            
            # Place order (requires confirmation in real use)
            # order = await session.call_tool("place_order", {
            #     "symbol": "AAPL", "side": "buy", "type": "market", "quantity": 1
            # })

if __name__ == "__main__":
    asyncio.run(main())
```

**Install deps:** `pip install mcp`

---

### Custom Node.js Agent

```javascript
// mcp-robinhood-client.js
import { Client } from "@modelcontextprotocol/sdk/client/index.js";
import { StreamableHTTPClientTransport } from "@modelcontextprotocol/sdk/client/streamableHttp.js";

const client = new Client(
  { name: "dregwise-agent", version: "1.0.0" },
  { capabilities: { tools: {} } }
);

const transport = new StreamableHTTPClientTransport(
  new URL("https://agent.robinhood.com/mcp/trading")
);

await client.connect(transport);

// List tools
const tools = await client.listTools();
console.log("Tools:", tools.tools.map(t => t.name));

// Get positions
const positions = await client.callTool({ name: "get_positions", arguments: {} });
console.log("Positions:", positions);

// Place order (with confirmation)
// const order = await client.callTool({
//   name: "place_order",
//   arguments: { symbol: "AAPL", side: "buy", type: "market", quantity: 1 }
// });

await client.close();
```

**Install deps:** `npm install @modelcontextprotocol/sdk`

---

### Custom Go Agent

```go
// main.go
package main

import (
    "context"
    "log"
    "github.com/mark3labs/mcp-go/client"
    "github.com/mark3labs/mcp-go/client/streamablehttp"
)

func main() {
    c, err := streamablehttp.NewClient("https://agent.robinhood.com/mcp/trading")
    if err != nil {
        log.Fatal(err)
    }
    defer c.Close()

    ctx := context.Background()
    if err := c.Initialize(ctx); err != nil {
        log.Fatal(err)
    }

    // List tools
    tools, err := c.ListTools(ctx)
    if err != nil {
        log.Fatal(err)
    }
    for _, t := range tools.Tools {
        log.Println("Tool:", t.Name)
    }

    // Get positions
    result, err := c.CallTool(ctx, "get_positions", map[string]any{})
    if err != nil {
        log.Fatal(err)
    }
    log.Println("Positions:", result)
}
```

**Install deps:** `go get github.com/mark3labs/mcp-go`

---

### HTTP API (Direct REST-like)

If your client doesn't support MCP natively, you can proxy through a local MCP gateway:

```bash
# Run local MCP gateway (exposes MCP as REST)
npx @modelcontextprotocol/gateway --server https://agent.robinhood.com/mcp/trading --port 8080
```

Then call:
```bash
curl -X POST http://localhost:8080/tools/get_positions -d '{}'
curl -X POST http://localhost:8080/tools/place_order -d '{"symbol":"AAPL","side":"buy","type":"market","quantity":1}'
```

---

## Available MCP Tools (All Clients)

| Tool | Arguments | Returns |
|------|-----------|---------|
| `get_accounts` | `{}` | Array of accounts with numbers, types, status |
| `get_positions` | `{}` | Holdings: symbol, qty, avg_cost, market_value, unrealized_pl |
| `get_balances` | `{}` | Cash, buying_power, margin_balance, unsettled_funds |
| `get_transactions` | `{limit?, cursor?}` | Paginated fills, dividends, splits |
| `get_watchlists` | `{}` | Watchlist names + symbols |
| `place_order` | `{symbol, side, type, quantity, price?, stop_price?, time_in_force?}` | Order confirmation with ID |
| `cancel_order` | `{order_id}` | Cancellation status |
| `get_order_status` | `{order_id}` | Order state: filled, partial, cancelled, pending |

**Order Types:**
- `market` — Immediate execution
- `limit` — At specified price or better
- `stop` — Market when stop price hit
- `stop_limit` — Limit when stop price hit
- `trailing_stop` — Trailing %/$ below high

**Time in Force:**
- `day` — End of trading day
- `gtc` — Good till cancelled (90 days)
- `gtx` — Good till extended hours
- `ioc` — Immediate or cancel
- `fok` — Fill or kill

---

## Authentication Flow (All Clients)

```
1. Client initiates connection to https://agent.robinhood.com/mcp/trading
2. Server returns OAuth authorization URL
3. Client opens URL in browser (or provides link)
4. User signs into Robinhood
5. User authorizes requested scopes:
   - read:accounts
   - read:positions
   - read:orders
   - read:watchlists
   - trade:agentic
6. Robinhood redirects back with auth code
7. Client exchanges code for access token
8. MCP session established — tools available
9. First time? Agentic account onboarding triggered automatically
```

---

## Troubleshooting (Universal)

| Problem | Diagnosis | Fix |
|---------|-----------|-----|
| Connection refused | Network/firewall | `curl -v https://agent.robinhood.com/mcp/trading` |
| 401 Unauthorized | Token expired | Re-authenticate (client-specific) |
| 403 Forbidden | Scope missing | Ensure `trade:agentic` granted for orders |
| 500 Server error | Robinhood issue | Check status.robinhood.com; retry |
| Tools empty | MCP handshake failed | Restart client; check logs |
| No Agentic prompt | Account not eligible | Primary RH account must be verified & good standing |

---

## Security Checklist (All Clients)

- [ ] Use only official URL: `https://agent.robinhood.com/mcp/trading`
- [ ] Never hardcode OAuth tokens — use client's secure storage
- [ ] Implement confirmation prompts for `place_order` calls
- [ ] Set position/daily loss limits in agent logic
- [ ] Log all tool calls for audit trail
- [ ] Monitor Agentic account daily in Robinhood app
- [ ] Know how to revoke: disconnect MCP in client settings

---

## Resources

- **Dregwise GitHub:** https://github.com/Dregwise
- **X/Twitter:** [@_DregwiseRh](https://x.com/_DregwiseRh)
- **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`
- **MCP Spec:** https://modelcontextprotocol.io
- **MCP SDKs:** https://github.com/modelcontextprotocol
- **Robinhood Agentic:** https://robinhood.com/agentic
- **Disclosures:** https://robinhood.com/legal/

---

## Support

- **Issues:** https://github.com/Dregwise/issues
- **Website:** dregwise.xyz SOON

---

## Contributing New Client Guides

If you've connected a new MCP client, please contribute a guide:

1. Fork Dregwise repo
2. Add `guides/your-client.md` following this template
3. Include: config, auth flow, tools, examples, troubleshooting
4. Submit PR — we'll review and merge

**Template:** `guides/TEMPLATE.md` (create if needed)