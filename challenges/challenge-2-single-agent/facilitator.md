# Facilitator Notes — Challenge 2: Single Agent

## Time

~3 minutes live.

## What to show

1. Open VS Code with this folder as the workspace root.
2. Open `data/messy_expenditure.csv` — show the audience the problems (nulls, a bad date format, a duplicate row).
3. Open Copilot Chat in Agent mode.
4. Type: `/data-cleaner`
5. Watch the agent:
   - Read the CSV
   - Identify issues (it will log what it finds)
   - Write a cleaned CSV and a report
6. Open `solution/cleaning_report.md` — show what it caught and fixed.

## Talking points

- **The agent takes action.** It didn't just tell you what's wrong — it fixed the file.
- **Single responsibility.** One job: clean this dataset. Clear inputs, defined outputs.
- **Transparent.** The report shows every decision. You can audit what it did.
- **Repeatable.** Run this on next month's file with zero changes.
- **Next step:** What if you chained multiple agents together? That's Challenge 3.

## The messy data (intentional issues)

| Issue | Location |
|-------|----------|
| Missing `gdp_growth_pct` | Row 2 (HMRC, Feb) |
| Missing `expenditure_gbp_millions` | Row 6 (DWP, Feb) |
| Missing `expenditure_gbp_millions` | Row 14 (second HMRC January entry — missing expenditure) |
| Malformed date `2024/04` | Row 12 (MOD, Apr) |
| Exact duplicate row | Row 13 (MOD, Apr — becomes a duplicate of row 12 after the date is corrected) |

## Expected output

See `solution/` for the cleaned CSV and cleaning report.

**Note:** The cleaned file retains two HMRC January 2024 entries because the source data had two. The agent fills the missing expenditure value (4225) and keeps the row — it does not merge or deduplicate rows that differ in content.
