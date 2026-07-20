# Codex (Web UI) — Robinhood Trading MCP Setup

> **Connect Codex in browser to Robinhood Agentic Trading via Dregwise**
>
> **MCP Endpoint:** `https://agent.robinhood.com/mcp/trading`  
> **Dregwise X:** [@_DregwiseRh](https://x.com/_DregwiseRh)  
> **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`

---

## Prerequisites

- **Codex account** (codex.openai.com) with access
- **Robinhood account** with individual investing account in good standing
- **Web browser** for OAuth flow

---

## Quick Start (3 minutes)

1. Open **Codex** → **Settings** → **MCP servers**
2. Select **Streamable HTTP**
3. Add URL: `https://agent.robinhood.com/mcp/trading`
4. Click **Connect** → Authenticate Robinhood → Complete Agentic onboarding
5. Test in chat: *"What's my Robinhood portfolio value?"*

---

## Step-by-Step Setup

### Step 1: Open MCP Settings

1. Go to **codex.openai.com** and sign in
2. Click **Settings** (gear icon, bottom-left or top-right)
3. Select **MCP servers** tab

### Step 2: Add Robinhood Trading MCP

1. Click **Add MCP server** / **+ New server**
2. **Server type:** Select **Streamable HTTP**
3. **Configuration:**
   ```
   Name: Robinhood Trading (Dregwise)
   URL: https://agent.robinhood.com/mcp/trading
   ```
4. Click **Save** / **Connect**

### Step 3: OAuth Authentication

A popup/modal opens:

1. **Sign in** to Robinhood
2. **Authorize** Codex to access:
   - All accounts & account numbers
   - Positions, balances, buying power
   - Transaction history & orders
   - Watchlists & scans
   - Trading in **Agentic account only**
3. **First time?** Agentic onboarding:
   - Primary account check
   - Accept Terms & Disclosures
   - Account created instantly

### Step 4: Verify Connection

In Codex chat, test:

```
"What's my current portfolio value and buying power on Robinhood?"
```

Codex should return live data via MCP tools.

---

## Available MCP Tools in Codex

| Tool | Use Case |
|------|----------|
| `get_accounts` | List all accounts, types, status |
| `get_positions` | Current holdings with P&L |
| `get_balances` | Cash, buying power, margin |
| `get_transactions` | Order fills, dividends, splits |
| `get_watchlists` | Saved watchlists & scans |
| `place_order` | Market/limit/stop/trailing (Agentic only) |
| `cancel_order` | Cancel open orders |
| `get_order_status` | Check order state |

---

## Example Prompts for Codex

### Code-Generation Style Trading
```python
# Codex can write and execute this logic
"Write a Python function that:
1. Fetches my positions via MCP
2. Calculates 20-day momentum for each
3. Rebalances top 3 to equal weight
4. Places limit orders within 0.5% of mid
5. Returns order confirmations"
```

### Research & Analysis
```
"Pull my watchlist 'AI Supply Chain'. For each symbol: get 30-day vol, short interest, earnings date, analyst revisions. Rank by composite score."
```

### Risk Management
```
"Check my Agentic account for: positions > 20% portfolio, correlation > 0.8 pairs, any stock with earnings in 5 days. Flag risks."
```

### Automation Scripts
```
"Create a daily 9:30 AM script: if SPY gap down > 1%, buy $200 SPY at market. Include PDT check. Output order IDs."
```

---

## Configuration (Codex Settings)

MCP servers persist in Codex settings. To view/edit:

1. Settings → MCP servers
2. Find **Robinhood Trading (Dregwise)**
3. Toggle **Enabled** / **Remove** as needed

**Config file location** (for reference):
- Settings stored in Codex cloud — no local file

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| "Server unreachable" | Check URL exactly: `https://agent.robinhood.com/mcp/trading` |
| "Auth failed" | Remove server → re-add → fresh OAuth |
| No Agentic prompt | Primary RH account must be verified & unrestricted |
| Tools not appearing | Refresh page; wait 10s for MCP handshake |
| Orders fail | Verify Agentic buying power, market hours, limits |

---

## Security Best Practices

1. **Prompt guardrails** — Include in every session:
   ```
   "Rules: No options. Max $1,000/trade. Daily loss cap $300. Confirm >$200. No pre-market."
   ```

2. **Session isolation** — Each Codex chat is independent; restate rules

3. **Revoke access** — Settings → MCP servers → Remove → immediate

4. **Audit trail** — Check Robinhood app → Agentic account → Activity

---

## Resources

- **Dregwise GitHub:** https://github.com/Dregwise
- **X/Twitter:** [@_DregwiseRh](https://x.com/_DregwiseRh)
- **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`
- **Codex Docs:** https://codex.openai.com/docs
- **MCP Spec:** https://modelcontextprotocol.io
- **Robinhood Agentic:** https://robinhood.com/agentic
- **Disclosures:** https://robinhood.com/legal/agentic-trading-disclosures

---

## Support

- **Issues:** https://github.com/Dregwise/issues
- **Discord:** https://discord.gg/dregwise
- **Email:** support@dregwise.xyz