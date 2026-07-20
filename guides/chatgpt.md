# ChatGPT (Custom GPT) — Robinhood Trading MCP Setup

> **Connect a Custom GPT in ChatGPT to Robinhood Agentic Trading via Dregwise**
>
> **MCP Endpoint:** `https://agent.robinhood.com/mcp/trading`  
> **Dregwise X:** [@_DregwiseRh](https://x.com/_DregwiseRh)  
> **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`

---

## Prerequisites

- **ChatGPT Plus/Team/Enterprise** (Custom GPTs require paid plan)
- **Developer Mode** enabled in ChatGPT settings
- **Robinhood account** with individual investing account in good standing
- **Web browser** for OAuth flow

---

## Quick Start (5 minutes)

1. ChatGPT → **Settings** → **Developer Mode** → **ON**
2. **Settings** → **Apps** → **Create app** (or "Create a GPT")
3. **Configure** → **Actions** → **Add Action** → **MCP**
4. URL: `https://agent.robinhood.com/mcp/trading`
5. **Save** → **Test** → Authenticate Robinhood → Complete Agentic onboarding
6. **Publish** your Custom GPT (private or public)

---

## Step-by-Step Setup

### Step 1: Enable Developer Mode

1. Open **ChatGPT** (chat.openai.com)
2. Click **profile** (bottom-left) → **Settings**
3. **Beta features** / **Developer** tab → Toggle **Developer Mode: ON**
4. Refresh page

### Step 2: Create Custom GPT (App)

1. Settings → **Apps** (or "My GPTs") → **Create app** / **Create a GPT**
2. **Configure** tab (left sidebar)

**Basic Info:**
```
Name: Dregwise Trading Agent
Description: AI agent for Robinhood Agentic Trading via MCP. Portfolio analysis, automated strategies, market research.
Category: Finance / Productivity
```

### Step 3: Add MCP Action

1. In Configure tab → **Actions** section → **Add Action**
2. Select **MCP (Model Context Protocol)** from dropdown
3. **Configuration:**
   ```
   Server URL: https://agent.robinhood.com/mcp/trading
   Transport: Streamable HTTP (default)
   ```
4. Click **Test Connection** — browser opens for OAuth

### Step 4: Robinhood OAuth & Agentic Onboarding

**Browser flow:**

1. **Sign in** to Robinhood
2. **Authorize** Custom GPT to access:
   - All accounts & numbers
   - Positions, balances, buying power
   - Transaction history & orders
   - Watchlists & scans
   - Trading in Agentic account only
3. **First time?** Agentic account onboarding:
   - Verify primary account in good standing
   - Accept Agentic Terms & Disclosures
   - Account opens instantly
4. Return to ChatGPT — shows **✅ Connected**

### Step 5: Configure GPT Instructions

**Instructions (System Prompt) — paste this:**

```markdown
# Dregwise Trading Agent — System Instructions

You are an AI trading agent connected to Robinhood Agentic Trading via MCP. You have real-time access to the user's portfolio, balances, orders, and can place trades in their Agentic account.

## Capabilities
- Read: All accounts, positions, balances, transactions, watchlists
- Trade: Market, limit, stop, stop-limit, trailing stop (Agentic account only)
- Analyze: Risk, concentration, factor exposure, market intel

## Guardrails (MANDATORY - never violate)
1. NEVER trade options, crypto, or fractional shares unless explicitly asked
2. MAX position size: $1,000 (or user-specified limit)
3. DAILY loss limit: $500 (or user-specified)
4. REQUIRE confirmation for orders > $200
5. NO pre/post-market unless requested
6. RESPECT PDT rules — flag if 3+ day trades in 5 days
7. ALWAYS show order preview before placing

## Response Format
- Data queries: Clean tables with key metrics
- Trade proposals: Order ticket preview (symbol, side, qty, type, price, time-in-force)
- Analysis: Structured sections (Thesis, Risks, Catalysts, Levels)
- Errors: Clear explanation + suggested fix

## Tone
Professional, concise, data-driven. No hype. Flag risks prominently.
```

### Step 6: Save & Test

1. Click **Save** (top-right)
2. **Test in Preview** pane:
   - "What's my portfolio value?"
   - "Show my top 5 positions by P&L"
   - "Why is ROAR moving today?"

### Step 7: Publish (Optional)

- **Private:** Only you can use
- **Anyone with link:** Share with team
- **Public:** List in GPT Store (requires review)

---

## Available Actions (MCP Tools)

| Action | Description |
|--------|-------------|
| `get_accounts` | All Robinhood accounts, numbers, status |
| `get_positions` | Holdings: symbol, qty, avg cost, market value, P&L |
| `get_balances` | Cash, buying power, margin, unsettled |
| `get_transactions` | Fills, dividends, splits, corporate actions |
| `get_watchlists` | Custom watchlists & saved scans |
| `place_order` | Market/limit/stop/stop-limit/trailing (Agentic only) |
| `cancel_order` | Cancel open orders |
| `get_order_status` | Check order state |

---

## Example Conversations

### Portfolio Review
```
User: "Full portfolio breakdown with sector allocation and risk metrics"
GPT: [Returns formatted table + concentration analysis + beta + VaR]
```

### Automated Strategy
```
User: "Buy $100 of HMNI every Tuesday at 10 AM if it's down >1% from Friday close. Stop after 10 trades or $500 total."
GPT: [Confirms parameters → Sets up standing instruction → Reports weekly]
```

### Market Research
```
User: "Deep dive on ROAR: earnings history, insider transactions, short interest, options flow, catalyst calendar"
GPT: [Structured report with data tables, charts described, thesis summary]
```

### Risk Management
```
User: "Set a 10% trailing stop on all positions > $500. Alert me if any position drops 15% intraday."
GPT: [Places trailing stops → Confirms each → Sets monitoring]
```

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| "MCP connection failed" | Verify URL exactly: `https://agent.robinhood.com/mcp/trading` |
| "Authentication error" | Delete action → re-add → fresh OAuth |
| "No Agentic account" | Ensure primary RH account active; contact RH support |
| Actions not showing | Refresh page; check Developer Mode is ON |
| Rate limited | Wait 60s; MCP has generous limits but not infinite |

---

## Security Notes

- **OAuth tokens** managed by OpenAI — you never see them
- **Revoke access:** Delete the Action in GPT config → immediate revoke
- **Data privacy:** OpenAI processes data per their policy; Robinhood per theirs
- **Your responsibility:** All trades executed by your GPT are YOUR trades

---

## Resources

- **Dregwise GitHub:** https://github.com/Dregwise
- **X/Twitter:** [@_DregwiseRh](https://x.com/_DregwiseRh)
- **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44`
- **ChatGPT Custom GPTs:** https://platform.openai.com/docs/gpts
- **MCP Spec:** https://modelcontextprotocol.io
- **Robinhood Agentic:** https://robinhood.com/agentic
- **Disclosures:** https://robinhood.com/legal/agentic-trading-disclosures

---

## Support

- **Issues:** https://github.com/Dregwise/issues
- **Discord:** https://discord.gg/dregwise
- **Email:** support@dregwise.xyz