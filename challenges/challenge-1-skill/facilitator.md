# Facilitator Notes — Challenge 1: Skill

## Time

~2 minutes live.

## What to show

1. Open VS Code with this folder as the workspace root.
2. Open Copilot Chat in Agent mode.
3. Point to `.github/skills/data-profiler.md` — show the audience what a skill file looks like (plain markdown instructions).
4. In the chat, type: `Profile the file data/sample_expenditure.csv`
5. Copilot uses the skill to read the CSV, run pandas, and produce a markdown profile.

> **Fallback:** If Copilot answers from general knowledge and ignores the skill file, use the explicit prompt: `Using the data-profiler skill, profile data/sample_expenditure.csv`

## Talking points

- **A skill is a recipe.** It doesn't take action on its own — it runs when you invoke it.
- **Reusable across datasets.** The same skill works on any CSV. No code changes needed.
- **Team-sharable.** Commit the skill file to the repo, anyone can use it.
- **This is a building block.** The next challenge shows what happens when you give an agent more autonomy.

## Expected output

See `solution/profile_output.md` for what the skill produces.
