---
name: maiat-token-safety
description: Check if an ERC-20 token is safe before swapping. Detects honeypots, high-tax tokens, unverified contracts, and rug pull patterns. Use before any token swap or purchase.
tags: [security, defi, tokens]
---

# Maiat Token Safety Check

## Goal

Before swapping or buying any ERC-20 token, verify it's not a honeypot, high-tax token, or rug pull. Returns safety verdict with specific risk flags.

## Free API

```bash
curl "https://app.maiat.io/api/v1/token-check?token=<contract_address>"
```

## x402 Paid API ($0.01)

```bash
curl "https://app.maiat.io/api/x402/token-check?token=<contract_address>"
```

If using MoonPay CLI:
```bash
mp x402 request \
  --method GET \
  --url "https://app.maiat.io/api/x402/token-check?token=<contract_address>" \
  --wallet <wallet-name> \
  --chain base
```

## Response

```json
{
  "safe": true,
  "verdict": "proceed",
  "honeypot": false,
  "highTax": false,
  "verified": true,
  "buyTax": 0,
  "sellTax": 0.01
}
```

## Risk flags

| Flag | Meaning |
|------|---------|
| `honeypot: true` | Cannot sell after buying — **do not buy** |
| `highTax: true` | Buy/sell tax > 10% — likely scam |
| `verified: false` | Contract source not verified on explorer |

## Deep analysis ($0.05)

For suspicious tokens, run deep forensics with Wadjet ML:

```bash
curl -X POST "https://app.maiat.io/api/x402/token-forensics" \
  -H "Content-Type: application/json" \
  -d '{"token": "<contract_address>"}'
```

Returns ML-powered rug pull probability, team wallet analysis, and liquidity lock status.

## When to use

- **Always before swapping** into an unknown token
- **Before adding liquidity** to a new pool
- **When a user asks to buy a meme coin** or new token
- Token safety check costs $0.01 — cheaper than losing funds to a rug pull
