# Spectra

**AI Agent Monitoring & Anomaly Detection for Solana**

> "x402 processed 100M+ payments in 6 months. AI agents are now spending real money autonomously. But there's no oversight layer—no one knows when an agent goes rogue until it's too late."

Spectra is the monitoring layer that makes deploying autonomous AI agents safe. It watches agent wallets on Solana in real time, learns each agent's normal behaviour, classifies it, and raises an alert (or pulls the kill switch) the moment an agent starts acting out of character.

**Live demo:** https://spectra-prod-gamma.vercel.app/

---

## The Problem

As AI agents begin transacting autonomously via x402 and other protocols, businesses face a critical gap:

- **No visibility** into what agents are doing in real time
- **No alerts** when agents behave anomalously
- **No audit trail** for compliance and debugging
- **No kill switch** when things go wrong

One rogue agent can drain a treasury in minutes. Spectra prevents that.

---

## What Spectra Does

```
Agent wallet ──▶ Solana RPC / WebSocket ──▶ Transaction parser ──▶ Supabase
                                                                      │
                                       real-time subscription ◀───────┘
                                                  │
                                                  ▼
                       Dashboard: baseline → risk score → behaviour class
                                                  │
                                 Anomaly ──▶ Discord alert + kill switch
```

### Core Features

| Feature | Description |
|---------|-------------|
| **Real-Time Surveillance** | Subscribes to agent wallets over Solana RPC WebSockets and parses transfers, swaps, and x402 payments |
| **Behaviour Classification** | Scores each agent against its own baseline and labels it conservative, aggressive, anomalous, rogue, or dormant |
| **Anomaly Detection** | Frequency and spending-velocity analysis over rolling windows catches spam loops and treasury drains |
| **Alerting** | Discord webhook alerts plus in-dashboard notifications |
| **Kill Switch** | Pause an agent instantly when it misbehaves |
| **Live Dashboard** | Multi-agent fleet view with live trade feed via Supabase real-time subscriptions |
| **Rogue Simulation** | "Force anomaly" and bad-trade injection to demo and test thresholds deterministically |
| **Terminal UI** | A Textual-based TUI that mirrors the dashboard in your terminal |
| **Docs & SDK** | Built-in documentation site and SDK reference |

---

## Target Users

1. **Crypto Trading Firms** - Quant shops deploying AI trading agents
2. **DeFi Protocols** - Teams running automated yield/liquidation bots
3. **x402 API Providers** - Companies with AI agents as customers
4. **DAOs** - Organizations using AI for treasury management
5. **Enterprise/Fintech** - Regulated firms requiring compliance oversight

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Web app | Next.js 16 (App Router), React 19, TypeScript |
| UI | Tailwind CSS 4, shadcn/ui, Motion, GSAP, Three.js / OGL WebGL effects |
| Blockchain | Solana (`@solana/web3.js`, `@solana/spl-token`), x402 |
| Database & auth | Supabase (Postgres, Auth, real-time subscriptions) |
| Alerts | Discord webhooks |
| Docs | Fumadocs (MDX) |
| Terminal UI | Python, Textual, Rich, httpx |
| Hosting | Vercel |

---

## Getting Started

### Web app

```bash
cd spectra
npm install          # also generates the Fumadocs content index
npm run dev          # http://localhost:3000
```

Create `spectra/.env.local`:

| Variable | Purpose |
|----------|---------|
| `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Supabase project (`agents` and `trades` tables) |
| `SOLANA_RPC_URL`, `NEXT_PUBLIC_SOLANA_RPC_URL` | Solana RPC endpoint (e.g. devnet or a provider URL) |
| `DISCORD_WEBHOOK_URL` | Channel webhook for anomaly alerts |
| `SPECTRA_API_KEY` | API key shown in the SDK example |

### Terminal UI

```bash
cd spectra-tui
pip install -e .
SPECTRA_API_URL=http://localhost:3000 spectra
```

The TUI reads from the web app's `/api/dashboard` endpoint. See [`spectra-tui/README.md`](spectra-tui/README.md) for options and keyboard shortcuts.

---

## Repository Structure

```text
spectra/                 Next.js web app
  app/                   Landing, dashboard, docs, SDK, pricing, auth pages
  app/api/               alerts, dashboard, search, solana/monitor, solana/transaction
  lib/solana/            RPC connection, wallet monitor, transaction parser
  lib/supabase/          Browser and server clients
  content/docs/          Documentation (MDX)
spectra-tui/             Python Textual terminal dashboard
docs/                    Architecture, MVP scope, market research, pitch
FEATURE_VERIFICATION.md  Feature-by-feature implementation check
```

---

## Hackathon

Built for **uOttaHack 8**.

### Team
- Angus
- Kabith
- Rohan
- David
