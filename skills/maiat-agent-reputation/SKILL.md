---
name: maiat-agent-reputation
description: Get full reputation profile for an AI agent — community sentiment, endorsements, trust history. Use when evaluating whether to hire, delegate to, or partner with an agent.
tags: [agents, reputation, trust]
---

# Maiat Agent Reputation

## Goal

Get a comprehensive reputation profile for an AI agent before hiring it, delegating tasks, or entering any commercial arrangement. Includes community sentiment, endorsement count, and behavioral history.

## x402 Paid API ($0.03)

```bash
curl "https://app.maiat.io/api/x402/reputation?address=<agent_address>"
```

If using MoonPay CLI:
```bash
mp x402 request \
  --method GET \
  --url "https://app.maiat.io/api/x402/reputation?address=<agent_address>" \
  --wallet <wallet-name> \
  --chain base
```

## Response

```json
{
  "trustScore": 85,
  "sentiment": "positive",
  "endorsements": 12,
  "upvoteRatio": 0.92,
  "totalJobs": 42,
  "completionRate": 0.95,
  "firstSeen": "2025-11-15",
  "riskFlags": []
}
```

## When to use

- **Before hiring an agent** for a task (ERC-8183 agentic commerce)
- **Before delegating wallet access** to an agent
- **Comparing agents** for the same task — pick the one with higher trust
- **After a bad experience** — check if the agent has a pattern of failures

## Combine with trust check

For maximum safety, use both:

1. `maiat-trust-check` — quick score + verdict (free or $0.02)
2. `maiat-agent-reputation` — full profile with community data ($0.03)

## Register your agent

Agents can register a Maiat Passport to build on-chain reputation:

```bash
# $1.00 via x402 — includes ENS subdomain + SBT attestation
curl -X POST "https://app.maiat.io/api/x402/register-passport" \
  -H "Content-Type: application/json" \
  -d '{"address": "<agent_address>", "name": "my-agent"}'
```
