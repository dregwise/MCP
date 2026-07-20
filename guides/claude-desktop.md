# Claude Desktop — Robinhood Trading MCP Setup

> **Connect Claude Desktop (GUI app) to Robinhood Agentic Trading via Dregwise**
>
> **MCP Endpoint:** `https://agent.robinhood.com/mcp/trading`  
> **Dregwise X:** [@_DregwiseRh](https://x.com/_DregwiseRh)  
> **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`

---

## Prerequisites

- **Claude Desktop** installed (macOS/Windows/Linux)
- **Anthropic account** with Claude Pro/Max or API access
- **Robinhood account** with individual investing account in good standing
- **Internet connection** for OAuth flow

---

## Quick Start (2 minutes)

1. Open **Claude Desktop** → **Settings** → **Connectors**
2. Click **Add custom connector**
3. Paste: `https://agent.robinhood.com/mcp/trading`
4. Click **Save** → **Authenticate** in browser
5. Complete **Agentic onboarding** if prompted
6. Test in chat: *"What's my Robinhood portfolio value?"*

---

## Step-by-Step Setup

### Step 1: Open Connector Settings

1. Launch **Claude Desktop**
2. Click your **profile avatar** (top-right) → **Settings**
3. Select **Connectors** tab (left sidebar)
4. Click **Add custom connector** button

### Step 2: Configure MCP Connection

**Connector Details:**
```
Name: Robinhood Trading (or Dregwise Trading)
Type: MCP (Model Context Protocol)
URL: https://agent.robinhood.com/mcp/trading
Transport: HTTP / Streamable HTTP (auto-detected)
```

Click **Save** or **Connect**.

### Step 3: OAuth Authentication

A browser window opens automatically:

1. **Sign in** to Robinhood (email/phone + 2FA)
2. **Review permissions** — the connector requests:
   - ✅ Read all accounts & account numbers
   - ✅ Read positions, balances, buying power
   - ✅ Read transaction history & orders
   - ✅ Read watchlists & scans
   - ✅ Place trades in **Agentic account only**
3. Click **Authorize** / **Allow**

### Step 4: Agentic Account Onboarding (First Time Only)

If you don't have an Agentic Trading account:

1. Robinhood shows: **"Open an Agentic Trading account?"**
2. **Requirements check:**
   - ✅ Primary individual investing account in good standing
   - ✅ Identity verified (SSN, address, DOB)
   - ✅ No account restrictions
3. **Review & Accept:**
   - Agentic Trading Terms of Service
   - Risk Disclosures
   - Market Data Agreements
4. Click **Open Account** — completes in seconds

> **Note:** You can have up to 10 self-directed individual investing accounts total (including Agentic).

### Step 5: Verify in Claude Desktop

Return to Claude Desktop. Start a new chat:

```
"What's my current portfolio value and buying power on Robinhood?"
```

Claude should respond with real data from your Agentic account.

---

## Available Capabilities in Claude Desktop

### Portfolio & Account Data
- "Show all my positions with P&L"
- "What's my cash balance and buying power?"
- "List my watchlists and the stocks in each"
- "Show my last 20 trades with fill prices"

### Trading (Agentic Account Only)
- "Buy $500 of AAPL at market"
- "Place limit order: 10 TSLA @ $250, good till cancelled"
- "Set trailing stop loss 5% on my NVDA position"
- "Cancel all open orders on Agentic account"

### Analysis & Intelligence
- "Analyze my portfolio risk: concentration, beta, sector exposure"
- "Why is ROAR up today? News, sentiment, options flow"
- "Build a bull/bear thesis for HMNI based on earnings, guidance, shorts"
- "Screen for stocks matching: market cap < $2B, insider buying > $500k, revenue growth > 30%"

### Automation (via Prompt Instructions)
```
"Every weekday at 9:35 AM ET, rebalance to 60% SPY / 40% QQQ using limit orders within 0.2% of mid. Skip if daily loss > $300."
```

---

## Configuration Persistence

Claude Desktop stores connectors in:

| OS | Path |
|----|------|
| macOS | `~/Library/Application Support/Claude/connectors.json` |
| Windows | `%APPDATA%\Claude\connectors.json` |
| Linux | `~/.config/Claude/connectors.json` |

**Backup/share config:**
```json
{
  "connectors": [
    {
      "id": "robinhood-trading",
      "name": "Robinhood Trading",
      "type": "mcp",
      "url": "https://agent.robinhood.com/mcp/trading",
      "enabled": true
    }
  ]
}
```

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Connector shows "Disconnected" | Click **Reconnect** → re-authenticate |
| "Failed to fetch tools" | Check internet → `curl https://agent.robinhood.com/mcp/trading` |
| No Agentic prompt | Primary RH account must be active & verified; contact RH support |
| Orders fail | Verify: Agentic buying power > 0, market hours, no PDT violation |
| "I can't access Robinhood" | Settings → Connectors → ensure **enabled** toggle is ON |

### Reset Connection

1. Settings → Connectors → **Remove** Robinhood Trading
2. Restart Claude Desktop
3. Re-add connector (Steps 1-4 above)

---

## Security Best Practices

⚠️ **You are responsible for all trades your agent executes.**

1. **Set guardrails in every prompt:**
   ```
   "Rules: No options. Max position $1,000. Daily stop-loss $300. Confirm before any trade > $200."
   ```

2. **Monitor daily** — Check Agentic account in Robinhood mobile app

3. **Revoke instantly** — Settings → Connectors → Remove → access revoked immediately

4. **Use unique instructions** — Don't copy-paste prompts blindly; tailor to your risk tolerance

---

## Resources

- **Dregwise GitHub:** https://github.com/Dregwise
- **X/Twitter:** [@_DregwiseRh](https://x.com/_DregwiseRh)
- **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`
- **Claude Desktop Docs:** https://support.anthropic.com/en/articles/9463449
- **MCP Spec:** https://modelcontextprotocol.io
- **Robinhood Agentic:** https://robinhood.com/agentic
- **Disclosures:** https://robinhood.com/legal/agentic-trading-disclosures

---

## Support

- **Issues:** https://github.com/Dregwise/issues
- **Discord:** https://discord.gg/dregwise
- **Email:** support@dregwise.xyz