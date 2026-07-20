# Codex CLI — Robinhood Trading MCP Setup

> **Connect Codex CLI (terminal) to Robinhood Agentic Trading via Dregwise**
>
> **MCP Endpoint:** `https://agent.robinhood.com/mcp/trading`  
> **Dregwise X:** [@_DregwiseRh](https://x.com/_DregwiseRh)  
> **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`

---

## Prerequisites

- **Codex CLI** installed: `npm install -g @openai/codex`
- **Authenticated:** `codex auth login`
- **Robinhood account** with individual investing account in good standing
- **Terminal** (macOS/Linux/WSL)

---

## Quick Start (30 seconds)

```bash
# 1. Add MCP server
codex mcp add robinhood-trading --url https://agent.robinhood.com/mcp/trading

# 2. Start Codex CLI
codex

# 3. In Codex, open MCP selector
/mcp

# 4. Select 'robinhood-trading' → Authenticate in browser → Complete Agentic onboarding
```

---

## Step-by-Step Setup

### Step 1: Install & Authenticate Codex CLI

```bash
# Install
npm install -g @openai/codex

# Verify
codex --version

# Authenticate with OpenAI
codex auth login
# Opens browser → sign in → authorize
```

### Step 2: Add Robinhood Trading MCP

```bash
codex mcp add robinhood-trading \
  --url https://agent.robinhood.com/mcp/trading
```

**Output:**
```
Added MCP server 'robinhood-trading' at https://agent.robinhood.com/mcp/trading
```

### Step 3: Connect in Codex Session

```bash
codex
# Wait for prompt, then:
/mcp
```

Select **robinhood-trading** from the list.

### Step 4: Robinhood OAuth Flow

Browser opens automatically:

1. **Sign in** to Robinhood
2. **Authorize** Codex CLI to access:
   - All accounts & numbers
   - Positions, balances, buying power
   - Transaction history & orders
   - Watchlists & scans
   - Trading in **Agentic account only**
3. **First time?** Agentic onboarding:
   - Primary account verification
   - Accept Terms & Disclosures
   - Instant account creation

### Step 5: Verify

In Codex CLI:

```
> What's my Robinhood portfolio value and buying power?
```

Returns live data from your Agentic account.

---

## Available MCP Tools

| Tool | Description |
|------|-------------|
| `get_accounts` | All accounts, numbers, status |
| `get_positions` | Holdings: symbol, qty, avg cost, market value, P&L |
| `get_balances` | Cash, buying power, margin, unsettled |
| `get_transactions` | Fills, dividends, splits, corporate actions |
| `get_watchlists` | Custom watchlists & saved scans |
| `place_order` | Market, limit, stop, stop-limit, trailing (Agentic only) |
| `cancel_order` | Cancel open orders |
| `get_order_status` | Check order state |

---

## Example Prompts

### Portfolio Analysis
```
"Fetch my positions, calculate 30-day momentum for each, show me the bottom 3 performers with >$500 position size."
```

### Automated Strategy (Codex writes & executes)
```
"Write a Python script that:
1. Gets my watchlist 'Momentum'
2. Screens for: price > $5, vol > 500k, RSI < 30
3. Places $150 limit orders at 0.5% below mid for top 3
4. Sets 3% trailing stop on each
5. Runs daily at 9:35 AM ET via cron
Save as momentum_strategy.py and run it."
```

### Risk Report
```
"Full risk report: sector weights, factor betas (size, value, mom, quality), max drawdown estimate, correlation matrix of top 10 positions, PDT status."
```

### Market Intelligence
```
"Why is HMNI moving? Get: news (24h), Twitter sentiment, options flow (unusual volume, put/call skew), short interest change, earnings calendar, analyst actions."
```

---

## Configuration File

Codex CLI stores MCP config at:

| OS | Path |
|----|------|
| macOS | `~/.codex/mcp.json` |
| Linux | `~/.config/codex/mcp.json` |
| Windows | `%USERPROFILE%\.codex\mcp.json` |

**Example `mcp.json`:**
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

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| `MCP server not found` | `codex mcp list` → verify → `codex mcp remove robinhood-trading` → re-add |
| `Authentication failed` | Clear browser cookies for robinhood.com → retry `/mcp` |
| `No Agentic prompt` | Primary RH account must be active & verified; contact RH support |
| `Orders fail` | Check: Agentic buying power, market hours, PDT rules, position limits |
| `Connection timeout` | `curl -v https://agent.robinhood.com/mcp/trading` — check firewall/proxy |

### Debug Commands

```bash
# List MCP servers
codex mcp list

# Remove server
codex mcp remove robinhood-trading

# Test endpoint
curl -v https://agent.robinhood.com/mcp/trading

# View config
cat ~/.codex/mcp.json
```

---

## Security Best Practices

1. **Guardrails in every prompt:**
   ```
   "Constraints: No options. Max position $1,000. Daily stop-loss $300. Confirm orders > $200."
   ```

2. **Monitor daily** — Check Agentic account in Robinhood app

3. **Instant revoke** — `codex mcp remove robinhood-trading`

4. **No stored secrets** — OAuth tokens managed by Codex CLI securely

---

## Resources

- **Dregwise GitHub:** https://github.com/Dregwise
- **X/Twitter:** [@_DregwiseRh](https://x.com/_DregwiseRh)
- **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`
- **Codex CLI Docs:** https://github.com/openai/codex
- **MCP Spec:** https://modelcontextprotocol.io
- **Robinhood Agentic:** https://robinhood.com/agentic
- **Disclosures:** https://robinhood.com/legal/agentic-trading-disclosures

---

## Support

- **Issues:** https://github.com/Dregwise/issues
- **Discord:** https://discord.gg/dregwise
- **Email:** support@dregwise.xyz