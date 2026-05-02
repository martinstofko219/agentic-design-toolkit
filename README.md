# agentic-design-toolkit

Reusable AI skills and agents for design workflows, built for GitHub Copilot and Claude.

## Overview

This toolkit provides composable, prompt-based components for automating design tasks using AI. Skills are scoped to single workflows and written to be invoked directly inside your AI assistant of choice.

## Structure

```
agentic-design-toolkit/
├── skills/                        # Skill prompts for Claude and GitHub Copilot
│   └── wireframe-design/
│       └── SKILL.md
├── agents/                        # Agent definitions for GitHub Copilot only
├── .github/
│   └── copilot-instructions.md    # Workspace-level Copilot instructions
└── CLAUDE.md                      # Workspace-level Claude instructions
```

## Skills

Skills are self-contained prompt files that define a single design task. Each skill includes trigger conditions, expected inputs, step-by-step instructions, and output format.

| Skill | Description |
|---|---|
| [wireframe-design](skills/wireframe-design/SKILL.md) | Generate low-fidelity wireframe descriptions from a feature brief |

## Agents

Agents are Copilot-specific and invoked via `@agent-name` in Copilot Chat. Each agent lives in its own folder under `agents/` with a `README.md` describing its purpose and behavior.

> No agents have been added yet.

## Platform Support

| Concept | GitHub Copilot | Claude |
|---|---|---|
| Reusable task prompt | `SKILL.md` in `.github/skills/` | `SKILL.md` in `skills/` |
| Named agent | `@agent-name` via `agents/` | Not in scope |
| Workspace instructions | `.github/copilot-instructions.md` | `CLAUDE.md` |

## Contributing

When adding a skill, create a new folder under `skills/` with a `SKILL.md` as the entry point. Include: trigger conditions, inputs, step-by-step instructions, and expected output format.

When adding an agent, document it in `agents/<name>/README.md`.
