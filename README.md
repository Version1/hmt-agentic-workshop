# HMT Agentic Workshop

Three progressive exercises demonstrating the **skill → agent → agent chain** progression using GitHub Copilot in Agent mode.

## Prerequisites

- VS Code with GitHub Copilot (Agent mode enabled)
- Python 3.10+
- `pip install plotly pandas kaleido` (Challenge 3 only)

## The challenges

### Challenge 1 — Skill (~2 min)

A **skill** is a reusable recipe. It runs when you invoke it; it doesn't act autonomously.

Open `challenges/challenge-1-skill/` as your workspace root, then in Copilot Chat (Agent mode):

```
Profile the file data/sample_expenditure.csv
```

The `data-profiler` skill reads the CSV with pandas and outputs a markdown profile — column types, null counts, and basic statistics — directly in chat.

---

### Challenge 2 — Single Agent (~5 min)

An **agent** takes action. It reads files, makes decisions, and writes output.

Open `challenges/challenge-2-single-agent/` as your workspace root, then:

```
/data-cleaner
```

The agent reads `data/messy_expenditure.csv` (~1,010 rows with mixed date formats, sentinel nulls, duplicate rows, and formatting noise), cleans it autonomously, and writes:
- `solution/cleaned_data.csv`
- `solution/cleaning_report.md`

---

### Challenge 3 — Agent Chain (~10 min)

**Chained agents** hand off between specialists. Each agent does one job, produces a defined output, and names the next agent.

Open `challenges/challenge-3-agent-chain/` as your workspace root.

**Step-by-step (teaching mode):**

```
/data-ingestor      → outputs/data_summary.json, outputs/ingest_report.md
/data-visualiser    → outputs/expenditure_chart.html, outputs/expenditure_chart.png
/analyst-review     → outputs/analyst_commentary.md
```

**Full pipeline in one pass:**

```
/pipeline-orchestrator
```

The orchestrator runs all three phases without stopping for confirmation.

> **Demo tip:** Pre-run `/data-ingestor` before presenting so the ingest outputs already exist. The live demo then starts from `/data-visualiser`. The dataset contains two deliberate anomalies: a TCA August 2023 expenditure spike (£5,400m vs average £4,370m) and a missing GDP value for SWA August 2023.

---

## Key concept

A **skill** is a task recipe. An **agent** is a teammate with a job. Skills are building blocks; agents use them and take action. Chain agents together for multi-step workflows where each specialist does one thing well.

---

All data in this repository is fictitious.
