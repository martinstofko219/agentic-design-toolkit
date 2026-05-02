# agentic-design-toolkit

A collection of agentic AI tools — skills, agents, and instructions — focused on design workflows.

## Purpose
This toolkit provides reusable, composable components for automating design-related tasks using AI. GitHub Copilot is the primary consumer. Claude (via Claude Code / Cowork) is secondary.

## Project Structure
- `.github/skills/` — Skill prompt files for GitHub Copilot, each scoped to a single design task or workflow
- `agents/` — Agent definitions for GitHub Copilot. Each agent lives in its own folder with a `README.md` describing its purpose, inputs, and behavior.
- `skills/` — Skill prompt files for Claude (separate from Copilot skills)

## Conventions
- Each Copilot skill lives in `.github/skills/` with a `SKILL.md` as the entry point
- Each agent lives in its own folder under `agents/` with a `README.md` describing its purpose, trigger, and expected behavior
- Skills should be self-contained: clear trigger conditions, a defined input/output contract, and step-by-step instructions
- Prefer prose instructions over bullet lists in skill and agent files — they read better as system prompts

## Platform Notes
Tools in this repo target two AI platforms with different agent models:

| Concept | GitHub Copilot | Claude |
|---|---|---|
| Invokable named agent | `@agent-name` in Copilot Chat (`agents/`) | Not in scope — use a separate `plugins/` folder if needed |
| Reusable task prompt | `SKILL.md` in `.github/skills/` | `SKILL.md` in `skills/` |
| Workspace instructions | `.github/copilot-instructions.md` | `CLAUDE.md` |

## Contribution
When adding a new Copilot skill, add it to `.github/skills/` and include: trigger conditions, inputs, step-by-step instructions, and expected output format. When adding an agent, document its definition in `agents/<name>/README.md`.
