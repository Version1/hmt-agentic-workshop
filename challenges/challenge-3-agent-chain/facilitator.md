# Facilitator Notes — Challenge 3: Agent Chain

## Time

~10 minutes total (split across pre-staged and live steps).

## Quick run (single command)

To run the full pipeline in one step, type in Copilot Chat (Agent mode):

```
/pipeline-orchestrator
```

The orchestrator runs all three phases — ingestion, visualisation, and analyst review — without stopping for confirmation between steps. All seven output files are written to `outputs/` in a single pass.

Use this to reset the `outputs/` directory before a demo, or when you want to see the full pipeline output immediately without narrating each handoff.

---

## Step-by-step walkthrough (teaching mode)

The steps below show how to run each agent individually. Use this format when you want to narrate the handoff between agents live.

### Step 1: Pre-staged ingest (2 min)

Before the session, run `/data-ingestor` so that `outputs/data_summary.json` and `outputs/ingest_report.md` already exist.

During the demo:
1. Open `outputs/data_summary.json` — point to the anomaly flags (TCA August spike, SWA missing GDP value).
2. Open `outputs/ingest_report.md` — read one sentence showing it's written for non-technical readers.
3. Show the handoff instruction at the bottom of the agent file: "the next step is to use `/data-visualiser`".

### Step 2: Live visualisation (5 min)

1. In Copilot Chat (Agent mode), type: `/data-visualiser`
2. Watch it read the JSON, write a Python script, and run it.
3. Open `outputs/expenditure_chart.html` in a browser — the live chart with red markers on anomalies is the payoff.
4. Pause. Let the room see the chart.

### Step 3: Analyst review (2–3 min, live or pre-staged)

1. Type `/analyst-review` (or show pre-generated output if time is short).
2. Open `outputs/analyst_commentary.md` — read the anomalies section aloud.
3. Point out: the same anomalies the chart highlighted are now in plain English for a non-technical reader.

### Wrap (under 1 min)

Show the `outputs/` directory with all files. Summarise: one initial instruction, three agents, three formulaic steps, no manual work in between.

## Talking points

- **One agent, one job.** Each agent has a single responsibility with clear inputs and outputs.
- **Handoff is explicit.** The agent file names the next agent. Copilot makes it available. The human confirms.
- **Human stays in control.** Every handoff requires approval. This is intentional for government contexts.
- **Context isolation.** Each agent works in its own context — the pipeline stays clean.
- **This is the mapping from Slide 7 made real.** Three formulaic tasks, three agents.

## The dataset

536 rows covering DSA, SWA, and TCA from 1995-01 to 2023-12. The demo focuses on the 2023 portion (36 rows across 3 departments). Two deliberate anomalies:
- **TCA August 2023 spike**: £5,400m vs average £4,370m (23.6% above)
- **SWA August 2023 missing GDP**: `gdp_growth_pct` is blank

## Pre-flight checklist

> **If cloning fresh on demo day:** run `/data-ingestor` before presenting to populate the `outputs/` directory. Step 1 of the demo depends on those files existing.

- [ ] Python environment has `plotly`, `pandas`, `kaleido` installed
- [ ] Agent 1 has been pre-run — `outputs/data_summary.json` and `outputs/ingest_report.md` exist (or run `/pipeline-orchestrator` to skip manual pre-staging)
- [ ] Recording fallback is ready in case of connectivity issues

## Expected output

See `solution/` for example `data_summary.json` and `analyst_commentary.md`.
