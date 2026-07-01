# Workshop Challenges: Agentic Workflows with GitHub Copilot

Three progressive show-and-tell exercises demonstrating the skill → agent → agent-chain progression.

## The progression

| # | Challenge | Concept | Time |
|---|-----------|---------|------|
| 1 | [Profile This Dataset](challenge-1-skill/) | **Skill** — a reusable recipe invoked on demand | ~2 min |
| 2 | [Clean This Messy File](challenge-2-single-agent/) | **Agent** — takes action, writes output, reports back | ~3 min |
| 3 | [The Full Pipeline](challenge-3-agent-chain/) | **Agent chain** — three specialists, handoff between each | ~10 min |

## How to use

Each challenge folder is self-contained:
- `README.md` — brief description of the challenge
- `facilitator.md` — delivery notes, talking points, and timing
- `.github/` — the skill or agent files (ready to use)
- `data/` — the input dataset
- `solution/` — expected output for reference

## Setup

- VS Code with GitHub Copilot (Agent mode enabled)
- Python 3.10+
- For Challenge 3: `pip install plotly pandas kaleido`

## Key message

A **skill** is a task recipe. An **agent** is a teammate with a job. Skills are building blocks; agents use them and take action. Chain agents together for multi-step workflows where each specialist does one thing well.
