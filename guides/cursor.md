# Cursor — Robinhood Trading MCP Setup

> **Connect Cursor IDE to Robinhood Agentic Trading via Dregwise**
>
> **MCP Endpoint:** `https://agent.robinhood.com/mcp/trading`  
> **Dregwise X:** [@_DregwiseRh](https://x.com/_DregwiseRh)  
> **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`

---

## Prerequisites

- **Cursor** installed (cursor.sh)
- **Robinhood account** with individual investing account in good standing
- **Cursor account** (free or Pro)

---

## Quick Start (2 minutes)

1. Cursor → **Settings** → **Cursor Settings** (Cmd/Ctrl + Shift + J)
2. **Tools & MCPs** → **Connect** → **Add MCP Server**
3. URL: `https://agent.robinhood.com/mcp/trading`
4. **Connect** → Authenticate Robinhood → Complete Agentic onboarding
5. Test in Cursor Chat: *"What's my Robinhood portfolio value?"*

---

## Step-by-Step Setup

### Step 1: Open MCP Settings

1. Open **Cursor**
2. **Settings** (gear icon) → **Cursor Settings**
   - Or press `Cmd+Shift+J` (macOS) / `Ctrl+Shift+J` (Windows/Linux)
3. Navigate to **Tools & MCPs** tab (left sidebar)
4. Click **Connect** under "MCP Servers"

### Step 2: Add Robinhood Trading MCP

**MCP Server Configuration:**
```
Name: Robinhood Trading (Dregwise)
Type: HTTP / Streamable HTTP
URL: https://agent.robinhood.com/mcp/trading
```

Click **Connect** / **Save**.

### Step 3: OAuth Authentication

Browser window opens:

1. **Sign in** to Robinhood
2. **Authorize** Cursor to access:
   - All accounts & account numbers
   - Positions, balances, buying power
   - Transaction history & orders
   - Watchlists & scans
   - Trading in **Agentic account only**
3. **First time?** Agentic onboarding:
   - Primary account check
   - Accept Terms & Disclosures
   - Account created instantly

### Step 4: Verify in Cursor Chat

Open **Cursor Chat** (Cmd/Ctrl + L):

```
"What's my current portfolio value and buying power on Robinhood?"
```

Cursor should return live data via MCP.

---

## Using Robinhood MCP in Cursor

### Cursor Chat (Cmd/Ctrl + L)

Natural language queries:
- "Show my positions with P&L"
- "Why is ROAR up today? News, sentiment, options flow"
- "Build a rebalance script for 60/40 SPY/QQQ"
- "Place limit order: 20 HMNI @ $12.50, GTC — show preview first"

### Cursor Composer (Cmd/Ctrl + I)

Multi-file trading automation:
```
"Create a daily trading bot:
1. src/mcp/robinhood.py — MCP client wrapper
2. src/strategies/momentum.py — RSI < 30 screener
3. src/risk/guards.py — position limits, PDT check
4. scripts/daily.py — runs at 9:30 AM via cron
5. README with setup instructions"
```

### Inline Editor (Cmd/Ctrl + K)

Quick edits with MCP context:
- Highlight code → Cmd/Ctrl + K → "Add trailing stop logic using Robinhood MCP place_order tool"

---

## Available MCP Tools in Cursor

| Tool | Cursor Integration |
|------|-------------------|
| `get_accounts` | Chat, Composer, Inline |
| `get_positions` | Chat, Composer, Inline |
| `get_balances` | Chat, Composer, Inline |
| `get_transactions` | Chat, Composer |
| `get_watchlists` | Chat, Composer |
| `place_order` | Chat (with confirmation), Composer |
| `cancel_order` | Chat, Composer |
| `get_order_status` | Chat |

---

## Example Workflows

### 1. Portfolio Dashboard (Composer)
```
"Build a React dashboard (Next.js + Tailwind) showing:
- Total portfolio value & daily P&L
- Position table with sparklines
- Sector allocation pie chart
- Buying power & margin usage
- Auto-refresh every 30s via MCP"
```

### 2. Automated Strategy (Composer)
```
"Create a fully typed TypeScript trading bot:
- Strategy: Mean reversion on watchlist 'Oversold'
- Entry: RSI(14) < 30, vol > 1M, price > $10
- Sizing: $200 max, 2% trailing stop
- Risk: Max 5 positions, daily loss cap $400
- Schedule: 9:35 AM & 1:00 PM ET
- Logging: Winston to file + console
- Tests: Vitest with mocked MCP responses"
```

### 3. Research Agent (Chat)
```
"Analyze my watchlist 'Biotech Catalysts'. For each:
- Upcoming catalysts (PDUFA, ASCO, earnings)
- Cash runway (quarters)
- Insider transactions (6mo)
- Short interest & days to cover
- Options gamma exposure
Output as markdown table with conviction score 1-10."
```

---

## Configuration (Local Config)

Cursor stores MCP config in:

| OS | Path |
|----|------|
| macOS | `~/Library/Application Support/Cursor/User/globalStorage/mcp.json` |
| Windows | `%APPDATA%\Cursor\User\globalStorage\mcp.json` |
| Linux | `~/.config/Cursor/User/globalStorage/mcp.json` |

**Manual config (if needed):**
```json
{
  "mcpServers": {
    "robinhood-trading": {
      "url": "https://agent.robinhood.com/mcp/trading",
      "transport": "streamable-http",
      "enabled": true
    }
  }
}
```

Restart Cursor after manual edit.

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| "MCP connection failed" | Verify URL exactly: `https://agent.robinhood.com/mcp/trading` |
| "Tools not loading" | Restart Cursor → Settings → Tools & MCPs → Reconnect |
| No Agentic prompt | Primary RH account must be active & verified |
| Orders fail | Check: Agentic buying power, market hours, PDT status |
| Auth loop | Clear Cursor cookies → re-authenticate |

---

## Security Best Practices

1. **Prompt guardrails** — Include in system prompt or each request:
   ```
   "Rules: No options/crypto. Max $1,000/trade. Daily stop $300. Confirm >$200."
   ```

2. **Use .cursorrules** — Project-level rules file:
   ```
   # .cursorrules
   - Never place orders without explicit user confirmation
   - Max position size: $1,000
   - Daily loss limit: $300
   - Respect PDT rules
   ```

3. **Monitor daily** — Robinhood app → Agentic account

4. **Revoke instantly** — Settings → Tools & MCPs → Disconnect

---

## Resources

- **Dregwise GitHub:** https://github.com/Dregwise
- **X/Twitter:** [@_DregwiseRh](https://x.com/_DregwiseRh)
- **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`
- **Cursor Docs:** https://cursor.sh/docs
- **Cursor MCP:** https://cursor.sh/docs/mcp
- **MCP Spec:** https://modelcontextprotocol.io
- **Robinhood Agentic:** https://robinhood.com/agentic
- **Disclosures:** https://robinhood.com/legal/

---

## Support

- **Issues:** https://github.com/Dregwise/issues
- **Website:** dregwise.xyz SOON