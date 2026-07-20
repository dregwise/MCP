# Grok (xAI) — Robinhood Trading MCP Setup

> **Connect Grok to Robinhood Agentic Trading via Dregwise**
>
> **MCP Endpoint:** `https://agent.robinhood.com/mcp/trading`  
> **Dregwise X:** [@_DregwiseRh](https://x.com/_DregwiseRh)  
> **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`

---

## Prerequisites

- **Grok access** (grok.x.ai or X Premium+)
- **Robinhood account** with individual investing account in good standing
- **Web browser** for OAuth flow

---

## Quick Start (3 minutes)

1. Open **Grok** (grok.x.ai or X app)
2. Start new chat → Click **+** (plus sign) → **Add connector** → **Custom**
3. Paste: `https://agent.robinhood.com/mcp/trading`
4. **Connect** → Authenticate Robinhood → Complete Agentic onboarding
5. Test: *"What's my Robinhood portfolio value?"*

---

## Step-by-Step Setup

### Step 1: Open Grok Connector Menu

**On web (grok.x.ai):**
1. Start a new chat
2. Click **+** (plus sign) next to message input
3. Select **Add connector** → **Custom**

**On X app:**
1. Open Grok chat
2. Tap attachment/connector icon
3. Select **Custom connector**

### Step 2: Configure Custom Connector

**Connector Details:**
```
Name: Robinhood Trading (Dregwise)
Type: MCP (Model Context Protocol)
URL: https://agent.robinhood.com/mcp/trading
```

Click **Save** / **Connect**.

### Step 3: OAuth Authentication

Browser/tab opens:

1. **Sign in** to Robinhood
2. **Authorize** Grok to access:
   - All accounts & numbers
   - Positions, balances, buying power
   - Transaction history & orders
   - Watchlists & scans
   - Trading in **Agentic account only**
3. **First time?** Agentic onboarding:
   - Primary account check
   - Accept Terms & Disclosures
   - Account created instantly

### Step 4: Verify in Grok

Back in Grok chat:

```
"What's my current portfolio value and buying power on Robinhood?"
```

Grok returns live data via MCP tools.

---

## Available MCP Tools in Grok

| Tool | Description |
|------|-------------|
| `get_accounts` | All Robinhood accounts, numbers, status |
| `get_positions` | Holdings: symbol, qty, avg cost, market value, P&L |
| `get_balances` | Cash, buying power, margin, unsettled |
| `get_transactions` | Fills, dividends, splits, corporate actions |
| `get_watchlists` | Custom watchlists & saved scans |
| `place_order` | Market, limit, stop, stop-limit, trailing (Agentic only) |
| `cancel_order` | Cancel open orders |
| `get_order_status` | Check order state |

---

## Example Prompts for Grok

### Portfolio Analysis
```
"Analyze my Robinhood portfolio: total value, daily P&L, top 5 positions, sector allocation, any concentration risk >15% in single name."
```

### Market Intelligence (Grok strength)
```
"Why is ROAR moving today? Use X/Twitter sentiment, news, options flow, short interest. Give me a bull/bear case with price levels."
```

### Automated Strategy
```
"Set up: If SPY drops >1.5% intraday, buy $200 SPY at market. Max 1/day. Stop if daily loss > $300. Confirm each trade."
```

### Research Deep Dive
```
"Research HMNI: last 4 earnings calls, insider buying/selling, institutional ownership changes, short interest trend, catalyst calendar. Format as investment memo."
```

### Risk Management
```
"Check my Agentic account for: PDT violation risk, margin usage > 50%, earnings in next 7 days for any position > $500, correlation clusters."
```

---

## Configuration

Grok stores connectors per account. To manage:

1. Grok chat → **+** → **Manage connectors**
2. Find **Robinhood Trading (Dregwise)**
3. **Disconnect** to revoke, **Reconnect** to re-auth

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| "Connector failed" | Verify URL: `https://agent.robinhood.com/mcp/trading` |
| "Auth error" | Remove connector → re-add → fresh OAuth |
| No Agentic prompt | Primary RH account must be verified & in good standing |
| Tools not working | Refresh Grok; wait for MCP handshake (5-10s) |
| Orders rejected | Check: Agentic buying power, market hours, limits |

---

## Security Best Practices

1. **Guardrails in prompts** — Grok doesn't persist system prompts; include every time:
   ```
   "Rules: No options. Max $1,000/trade. Daily stop $300. Confirm >$200. No pre-market."
   ```

2. **Monitor daily** — Robinhood app → Agentic account → Activity

3. **Instant revoke** — Grok → **+** → Manage connectors → Disconnect

4. **Session isolation** — Each Grok chat is fresh; restate rules

---

## Resources

- **Dregwise GitHub:** https://github.com/Dregwise
- **X/Twitter:** [@_DregwiseRh](https://x.com/_DregwiseRh)
- **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`
- **Grok Docs:** https://grok.x.ai/docs
- **MCP Spec:** https://modelcontextprotocol.io
- **Robinhood Agentic:** https://robinhood.com/agentic
- **Disclosures:** https://robinhood.com/legal/

---

## Support

- **Issues:** https://github.com/Dregwise/issues
- **Website:** dregwise.xyz SOON