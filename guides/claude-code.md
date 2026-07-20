# Claude Code — Robinhood Trading MCP Setup

> **Connect Claude Code (terminal) to Robinhood Agentic Trading via Dregwise**
>
> **MCP Endpoint:** `https://agent.robinhood.com/mcp/trading`  
> **Dregwise X:** [@_DregwiseRh](https://x.com/_DregwiseRh)  
> **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`

---

## Prerequisites

- **Claude Code** installed: `npm install -g @anthropic-ai/claude-code`
- **Authenticated:** `claude auth login`
- **Robinhood account** with individual investing account in good standing
- **Terminal** (macOS/Linux/WSL on Windows)

---

## Quick Start (30 seconds)

```bash
# 1. Add the Robinhood Trading MCP server
claude mcp add robinhood-trading --transport http https://agent.robinhood.com/mcp/trading

# 2. Start Claude Code
claude

# 3. In Claude Code, open MCP selector
/mcp

# 4. Select 'robinhood-trading' → Authenticate in browser → Complete Agentic onboarding
```

---

## Step-by-Step Setup

### Step 1: Install & Authenticate Claude Code

```bash
# Install (if not already)
npm install -g @anthropic-ai/claude-code

# Verify
claude --version

# Authenticate with Anthropic
claude auth login
# Opens browser → sign in → authorize
```

### Step 2: Add Robinhood Trading MCP

```bash
claude mcp add robinhood-trading \
  --transport http \
  https://agent.robinhood.com/mcp/trading
```

**Output:**
```
Added MCP server 'robinhood-trading' with transport 'http' at https://agent.robinhood.com/mcp/trading
```

### Step 3: Connect in Claude Code Session

```bash
claude
# Wait for prompt, then:
/mcp
```

**You'll see:**
```
Available MCP servers:
  ○ robinhood-trading (http://agent.robinhood.com/mcp/trading) — Not connected
```

Press `Enter` on `robinhood-trading` to connect.

### Step 4: Robinhood OAuth Flow

A browser window opens:

1. **Sign in** to Robinhood (or create account)
2. **Authorize** the MCP connector to access:
   - All accounts & account numbers
   - Positions, balances, buying power
   - Transaction history & orders
   - Watchlists & scans
3. **Agentic Account Onboarding** (first time only):
   - Robinhood prompts: "Open an Agentic Trading account?"
   - Requirements: Primary individual account in good standing
   - Accept Terms & Disclosures
   - Account opens instantly

### Step 5: Verify Connection

Back in Claude Code, test:

```
> What's my Robinhood portfolio value and buying power?
```

Expected: Claude returns real account data via MCP tools.

---

## Available MCP Tools (Robinhood Trading)

| Tool | Description |
|------|-------------|
| `get_accounts` | All accounts, numbers, status, type |
| `get_positions` | Current holdings: symbol, qty, avg cost, market value, P&L |
| `get_balances` | Cash, buying power, margin, unsettled funds |
| `get_transactions` | Order history: fills, dividends, splits, corporate actions |
| `get_watchlists` | Custom watchlists, saved scans |
| `place_order` | Market, limit, stop, stop-limit, trailing stop (Agentic only) |
| `cancel_order` | Cancel open orders |
| `get_order_status` | Check order state |

---

## Example Prompts for Agentic Trading

### Portfolio Building
```
Research the AI infrastructure supply chain (not NVDA/AMD). Find 8-10 small-cap tickers with strong fundamentals, insider buying, and catalyst timelines. Build a $25k portfolio with position sizes and entry limits.
```

### Automated Strategy
```
Standing order: Buy $200 of ROAR whenever it drops 3%+ intraday. Use limit orders at 0.2% below trigger. Max 1 trade/day. Stop if daily loss > $500.
```

### Rebalancing
```
Rebalance Agentic account to 25% ROAR / 75% HMNI. Use limit orders within 0.3% of mid. Show me the orders before placing.
```

### Risk Analysis
```
Full portfolio risk report: sector concentration, factor exposure (size, value, momentum), beta to SPY, max drawdown scenario, correlation matrix of top 10 positions.
```

### Market Intelligence
```
Why is HMNI moving today? Pull: news (last 48h), Twitter sentiment, options flow (unusual volume, put/call ratio), short interest change, earnings calendar, analyst revisions.
```

---

## Configuration File (Persistent)

Create `.claude/mcp.json` in your project root:

```json
{
  "mcpServers": {
    "robinhood-trading": {
      "transport": "http",
      "url": "https://agent.robinhood.com/mcp/trading"
    }
  }
}
```

Claude Code auto-loads this on startup.

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| `MCP server not found` | `claude mcp list` → verify entry exists → re-add |
| `Authentication failed` | Clear browser cookies for robinhood.com → retry `/mcp` |
| `No Agentic account prompt` | Ensure primary RH account is active & verified; contact RH support |
| `Orders fail` | Check: Agentic buying power, market hours, PDT status, position limits |
| `Connection timeout` | `curl -v https://agent.robinhood.com/mcp/trading` — check firewall/proxy |

### Debug Commands

```bash
# List configured MCPs
claude mcp list

# Remove & re-add
claude mcp remove robinhood-trading
claude mcp add robinhood-trading --transport http https://agent.robinhood.com/mcp/trading

# Test endpoint directly
curl -v https://agent.robinhood.com/mcp/trading
```

---

## Security Best Practices

1. **Guardrails in prompts:**
   ```
   "Never trade options. Max position $1,000. Daily loss limit $500. Require my confirmation for orders > $200."
   ```

2. **Monitor daily** — Check Agentic account in Robinhood app

3. **Revoke instantly** — `/mcp` → disconnect, or `claude mcp remove robinhood-trading`

4. **No API keys stored** — OAuth tokens managed by Claude Code securely

---

## Resources

- **Dregwise GitHub:** https://github.com/Dregwise
- **X/Twitter:** [@_DregwiseRh](https://x.com/_DregwiseRh)
- **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`
- **Claude Code Docs:** https://docs.anthropic.com/en/docs/claude-code
- **MCP Spec:** https://modelcontextprotocol.io
- **Robinhood Agentic:** https://robinhood.com/agentic
- **Disclosures:** https://robinhood.com/legal/

---

## Support

- **Issues:** https://github.com/Dregwise/issues
- **Website:** dregwise.xyz SOON
