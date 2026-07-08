# agentic-design-toolkit

Reusable AI skills and agents for design workflows, built for GitHub Copilot and Claude.

## Overview

This toolkit provides composable, prompt-based components for automating design tasks using AI. Skills are scoped to single workflows and written to be invoked directly inside your AI assistant of choice.

## Structure

```
agentic-design-toolkit/
├── skills/                        # Skill prompts for Claude and GitHub Copilot
│   ├── wireframe-design/
│   │   ├── SKILL.md
│   │   └── README.md
│   ├── prototype-design/
│   │   ├── SKILL.md
│   │   └── README.md
│   ├── design-grill/
│   │   ├── SKILL.md
│   │   └── README.md
│   ├── storybook-docs/
│   │   ├── SKILL.md
│   │   └── README.md
│   ├── spec-design/
│   │   ├── SKILL.md
│   │   └── README.md
│   ├── research-synthesis/
│   │   ├── SKILL.md
│   │   └── README.md
│   └── prototype-audit/
│       ├── SKILL.md
│       └── README.md
├── agents/                        # Agent definitions for GitHub Copilot only
├── instructions/                  # VS Code-style instruction files for Copilot
├── .github/
│   └── copilot-instructions.md    # Workspace-level Copilot instructions
└── CLAUDE.md                      # Workspace-level Claude instructions
```

## Skills

Skills are self-contained prompt files that define a single design task. Each skill includes trigger conditions, expected inputs, step-by-step instructions, and output format.

| Skill | Description |
|---|---|
| [wireframe-design](skills/wireframe-design/SKILL.md) | Generate low-fidelity wireframe explorations from a feature brief or design problem |
| [prototype-design](skills/prototype-design/SKILL.md) | Build a realistic, interactive React + Vite prototype from a design concept |
| [design-grill](skills/design-grill/SKILL.md) | Stress-test a design idea through relentless one-at-a-time questioning before committing to a direction |
| [storybook-docs](skills/storybook-docs/SKILL.md) | Turn a design-system component or foundation into Storybook MDX docs and Angular stories |
| [spec-design](skills/spec-design/SKILL.md) | Build production-ready Angular UI pages and sections using the Nextech Design System |
| [research-synthesis](skills/research-synthesis/SKILL.md) | Turn interview transcripts and research notes into a synthesis doc of themes, insights, and recommendations |
| [prototype-audit](skills/prototype-audit/SKILL.md) | Check a prototype against a research synthesis and produce a prioritized implementation plan to close the gaps |

## Agents

Agents are Copilot-specific and invoked via `@agent-name` in Copilot Chat. Each agent lives in its own folder under `agents/` with a `README.md` describing its purpose and behavior.

> No agents have been added yet.

## Platform Support

| Concept | GitHub Copilot | Claude |
|---|---|---|
| Reusable task prompt | `SKILL.md` in `skills/` | `SKILL.md` in `skills/` |
| Named agent | `@agent-name` via `agents/` | Not in scope |
| Workspace instructions | `.github/copilot-instructions.md` | `CLAUDE.md` |

## Contributing

When adding a skill, create a new folder under `skills/` with a `SKILL.md` as the entry point and a `README.md` describing its purpose, trigger conditions, and expected output.

When adding an agent, document it in `agents/<name>/README.md`.
