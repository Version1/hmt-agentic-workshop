# Facilitator Notes — Challenge 2: Single Agent

## Time

~5 minutes live.

## What to show

1. Open VS Code with this folder as the workspace root.
2. Open `data/messy_expenditure.csv` — briefly scroll to show the audience the variety of problems (mixed date formats, sentinel nulls, formatting noise, category inconsistencies, duplicate rows).
3. Open Copilot Chat in Agent mode.
4. Type: `/data-cleaner`
5. Watch the agent:
   - Read the CSV and scan all 1,010 rows
   - Identify each category of issue and log counts
   - Write a cleaned CSV and a detailed report
6. Open `solution/cleaning_report.md` — show what it caught and fixed.

## Talking points

- **The agent takes action.** It didn't just tell you what's wrong — it fixed the file.
- **Single responsibility.** One job: clean this dataset. Clear inputs, defined outputs.
- **Transparent.** The report shows every decision. You can audit what it did.
- **Repeatable.** Run this on next month's file with zero changes.
- **Next step:** What if you chained multiple agents together? That's Challenge 3.

## The messy data — issue categories

The dataset contains ~1,010 rows across 10 fictitious departments (2022–2024). All department names are synthetic — no real government data is used.

| Issue type | What it looks like | Approx. count |
|------------|-------------------|---------------|
| Missing values — blank | Empty cell | ~50 cells |
| Missing values — sentinel | `NULL`, `N/A`, `n/a`, `#N/A`, `-` | ~40 cells |
| Malformed dates | `2023/05`, `Sep-2023`, `2022-6`, `2024-07-01` | ~80 rows |
| Expenditure formatting | `£4200`, `"4,200"`, `4200M`, `4200 ` | ~60 cells |
| Negative expenditure | `-3200` (sign-flip data entry error) | ~10 rows |
| Out-of-range GDP growth | `150`, `-99` | ~8 rows |
| Category inconsistencies | `Welfare`, `WELFARE`, `welfare benefits`, `welfare_benefits` | ~70 cells |
| Whitespace / case in dept name | ` RCA`, `rca`, `Revenue Collections Agency` | ~55 cells |
| Exact duplicate rows | Identical rows (re-submitted extracts) | ~200 rows |
| Near-duplicate rows | Same dept/month, expenditure off by ≤10 | ~150 rows |
| GDP drift duplicates | Same dept/month, GDP off by ≤0.2 | ~300 rows |

## Departments in the dataset

| Code | Full name | Category |
|------|-----------|----------|
| RCA | Revenue Collections Agency | tax_collection |
| SBD | Social Benefits Directorate | welfare |
| NDO | National Defence Office | defence |
| ITB | Infrastructure & Transport Bureau | infrastructure |
| HSE | Health Services Executive | health |
| ESA | Education Standards Authority | education |
| HCD | Housing & Communities Directorate | housing |
| DTO | Digital & Technology Office | digital |
| EPB | Environment Protection Bureau | environment |
| JCS | Justice & Courts Service | justice |
