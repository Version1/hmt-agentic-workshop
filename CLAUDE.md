# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A workshop repository for a 45-minute HM Treasury session on **Agentic Workflows with GitHub Copilot**. It contains three progressive challenges demonstrating the skill → single agent → agent chain progression, plus the facilitator brief (`hmt-agentic-workflows-brief-45min.md`).

## Setup

- VS Code with GitHub Copilot (Agent mode enabled)
- Python 3.10+
- For Challenge 3: `pip install plotly pandas kaleido`

## Repository structure

Each challenge is self-contained under `challenges/`:

```
challenge-1-skill/          # Skill: data-profiler invoked on demand
challenge-2-single-agent/   # Agent: DataCleanerAgent takes action and writes output
challenge-3-agent-chain/    # Agent chain: data-ingestor → data-visualiser → analyst-review
```

Within each challenge:
- `.github/skills/` or `.github/agents/` — the Copilot skill/agent definition files
- `data/` — input CSV
- `solution/` — reference output
- `outputs/` (challenge 3 only) — written by agents at runtime

## Architecture: skills vs agents

**Skills** (`.github/skills/*.md`) are reusable instruction recipes. They run when invoked and produce output in-chat. They do not write files unless asked.

**Agents** (`.github/agents/*.agent.md`) take action: read files, run code, write outputs. Invoked as `/agent-name` in Copilot Chat (Agent mode). Each agent file defines its role, expected inputs, outputs, and the next agent to hand off to.

**Agent chain (Challenge 3)** is three agents in sequence:
1. `/data-ingestor` → reads `data/hmt_monthly_expenditure.csv`, writes `outputs/data_summary.json` and `outputs/ingest_report.md`
2. `/data-visualiser` → reads `outputs/data_summary.json`, writes a Python Plotly script, runs it, produces `outputs/expenditure_chart.html` and `.png`
3. `/analyst-review` → reads the three output files, writes `outputs/analyst_commentary.md`

Handoff is explicit: each agent file instructs Copilot to name the next agent; the human confirms each step.

## Challenge 3 conventions

- All code must be Python using pandas and Plotly.
- All outputs go to `outputs/`.
- Written commentary must be in British English.
- The dataset is entirely fictitious — never use real HMT data.

## Demo pre-flight (Challenge 3)

Pre-run `/data-ingestor` before presenting so `outputs/data_summary.json` and `outputs/ingest_report.md` exist. The demo starts from those pre-staged outputs and runs `/data-visualiser` live. Confirm `kaleido` is installed — the PNG export step fails without it.
