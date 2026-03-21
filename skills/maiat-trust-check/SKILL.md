---
name: maiat-trust-check
description: Check if an agent or token is trustworthy before transacting. Returns trust score, verdict, and behavioral analysis from 18,600+ indexed agents on Base. Use before any swap, transfer, or interaction with an unknown agent or token.
tags: [security, trust, agents, defi]
---

# Maiat Trust Check

## Goal

Before interacting with any agent or token, check its trust score via Maiat's API. Returns a verdict (proceed/caution/avoid) based on behavioral analysis, completion rates, and on-chain history.

## Free API (no payment required)

```bash
curl https://app.maiat.io/api/v1/trust?address=<address>
```

**Response:**
```json
{
  "trustScore": 85,
  "verdict": "proceed",
  "summary": "Reliable ACP agent — 42 jobs, 95% completion",
  "completionRate": 0.95,
  "totalJobs": 42
}
```

## x402 Paid API (richer data, no rate limit)

```bash
# Requires x402-compatible wallet with USDC on Base
# Price: $0.02 per request
curl https://app.maiat.io/api/x402/trust?address=<address>
```

If using MoonPay CLI:
```bash
mp x402 request \
  --method GET \
  --url "https://app.maiat.io/api/x402/trust?address=<address>" \
  --wallet <wallet-name> \
  --chain base
```

## When to use

- **Before swapping a token** — check if the token contract is safe
- **Before delegating to an agent** — check if the agent has a good track record
- **Before accepting a job from an agent** — verify the buyer's reputation
- **Before any DeFi interaction** — quick safety check

## Decision logic

| Score | Verdict | Action |
|-------|---------|--------|
| 80-100 | `proceed` | Safe to interact |
| 60-79 | `caution` | Proceed with lower amounts, monitor |
| 0-59 | `avoid` | Do not interact |

## Example workflow

1. User says: "Swap 100 USDC for TOKEN_X"
2. **First**, check trust: `curl https://app.maiat.io/api/v1/trust?address=<TOKEN_X_ADDRESS>`
3. If verdict is `avoid` → warn the user and do not proceed
4. If verdict is `caution` → inform user of the risk, ask for confirmation
5. If verdict is `proceed` → execute the swap

## Related endpoints

| Endpoint | Price | Purpose |
|----------|-------|---------|
| `/api/v1/trust` | Free | Basic trust score |
| `/api/x402/trust` | $0.02 | Full trust analysis |
| `/api/x402/token-check` | $0.01 | Honeypot/tax detection |
| `/api/x402/token-forensics` | $0.05 | Deep rug pull analysis |
| `/api/x402/reputation` | $0.03 | Community sentiment |

## Links

- **API Docs**: https://app.maiat.io/api/v1
- **SDK**: `npm install @jhinresh/maiat-sdk`
- **MCP Server**: https://app.maiat.io/api/mcp
