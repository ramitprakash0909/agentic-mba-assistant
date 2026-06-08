# 🤖 Agentic MBA Assistant

An **autonomous, multi-agent system** that prepares me for my MBA classes every day — and a
hands-on lab for learning **agentic AI** by building it.

> Every weekday at 7 PM, three scheduled agents wake up on their own, read tomorrow's class
> schedule, find the assigned pre-reads in cloud storage, and write a detailed "Professor Mode"
> study brief for each subject — then leave it as a draft in my inbox. No human in the loop until
> I press send.

**Live Observatory:** _(GitHub Pages link will go here once deployed)_

---

## Why this exists

Two goals at once:
1. **Study smarter** — turn raw pre-reads into tailored, exam-ready analyses automatically.
2. **Learn agentic AI for real** — not a toy demo; a system that actually runs in production daily.

This repo is the **Observatory**: it makes the running agents *legible* — you can see each run's
reasoning trace and the agentic patterns it demonstrates.

## Architecture (at a glance)

```
        ┌─────────────────────────────────────────────────────────┐
        │  3 scheduled agents (7:00 / 7:15 / 7:30 PM IST)          │
        │  load-distributed, round-robin over tomorrow's sessions  │
        └───────────────┬─────────────────────────────────────────┘
                        │ perceive → plan → act
        ┌───────────────▼───────────────┐
        │ Google Calendar  (perception) │  what classes are tomorrow?
        │ Google Drive     (RAG)        │  read the assigned pre-read
        │ Claude (reasoning)            │  generate the analysis
        │ Google Drive     (write)      │  save the study doc
        │ Gmail            (act)        │  create a draft (human-in-the-loop)
        │ This repo        (log)        │  commit a run-trace → Observatory
        └───────────────────────────────┘
```

## Agentic patterns demonstrated

| Pattern | Where it shows up here |
|---|---|
| **Scheduled autonomy** | 3 cron-triggered agents, no human trigger |
| **Tool use** | Calendar / Drive / Gmail via MCP connectors |
| **RAG** | retrieves the actual pre-read from Drive before writing |
| **Planning / decomposition** | filter sessions → map to course → find reading → generate |
| **Multi-agent load distribution** | round-robin split across 3 runs to stay within limits |
| **Idempotency** | skips creating a doc if one already exists for that day |
| **Human-in-the-loop** | outputs are Gmail *drafts*, never auto-sent |
| **Honest sourcing** | flags when a source wasn't found vs. read from file |

## Tech stack (100% free)

- **Brain:** Claude (via Claude Code scheduled routines) — covered by Claude Pro
- **Data/log:** this GitHub repo (agents commit their run-traces here)
- **Dashboard:** static HTML/JS on **GitHub Pages**
- No paid API, no paid hosting.

## Repo layout

```
/                 → README (this file)
/index.html       → the Observatory dashboard (GitHub Pages)
/data/run-log.json→ append-only log of agent runs (committed by the agent)
```

---

_Built by directing Claude Code — learning agentic AI by shipping it._
