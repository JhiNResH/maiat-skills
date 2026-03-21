# Maiat Skills

[Agent Skills](https://agentskills.io) for **trust verification** in agentic commerce — check agent reputation, token safety, and rug pull risk before any transaction.

Maiat indexes 18,600+ agents on Base and provides trust scores, behavioral analysis, and community sentiment via free and x402-paid APIs.

## Install

```bash
npx skills add JhiNResH/maiat-skills
```

Install specific skills:

```bash
npx skills add JhiNResH/maiat-skills --skill maiat-trust-check
```

Install globally (available across all projects):

```bash
npx skills add JhiNResH/maiat-skills --global
```

Works with Claude Code, Cursor, Windsurf, Codex, and [40+ other agents](https://github.com/vercel-labs/skills#supported-agents).

## Skills

| Skill | Description | Price |
|-------|-------------|-------|
| [maiat-trust-check](skills/maiat-trust-check) | Check agent/token trust score before transacting | Free or $0.02 |
| [maiat-token-safety](skills/maiat-token-safety) | Detect honeypots, high-tax tokens, rug pulls | Free or $0.01 |
| [maiat-agent-reputation](skills/maiat-agent-reputation) | Full agent reputation profile + community sentiment | $0.03 |

## How it works

1. Agent receives a task involving a swap, transfer, or agent interaction
2. Before executing, the agent calls Maiat's API to check trust
3. If verdict is `avoid` → agent warns the user and stops
4. If verdict is `proceed` → agent continues with the transaction

## APIs

| Endpoint | Price | Method |
|----------|-------|--------|
| `app.maiat.io/api/v1/trust` | Free | GET |
| `app.maiat.io/api/x402/trust` | $0.02 USDC | GET |
| `app.maiat.io/api/x402/token-check` | $0.01 USDC | GET |
| `app.maiat.io/api/x402/token-forensics` | $0.05 USDC | POST |
| `app.maiat.io/api/x402/reputation` | $0.03 USDC | GET |
| `app.maiat.io/api/x402/register-passport` | $1.00 USDC | POST |

All x402 payments in USDC on Base. Free endpoints have rate limits.

## Links

- **App**: https://app.maiat.io
- **SDK**: `npm install @jhinresh/maiat-sdk`
- **MCP Server**: https://app.maiat.io/api/mcp
- **GitHub**: https://github.com/JhiNResH/maiat-protocol
