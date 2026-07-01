# Challenge 3: Agent Chain — The Full Pipeline

**Agent handoff** lets you chain specialist agents into a pipeline. Each agent does one job, produces a defined output, and names the next agent. The human confirms each handoff.

## The chain

| Step | Agent | Output |
|------|-------|--------|
| 1 | `/data-ingestor` | `outputs/data_summary.json`, `outputs/ingest_report.md` |
| 2 | `/data-visualiser` | `outputs/expenditure_chart.html`, `outputs/expenditure_chart.png` |
| 3 | `/analyst-review` | `outputs/analyst_commentary.md` |

## Usage

Run the full pipeline in one step:

```
/pipeline-orchestrator
```

Or run each agent individually in sequence — see [facilitator.md](facilitator.md) for the step-by-step walkthrough, talking points, and pre-flight checklist.
