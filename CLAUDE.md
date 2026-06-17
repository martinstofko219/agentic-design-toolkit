# agentic-design-toolkit

A collection of agentic AI tools — skills, agents, and instructions — focused on design workflows.

## Purpose
This toolkit provides reusable, composable components for automating design-related tasks using AI. All tools are built to work with both Claude (via Claude Code / Cowork) and GitHub Copilot (primary consumer).

## Project Structure
- `skills/` — Skill prompt files for Claude, each scoped to a single design task or workflow
- `agents/` — Agent definitions for GitHub Copilot only. Each agent lives in its own folder with a `README.md` describing its purpose, inputs, and behavior. If a Claude equivalent is ever needed, it will live in a separate top-level folder (e.g. `plugins/`).

## Conventions
- Each skill lives in its own folder under `skills/` with a `SKILL.md` as the entry point and a `README.md` describing its purpose, trigger conditions, and expected output
- Each agent lives in its own folder under `agents/` with a `README.md` describing its purpose, trigger, and expected behavior
- Skills should be self-contained: clear trigger conditions, a defined input/output contract, and step-by-step instructions
- Write skills to be model-agnostic where possible; note Claude- or Copilot-specific behavior explicitly when it diverges
- Prefer prose instructions over bullet lists in skill and agent files — they read better as system prompts

## Platform Notes
Tools in this repo target two AI platforms with different agent models:

| Concept | GitHub Copilot | Claude |
|---|---|---|
| Invokable named agent | `@agent-name` in Copilot Chat (`agents/`) | Not in scope — use a separate `plugins/` folder if needed |
| Reusable task prompt | `SKILL.md` in `skills/` | `SKILL.md` in `skills/` |
| Workspace instructions | `.github/copilot-instructions.md` | `CLAUDE.md` |

## Audience
Tools in this repo are consumed by:
- **GitHub Copilot** (primary) — via Copilot Workspace and agent mode
- **Claude** (secondary) — via Claude Code and Cowork

## Contribution
When adding a new skill, follow the existing folder structure and include: trigger conditions, inputs, step-by-step instructions, and expected output format. When adding an agent, document its Copilot definition in `agents/<name>/README.md`.
