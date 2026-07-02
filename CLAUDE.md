# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A workshop demonstrating the **skill → agent → agent chain** progression using GitHub Copilot (Agent mode). It is not a runnable application — it contains agent/skill definition files (`.agent.md`, `SKILL.md`) and CSV datasets. All data is fictitious HMT expenditure data.

## Setup

```bash
pip install plotly pandas kaleido  # required for Challenge 3 chart generation
```

VS Code with GitHub Copilot (Agent mode enabled) is required to invoke the skills and agents.

## Structure

Three self-contained challenge folders under `challenges/`, each with:
- `README.md` — what to do
- `facilitator.md` — demo talking points and timing
- `.github/` — the skill or agent definition files
- `data/` — input CSV
- `solution/` — reference output

Top-level `.github/` mirrors the Challenge 3 agents for reference.

## The three challenges

**Challenge 1 — Skill** (`challenge-1-skill/`): Invoke `data-profiler` skill in Copilot Chat. Profiles a CSV, outputs markdown to chat. No file writes.

**Challenge 2 — Single Agent** (`challenge-2-single-agent/`): Invoke `/data-cleaner`. Reads `data/messy_expenditure.csv`, cleans it, writes `solution/cleaned_data.csv` and `solution/cleaning_report.md`.

**Challenge 3 — Agent Chain** (`challenge-3-agent-chain/`): Three agents in sequence, all writing to `outputs/`:
1. `/data-ingestor` → `outputs/data_summary.json`, `outputs/ingest_report.md`
2. `/data-visualiser` → `outputs/expenditure_chart.html`, `outputs/expenditure_chart.png`, runs `outputs/visualise_expenditure.py`
3. `/analyst-review` → `outputs/analyst_commentary.md`

Run all three in one pass with `/pipeline-orchestrator` (defined in top-level `.github/agents/`).

## Conventions across all agents

- All code must use **Python and pandas**
- All written output uses **British English**
- All outputs go to the `outputs/` directory (Challenge 3) or `solution/` (Challenge 2)
- Do not invent data — missing values are filled using averages from the same dataset

## Challenge 3 demo pre-flight

Before presenting Challenge 3, pre-run `/data-ingestor` so `outputs/data_summary.json` and `outputs/ingest_report.md` already exist. The live demo starts from Step 2 (`/data-visualiser`). Alternatively, run `/pipeline-orchestrator` to populate the full `outputs/` directory in one pass.

The dataset has two deliberate anomalies to surface during the demo:
- TCA August 2023 spike: £5,400m vs average £4,370m (23.6% above)
- SWA August 2023 missing GDP: `gdp_growth_pct` is blank
