# HMT Training Session: Agentic Workflows with GitHub Copilot

**Session title:** Building Agentic Workflows with GitHub Copilot
**Audience:** HM Treasury — data scientists, data analysts, developers (mixed AI experience)
**Duration:** 45 minutes (30-minute presentation + 15-minute Q&A)
**Primary IDE:** VS Code (JetBrains notes throughout)

---

## Audience context

HMT's team spans data scientists who build analytical tools, data analysts who interpret spending and economic data, and developers who build services. AI experience varies. Some attendees use Copilot for autocomplete only, some for chat prompting, a few are already in Agent mode. Frame every concept through data work, not software engineering, because analysts are the majority and need to see themselves in the examples.

---

## Workshop thesis

Data scientists lose a large share of their working time to preparation, cleaning, and repetitive checks. Commonly cited as roughly 45% on data preparation and cleaning

Much of that time goes on tasks that follow explicit rules: profiling columns, flagging nulls, running the same exploratory analysis scripts, grid-searching hyperparameters, and writing the same monitoring checks. Anything rule-followable is automatable. Skills and agents are the two mechanisms to automate it: a skill captures a reusable recipe, an agent takes action and chains steps. The session shows where each fits and demonstrates one worked pipeline.

---

## Concept framing

### Skills, briefly

Agent Skills are reusable, focused instruction sets for a single repeatable task, stored as Markdown and picked up automatically from locations such as `.github/skills/`. The team has met these already, so treat them as the foundation the session builds on, not new material.

The one line to land: a skill is a task recipe; an agent is a teammate with a role and a toolset that can pull in skills as it works.
https://github.com/github/awesome-copilot - community-created collection of custom agents, instructions, skills, hooks, workflows, and plugins to supercharge your GitHub Copilot experience.

### Agent files as specialist agents

Copilot supports custom agent definitions at `.github/agents/*.agent.md`. Each file defines one agent: its task, persona, inputs, outputs, and which agent (if any) takes over next. Once committed, the agent is available as a slash command; any team member invokes it by typing `/agent-name` in Copilot Chat in Agent mode.

### Agent handoff

In Agent mode, Copilot can see all agents defined in `.github/agents/`. An agent file can instruct Copilot to finish its task and then name the next agent. Copilot makes that agent available and the human confirms each handoff before it proceeds. This is the orchestration model: a chain of specialists, each scoped to one job, each handing off cleanly. A useful side effect is context isolation. A handed-off agent works in its own context so the main thread stays focused.

---

## Session structure (45 minutes)

| Block | Time | Content |
|---|---|---|
| Skills recap (light) | 0–5 min | Skills as the foundation, fast pivot to agents |
| Agent files, handoff, design | 5–13 min | How to build and chain specialist agents |
| Where the time goes | 13–18 min | Formulaic work, skill vs agent mapping |
| Demo: Spending Trends Pipeline | 18–28 min | Three-agent workflow, semi-staged |
| Wrap-up and what to try | 28–30 min | One agent, one job, this week |
| Q&A | 30–45 min | |

---

## PPT section guide

Approximately 9 to 10 content slides. One idea per slide. Favour diagrams and annotated screenshots over bullet lists.

---

### Slide 1 — Title slide

**Title:** Agentic Workflows with GitHub Copilot
**Subtitle:** Building AI pipelines that do the heavy lifting
**Facilitator note:** Open by asking how the room currently uses Copilot. Expect a mix of autocomplete and basic chat. Do not grade responses. Use it to calibrate, then move on.

---

### Slide 2 — From skills to agents (light recap)

**Heading:** You have skills. Now meet agents.

**Content to convey:** Acknowledge the earlier skills introduction. Recap in one breath: a skill is a reusable instruction set for one repeatable task. Then draw the line to today: an agent is a teammate with a defined role that does work, takes action, and can use skills along the way. Keep this to a minute or two. The session is about agents.

**Visual suggestion:** Two cards side by side. Left "Skill: a task recipe", one example line. Right "Agent: a teammate with a job", one example line. Arrow from skill to agent labelled "agents use skills".


---

### Slide 3 — What agents do

**Heading:** Agents take action, we do shoulder surfing

**Content to convey:** Agent mode lets Copilot read and edit multiple files, run terminal commands, observe the results of its own actions and adjust, and work iteratively until done. None of this happens automatically in chat. Frame for analysts: an agent can read a CSV, clean it, write a visualisation script, run it, and report back from a single instruction.

**Visual suggestion:** Icon-based capability list, one line each. Keep it clean.

---

### Slide 4 — Agent files: a job description for your agent

**Heading:** Agent files are briefing documents

**Content to convey:** Agent files live at `.github/agents/` with a `.agent.md` extension. Each defines one agent: name, role, inputs, output, and the next agent if any. Once committed, it is available as a slash command and anyone can invoke it with `/agent-name`. This is how a team shares and standardises AI workflows: one person defines the agent, everyone uses it without needing the internals.

**Visual suggestion:** Annotated screenshot of `data-ingestor.agent.md` in VS Code, with callouts on the frontmatter name and description, the role, the input spec, and the handoff line at the bottom. A second callout shows `/data-ingestor` being typed in Copilot Chat.

**JetBrains note:** Works identically. Invoke via `/agent-name`. If the agent is missing from the slash list, confirm `.github/agents/` is committed and the workspace is open at the repository root.

---

### Slide 5 — How agent handoff works

**Heading:** Agents can pass work to other agents

**Content to convey:** In Agent mode Copilot sees all defined agents. An agent file can instruct Copilot to finish, then name the next agent. Copilot makes it available and the human confirms before it proceeds. Emphasise this is not magic: each handoff is written by a human into the agent file. The agent follows instructions; it does not decide to call another agent on its own. Humans design the workflow, Copilot executes it. Add one line on the side benefit: each handed-off agent works in its own context, keeping the main thread clean.

**Visual suggestion:** Horizontal pipeline. DataIngestorAgent → DataVisualiserAgent → AnalystReviewAgent. One-line job under each box. Arrows labelled "handoff instruction in agent file". Mirror the demo.

---

### Slide 6 — Designing a good agent

**Heading:** One job. Clear inputs. Defined output.

**Content to convey:** A good agent has a single, clearly scoped responsibility and knows what it reads, what it produces, and where output goes. If you cannot describe the agent in one sentence, it is doing too much. The three principles:
- **Single responsibility:** one task, not three
- **Explicit inputs:** name the exact file, format, or data to read
- **Defined handoff:** state what to do when finished, including the next agent file if there is one

---

### Slide 7 — Where the time goes

**Heading:** Most data prep follows rules. Rules can be automated.

**Content to convey:** Open with the framing stat: data scientists spend a large share of their time on preparation and cleaning, roughly 45%. Then make the point that lands the whole session: profiling columns, flagging nulls, running the same EDA scripts, grid-searching hyperparameters, and writing the same monitoring checks are formulaic enough to follow explicit rules. Anything rule-followable is a candidate for a skill or an agent.

Give the rule of thumb: if it is a recipe you reuse, it is a skill; if it needs to take action or chain steps, it is an agent.

**Visual suggestion:** A simple split. Left: the formulaic tasks under the heading "Time sinks". Right: the same tasks mapped to "Skill" or "Agent" with a one-word reason. Keep the mapping table (below) as the takeaway slide or handout.

**Task mapping (use as a slide or handout):**

| Formulaic task | Solution | Why |
|---|---|---|
| Column profiling, null and type flagging | **Skill** | A reusable recipe applied on demand to any dataframe |
| Standard EDA scripts (distributions, correlations, summary stats) | **Skill** | Same scaffold every time; capture once, invoke anywhere |
| Recurring data-quality and monitoring checks | **Skill** | Fixed validation rules; consistency matters more than autonomy |
| Hyperparameter grid search | **Agent** | Needs to run code, observe results, and report the best configuration |
| Ingest → clean → flag → summarise | **Agent** | Multi-step, takes action, hands off between specialists (the demo) |
| Drafting plain-English commentary from outputs | **Agent** | Reads several files, produces a written artefact, ends the chain |

**Facilitator note:** Invite the room to name their own formulaic task and decide aloud whether it is a skill or an agent. Two or three examples here make the demo land harder, because the demo is now a worked example of the principle just stated.

---

### Slide 8 — Demo preview

**Heading:** What we are about to build

**Content to convey:** The demo is the mapping made real. The audience will see a three-agent pipeline, the Spending Trends Pipeline, on a sample CSV of anonymised monthly departmental expenditure. Agent one ingests and cleans the data and flags anomalies. Agent two generates a Python Plotly chart. Agent three reads the outputs and writes a plain-English commentary. The only human input is the first instruction, plus confirming each handoff. Point back to Slide 8: each step is a formulaic task now handled by an agent.

**Visual suggestion:** Reuse the Slide 6 pipeline, labelled with specific inputs and outputs. Add an icon for the CSV input and the final commentary output.

---

### Slide 9 — What to try this week

**Heading:** Your starting point

**Content to convey:** Give one concrete, low-risk action. Pick one formulaic task from your own week (reformatting a file, profiling a dataframe, generating a chart, summarising a spreadsheet) and decide: skill or agent. Write the one file for it. No pipeline needed. One job. Share it with the team. Provide the agent file template from the demo as a starting point.

---

## Demo section

### Scenario: Spending Trends Pipeline

A monthly departmental expenditure report arrives as a CSV. Normally an analyst cleans it manually, builds a chart, and writes a commentary. The demo automates all three via a Copilot agent pipeline. It reflects real analyst workflows, not a software engineering example: data scientists recognise the Plotly output, analysts see the commentary as a time saver, developers read the agent file structure immediately. It is also a direct illustration of Slide 8: three formulaic steps, three agents.

### Timing reality and staging (read first)

The full three-agent demo runs to roughly 25 minutes when performed cold. This session allows about 10 minutes. Do not attempt all three live and cold. Recommended staging:

- **Pre-run agent 1 (DataIngestorAgent) before the session** so `outputs/data_summary.json` and `outputs/ingest_report.md` already exist. Show these as the starting point and explain what the agent did.
- **Run agent 2 (DataVisualiserAgent) live.** This is the visual payoff. Let the chart render and pause.
- **Run agent 3 (AnalystReviewAgent) live** if time allows, otherwise show its pre-generated output and read the anomalies section.
- **Record a full clean run as a fallback** in case of connectivity issues. A narrated recording beats a cancelled demo.

This keeps the moment that lands (the live chart with anomalies highlighted) while fitting the slot.

### Demo dataset

Create `data/hmt_monthly_expenditure.csv` with fictitious but plausible figures, roughly 24 rows (two years monthly):

```
month,department,expenditure_gbp_millions,gdp_growth_pct,category
2023-01,HMRC,4200,0.3,tax_collection
2023-01,DWP,8100,0.3,welfare
2023-01,MOD,3600,0.3,defence
...
```

Include two or three deliberate anomalies: a month where one department spikes more than 20%, and one row with a missing `gdp_growth_pct`. These are what agent 1 flags and agent 3 surfaces. The demo is more compelling when the audience sees the agents catch something real.

### Repository structure

```
hmt-spending-pipeline/
  .github/
    agents/
      data-ingestor.agent.md
      data-visualiser.agent.md
      analyst-review.agent.md
    copilot-instructions.md
  data/
    hmt_monthly_expenditure.csv
  outputs/
    (empty before the live portion)
  README.md
```

`copilot-instructions.md` should tell Copilot to use Python, write outputs to `outputs/`, and use British English in any commentary.

---

### Agent 1: DataIngestorAgent

**File:** `.github/agents/data-ingestor.agent.md`
**Purpose:** Read the raw CSV, validate structure, flag anomalies, clean the data, output a structured JSON summary, and hand off to the DataVisualiserAgent. **Pre-run this before the session.**

```markdown
---
name: DataIngestorAgent
description: Reads raw HMT expenditure CSV, validates structure, flags anomalies, and produces a clean structured summary for the visualisation agent.
---

# DataIngestorAgent

You are a data ingestion specialist. Your job is to read, validate, and summarise the raw expenditure data so that downstream agents can work with it reliably.

## Inputs

Read the file at `data/hmt_monthly_expenditure.csv`.

## What to do

1. Load the CSV and check that all expected columns are present: `month`, `department`, `expenditure_gbp_millions`, `gdp_growth_pct`, `category`. If any column is missing, stop and report the issue clearly.

2. Check for missing values in any column. Log any rows with missing values, noting the row number and the column affected. Do not drop these rows — flag them.

3. Check for anomalies in `expenditure_gbp_millions`. Flag any row where a department's expenditure in that month is more than 20% higher or lower than the same department's average across all months. List flagged rows with the actual value and the average.

4. Check that all `month` values are valid dates in the format `YYYY-MM`. Flag any that are not.

5. Produce a clean summary and write it to `outputs/data_summary.json`. The summary should include:
   - Total rows processed
   - Number of rows with missing values (with detail)
   - Number of anomalies flagged (with detail)
   - Department list
   - Date range covered
   - A `cleaned_data` array containing all rows, with a `flagged` boolean and a `flag_reason` string on each row (empty string if not flagged)

6. Write a short plain-English ingest report to `outputs/ingest_report.md` summarising what was found. Write in British English. Use plain language — this report may be read by non-technical colleagues.

## When you are finished

Your work is complete when both output files have been written. Tell the user that the data has been ingested and summarised, and that the next step is to use `/data-visualiser`. Ask the user if they would like to proceed.
```

**Facilitator demo note:** Because this runs before the session, open `outputs/data_summary.json` and `outputs/ingest_report.md` at the start of the demo and narrate what the agent found, pointing at the anomaly flags. Then move to the live visualiser step.

---

### Agent 2: DataVisualiserAgent

**File:** `.github/agents/data-visualiser.agent.md`
**Purpose:** Read the JSON summary, generate a Python Plotly visualisation, write and run it, hand off to the AnalystReviewAgent. **Run this live.**

```markdown
---
name: DataVisualiserAgent
description: Reads the structured data summary and generates a Python Plotly visualisation showing departmental expenditure trends with anomalies highlighted.
---

# DataVisualiserAgent

You are a data visualisation specialist. Your job is to take the cleaned and summarised data and produce a clear, informative Python chart that an analyst can use immediately.

## Inputs

Read `outputs/data_summary.json` produced by the DataIngestorAgent. If this file does not exist, stop and tell the user to run `/data-ingestor` first.

## What to do

1. Read the `cleaned_data` array from the JSON summary.

2. Write a Python script at `outputs/visualise_expenditure.py` that does the following using Plotly:
   - Creates a line chart showing monthly `expenditure_gbp_millions` for each department over time, with one line per department
   - Overlays a secondary y-axis showing `gdp_growth_pct` as a shaded area or bar chart
   - Highlights any rows where `flagged` is `true` with a visible marker (red dot or triangle) on the line
   - Adds a clear title: "HMT Departmental Expenditure vs GDP Growth"
   - Adds axis labels: "Month" on x, "Expenditure (£m)" on primary y, "GDP Growth (%)" on secondary y
   - Adds a legend
   - Saves the chart as an HTML file at `outputs/expenditure_chart.html` using `fig.write_html()`
   - Also saves a static PNG at `outputs/expenditure_chart.png` using `fig.write_image()` for use in reports

3. The script should be runnable with `python outputs/visualise_expenditure.py`. Include any necessary imports. Assume the user has `plotly`, `pandas`, and `kaleido` installed.

4. After writing the script, run it using the terminal. Confirm that both the HTML and PNG outputs have been created.

5. Write a brief note to `outputs/visualisation_notes.md` describing what the chart shows and what the highlighted points represent. Write in British English.

## When you are finished

Your work is complete when the chart files have been generated. Tell the user which files were created and where they can find them. Then tell the user the next step is to use `/analyst-review` and ask if they would like to proceed.
```

**Facilitator demo note:** This is the most visually impressive step. When Copilot runs the script and the HTML chart appears, open it in a browser. The live chart with flagged anomalies highlighted is the moment that lands. Pause and let the room react. **Pre-flight check: confirm `plotly`, `pandas`, and `kaleido` are installed on the demo machine. The PNG step needs `kaleido` and will fail without it.**

---

### Agent 3: AnalystReviewAgent

**File:** `.github/agents/analyst-review.agent.md`
**Purpose:** Read the summary, ingest report, and visualisation notes; write a plain-English analyst commentary for a non-technical audience. **Run live if time allows, otherwise show pre-generated output.**

```markdown
---
name: AnalystReviewAgent
description: Reads the data summary, ingest report, and visualisation notes to produce a plain-English analyst commentary on HMT departmental expenditure trends.
---

# AnalystReviewAgent

You are an experienced government data analyst reviewing departmental expenditure data. Your job is to produce a clear, accurate, and concise commentary that a senior civil servant could read and act on. You do not write for technical audiences.

## Inputs

Read the following files:
- `outputs/data_summary.json` — the structured data summary from the ingest step
- `outputs/ingest_report.md` — the plain-English ingest report
- `outputs/visualisation_notes.md` — the chart description

If any of these files are missing, stop and tell the user which file is absent and which agent to run to produce it.

## What to do

1. Review all three input files.

2. Write an analyst commentary to `outputs/analyst_commentary.md`. The commentary should include the following sections:

   **Summary** — two to three sentences giving the overall picture of departmental expenditure across the period covered.

   **Key trends** — up to five bullet points describing the most significant patterns observed. Each bullet should name the department or period, describe the trend, and state whether it warrants further investigation. Do not use jargon. Write as if explaining to a Minister's private office.

   **Anomalies and flags** — a paragraph describing each flagged row from the data summary. For each anomaly, state: what the figure was, what the expected range was, and what the possible explanations might be. Note any missing data and its potential impact on the analysis.

   **Recommendation** — one short paragraph recommending the next analytical step. This might be requesting further breakdowns, cross-referencing against budget forecasts, or escalating to a named team.

3. Write in British English. Use plain language. Avoid passive voice. Keep sentences short.

4. Do not invent figures. Work only from the data in the input files.

## When you are finished

Tell the user that the commentary has been written and is available at `outputs/analyst_commentary.md`. Tell them that all pipeline outputs are in the `outputs/` directory. This is the end of the pipeline.
```

---

### Demo flow summary for facilitator (about 10 min)

**Step 1 (2 min, pre-staged):** Open the pre-generated `outputs/data_summary.json` and `outputs/ingest_report.md`. Narrate what DataIngestorAgent did, point at the anomaly flags, read one sentence from the ingest report. Show the handoff instruction naming the next agent.

**Step 2 (5–6 min, live):** Invoke DataVisualiserAgent. Show Copilot writing the Python script in real time, then running it in the terminal. Open the HTML chart in a browser and pause. Draw attention to the red markers on the anomalous points. This is the payoff; give the room time.

**Step 3 (2–3 min, live or shown):** Invoke AnalystReviewAgent, or open its pre-generated output. Show it reading the inputs and writing `analyst_commentary.md`. Read the anomalies section aloud. Point out it surfaced the same points the chart highlighted, now in plain English for a non-technical reader.

**Wrap (under 1 min):** Show the `outputs/` directory with all files present. Summarise: one initial instruction, three agents, three formulaic steps, no manual work in between.

---

## Facilitator notes

**On mixed experience:** The PPT carries the lower-experience attendees; the demo will challenge them pleasantly. If someone is clearly lost, offer a one-to-one follow-up rather than pausing the room.

**On remote delivery:** Share screen for the demo. Start from a clean repository: CSV and the pre-staged agent 1 outputs present, the visualiser and review outputs absent. Keep the recording fallback ready.

**On IDE differences:** The JetBrains notes on the slides and steps are enough. If JetBrains users struggle with Agent mode, point to the Copilot Chat panel mode selector and confirm a recent plugin version. Do not spend more than two minutes on IDE troubleshooting; offer follow-up.

**On data sensitivity:** The demo dataset is entirely fictitious. Do not use real HMT data in any demo, even anonymised. If attendees ask about real data, direct them to their data governance team and HMT's data classification policy first.

**On the handoff mechanism:** Some attendees may say this is not "real" multi-agent orchestration because a human confirms each handoff. Acknowledge it directly. The confirmation keeps humans in the loop, which is intentional for a government context. The agent names the next agent, Copilot makes it available, the human approves.

---

## Q&A preparation (15 min)

Seed questions to have ready:

1. **Skill or agent: which do I reach for?** Skill for a single repeatable recipe (profiling, EDA scaffolds, validation rules). Agent when the work needs to take action or chain steps (grid search, ingest pipelines, drafting from outputs).

2. **Which of my own tasks are worth automating first?** Start with the formulaic, rule-followable ones from Slide 8: column profiling, null flagging, repeated EDA, monitoring checks. High frequency, low judgement, fast payback.

3. **Will this work on notebooks, not just repositories?** Agents operate on repository and workspace content. Notebooks committed to a repo are in scope. Be honest about interactive-kernel limits.

4. **How do we stop an agent making changes we did not want?** Scope tightly with single-responsibility agents, name exact inputs, add "do not modify" guards in the prompt, and require human review of any output before it is used.

5. **Is the demo dataset real?** No, entirely fictitious. Real data goes through data governance and HMT's classification policy first.

6. **What if Copilot does not pick up our agent file?** Confirm `.github/agents/` is committed and the workspace is open at the repository root, and that you are in Agent mode.

7. **Can one analyst's agent be shared with the team?** Yes. Agent files are versioned in git like any other code, so a team can maintain a shared library everyone can use.

---

## Resources for FDE

- GitHub Copilot Agent mode documentation: `https://docs.github.com/en/copilot/using-github-copilot/copilot-chat/using-copilot-chat-in-your-ide`
- Agent files (`.github/agents/`) documentation: `https://docs.github.com/en/copilot/customizing-copilot/using-copilot-agents`
- Plotly Python documentation: `https://plotly.com/python/`
- AI Engineering Lab platform: internal repository (confirm URL with Delivery Manager before session)
