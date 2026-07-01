# Challenge 1: Skill — Profile This Dataset

A **skill** is a reusable instruction set for a single repeatable task. This skill profiles any CSV file — reporting column types, null counts, and basic statistics. You write it once, anyone on the team can invoke it on any dataset.

## Usage

In Copilot Chat (Agent mode), type:

```
Profile the file data/sample_expenditure.csv
```

The `data-profiler` skill (defined in `.github/skills/data-profiler/SKILL.md`) reads the CSV and produces a markdown profile with column types, null counts, and basic statistics.

See [facilitator.md](facilitator.md) for delivery notes and talking points.
