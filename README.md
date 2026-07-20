# Dregwise — Robinhood Agentic Trading MCP Documentation

> **Official documentation for connecting AI agents to Robinhood Trading via MCP (Model Context Protocol)**
>
> **X (Twitter):** [@_DregwiseRh](https://x.com/_DregwiseRh)  
> **Contract:** `0x3547ffe3f05a8371f1c37ca0763456969889cf44` (Robinhood Mainnet)  
> **MCP:** `https://agent.robinhood.com/mcp/trading`

---

## 🎯 What is Dregwise?

Dregwise is the definitive integration layer and documentation hub for **Robinhood Agentic Trading** — enabling AI agents (Claude, ChatGPT, Codex, Cursor, Grok, and custom agents) to securely access your Robinhood portfolio, analyze markets, and execute trades through the **Robinhood Trading MCP** server.

### The Core Idea

> **Model Context Protocol (MCP)** is an open standard that lets AI agents connect to external apps and services. Instead of just answering questions, an AI with MCP access can **take actions on your behalf** — checking balances, analyzing positions, placing orders, and managing your portfolio.

With Dregwise, you connect your preferred AI agent to `https://agent.robinhood.com/mcp/trading`, authenticate with Robinhood, and your agent gains superpowers.

---

## 🤖 What Your Agent Can Do

Once connected to the Robinhood Trading MCP, your AI agent can:

| Category | Capabilities |
|----------|--------------|
| **Portfolio Intelligence** | View total portfolio value, buying power, cash balances, positions with real-time P&L |
| **Account Access** | Read all Robinhood accounts (individual, IRA, etc.), account numbers, status |
| **Transaction History** | Full order history, fills, dividends, corporate actions |
| **Watchlists & Scans** | Access custom watchlists, saved scans, screeners |
| **Trade Execution** *(Agentic Account only)* | Place market, limit, stop, stop-limit, trailing stop orders |
| **Order Management** | View open orders, cancel orders, check order status |

### Example Prompts Your Agent Can Execute

```
"Build a portfolio of 10 little-known AI supply chain tickers. Research news, filings, and allocate $50k."
"Buy $100 of ROAR every time it drops 2%+ in a day. Set as standing instruction."
"Rebalance to 20% ROAR / 80% HMNI using limit orders within 0.5% of mid."
"Analyze my portfolio: what risks am I exposed to? Sector concentration? Beta? Correlation?"
"Why is ROAR up today? Pull news, social sentiment, options flow, recent quotes — bull vs bear thesis."
"Set a trailing stop loss of 5% on my NVDA position."
```

> ⚠️ **Disclaimer:** These examples are for informational purposes only. Not investment advice. You are responsible for all trades your agent places.

---

## ⚠️ Risks & Responsibilities

| Risk | Details |
|------|---------|
| **You are liable** | All trades placed by your agent are **your responsibility**. Robinhood executes on your instructions. |
| **Auto-trading danger** | If you configure your agent to trade **without confirmation**, it can place orders autonomously. Review before enabling. |
| **Agent errors** | LLMs hallucinate. Your agent may misinterpret data, pick wrong tickers, or size positions incorrectly. |
| **Market risk** | Standard investment risks apply: volatility, liquidity, gaps, halts, extended hours. |
| **Technical risk** | MCP connection failures, API latency, Robinhood outages, authentication expiry. |
| **Regulatory** | Pattern Day Trading rules, margin requirements, account restrictions still apply. |

**Before enabling autonomous trading:**
- Set position size limits (e.g., "max $500 per trade")
- Set daily loss limits (e.g., "stop if down $1,000/day")
- Require confirmation for orders > $X
- Monitor daily via Robinhood app
- Read [Robinhood Agentic Trading Disclosures](https://robinhood.com/legal/agentic-trading-disclosures)

---

## 🔐 What Your Agent Can Access (Read-Only)

When you connect, the MCP grants your agent **read access** to:

- ✅ All your Robinhood accounts (including account numbers)
- ✅ All positions & balances (real-time)
- ✅ All transactions & order history
- ✅ All watchlists & saved scans

**Important:** Your agent can **only place trades in your Robinhood Agentic account** — not your primary or other accounts.

---

## 🚀 Quick Start: Open an Agentic Account

### Prerequisites
1. **Primary Robinhood individual investing account** in good standing
2. **Identity verification** complete
3. **< 10 self-directed individual accounts** total (Agentic counts as one)

### Flow
```
1. Choose your AI platform → 2. Connect MCP → 3. Authenticate with Robinhood
                                          ↓
                              4. Auto-prompted: Open Agentic account
                                          ↓
                              5. Complete onboarding → Done!
```

The Agentic account opens automatically during MCP authentication. No separate application needed.

---

## 📋 Platform Setup Guides

| Platform | Guide | Connection Method |
|----------|-------|-------------------|
| **Claude Code** | [guides/claude-code.md](guides/claude-code.md) | CLI: `claude mcp add` |
| **Claude Desktop** | [guides/claude-desktop.md](guides/claude-desktop.md) | Settings → Connectors → Custom |
| **ChatGPT (Custom GPT)** | [guides/chatgpt.md](guides/chatgpt.md) | Developer Mode → Create App |
| **Codex (Web)** | [guides/codex.md](guides/codex.md) | Settings → MCP Servers → Streamable HTTP |
| **Codex CLI** | [guides/codex-cli.md](guides/codex-cli.md) | CLI: `codex mcp add` |
| **Cursor** | [guides/cursor.md](guides/cursor.md) | Settings → Tools & MCPs → Connect |
| **Grok (xAI)** | [guides/grok.md](guides/grok.md) | Chat → + → Add Connector → Custom |
| **Other MCP Clients** | [guides/other.md](guides/other.md) | Use URL: `https://agent.robinhood.com/mcp/trading` |

---

## 🔗 MCP Endpoint Details

```
URL: https://agent.robinhood.com/mcp/trading
Transport: Streamable HTTP / HTTP
Authentication: OAuth 2.0 (handled via browser during setup)
Scope: read:accounts, read:positions, read:orders, read:watchlists, trade:agentic
```

**Test the endpoint:**
```bash
curl -v https://agent.robinhood.com/mcp/trading
# Should return MCP server info / capabilities
```

---

## 🛡️ Security Best Practices

1. **Use official MCP URL only** — `https://agent.robinhood.com/mcp/trading`
2. **Never share your Robinhood credentials** — OAuth handles auth
3. **Review agent permissions** — Some platforms let you restrict tool access
4. **Enable confirmations** — Require approval for trades > $X
5. **Monitor daily** — Check Agentic account in Robinhood app
6. **Revoke access anytime** — Disconnect MCP in your AI platform settings
7. **Use unique prompts** — "Never trade options. Max position $500. Daily stop-loss $200."

---

## 📁 Repository Structure

```
Dregwise/
├── README.md                    # This file
├── guides/
│   ├── claude-code.md          # Terminal-based Claude
│   ├── claude-desktop.md       # Desktop app
│   ├── chatgpt.md              # Custom GPT / ChatGPT
│   ├── codex.md                # Codex web UI
│   ├── codex-cli.md            # Codex CLI
│   ├── cursor.md               # Cursor IDE
│   ├── grok.md                 # xAI Grok
│   └── other.md                # Generic MCP clients
└── assets/
    ├── architecture.png        # System diagram
    └── flowcharts/             # Setup flow diagrams
```

---

## 🤝 Contributing

This is the official Dregwise documentation for Robinhood Agentic Trading MCP. 

- **Issues:** [GitHub Issues](https://github.com/Dregwise/issues)
- **Discussions:** [GitHub Discussions](https://github.com/Dregwise/discussions)
- **X/Twitter:** [@_DregwiseRh](https://x.com/_DregwiseRh)

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

## ⚖️ Legal Disclaimer

**This documentation and the Dregwise token are independent community projects.** They are not affiliated with, endorsed by, sponsored by, or officially connected to Robinhood Markets, Inc., Robinhood’s MCP products, Anthropic, OpenAI, or any other AI platform provider.

This documentation is provided for educational and informational purposes only. Nothing here constitutes financial, investment, legal, or trading advice. Trading securities, tokens, and digital assets involves substantial risk, and past performance does not guarantee future results. Always do your own research and consult a qualified advisor before making financial decisions.

The authors, contributors, and maintainers are not liable for any financial losses, damages, or consequences arising from the use of this documentation, connected AI agents, or related community-built tools.

---

**Important:** Robinhood’s official MCP offerings are separate from this project. The token, added tooling/tek, and detailed docs here are built by the Dregwise community and are **not endorsed by Robinhood**.

**Community:** [@_DregwiseRh](https://x.com/_DregwiseRh) • Contract: `0x3547ffe3f05a8371f1c37ca0763456969889cf44`
