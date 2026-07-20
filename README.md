# agentic-design-toolkit

Reusable AI skills and instructions for design workflows, built for GitHub Copilot and Claude.

## Overview

This toolkit provides composable, prompt-based components for automating design tasks using AI. Skills are scoped to single workflows and written to be invoked directly inside your AI assistant of choice.

## Structure

```
agentic-design-toolkit/
├── skills/                        # Skill prompts for Claude and GitHub Copilot
│   ├── design-grill/
│   │   ├── SKILL.md
│   │   └── README.md
│   ├── wireframe-design/
│   │   ├── SKILL.md
│   │   └── README.md
│   ├── prototype-design/
│   │   ├── SKILL.md
│   │   └── README.md
│   ├── research-plan/
│   │   ├── SKILL.md
│   │   ├── README.md
│   │   └── secondary-methods.md
│   ├── research-synthesis/
│   │   ├── SKILL.md
│   │   └── README.md
│   ├── prototype-audit/
│   │   ├── SKILL.md
│   │   └── README.md
│   ├── spec-design/
│   │   ├── SKILL.md
│   │   └── README.md
│   └── storybook-docs/
│       ├── SKILL.md
│       ├── README.md
│       └── design-system.config.template.md
├── instructions/                  # VS Code-style instruction files for Copilot
├── .github/
│   └── copilot-instructions.md    # Workspace-level Copilot instructions
└── CLAUDE.md                      # Workspace-level Claude instructions
```

## Skill Pipeline

The skills compose into a design workflow, from raw concept to production-ready UI. Each skill is self-contained and can be invoked at any entry point — not every project touches every stage.

```
design-grill → wireframe-design → prototype-design → research-plan → research-synthesis → prototype-audit → spec-design
```

`storybook-docs` sits outside the pipeline — a standalone skill for documenting the design system itself.

| Skill | Description |
|---|---|
| [design-grill](skills/design-grill/SKILL.md) | Stress-test a design idea through phased, batched questioning with recommended answers before committing to a direction |
| [wireframe-design](skills/wireframe-design/SKILL.md) | Generate low-fidelity wireframe explorations from a feature brief or design problem |
| [prototype-design](skills/prototype-design/SKILL.md) | Build a realistic, interactive React + Vite prototype from a design concept |
| [research-plan](skills/research-plan/SKILL.md) | Plan a research study — discovery interviews or a prototype-based usability test — co-drafting themes and test scenarios grounded in an analysis of the prototype (React, Angular, HTML, or Figma); surveys, card sorts, and A/B tests supported via a companion reference |
| [research-synthesis](skills/research-synthesis/SKILL.md) | Turn interview transcripts and research notes into a synthesis doc of themes, insights, and recommendations |
| [prototype-audit](skills/prototype-audit/SKILL.md) | Check a prototype — React/Vite, Angular, HTML wireframe, or Figma frames — against a research synthesis and produce a prioritized implementation plan to close the gaps |
| [spec-design](skills/spec-design/SKILL.md) | Build production-ready Angular UI pages and sections using the Nextech Design System |
| [storybook-docs](skills/storybook-docs/SKILL.md) | Turn a design-system component or foundation into Storybook MDX docs and Angular stories, readable by humans and consumable by AI agents, including design-to-code implementation mapping |

Each skill includes trigger conditions, expected inputs, step-by-step instructions, and output format.

## Platform Support

| Concept | GitHub Copilot | Claude |
|---|---|---|
| Reusable task prompt | `SKILL.md` in `skills/` | `SKILL.md` in `skills/` |
| File-scoped code conventions | `instructions/*.instructions.md` with `applyTo` | Not used — skills carry their own conventions |
| Workspace instructions | `.github/copilot-instructions.md` | `CLAUDE.md` |

## Contributing

When adding a skill, create a new folder under `skills/` with a `SKILL.md` as the entry point and a `README.md` describing its purpose, trigger conditions, and expected output. Note where the skill fits in the Skill Pipeline and cross-reference its neighbors.

Follow the conventions in [CLAUDE.md](CLAUDE.md) / [.github/copilot-instructions.md](.github/copilot-instructions.md): prose for judgment-heavy guidance, lists for enumerable rules and workflows, concise instructions, and bulky reference material split into companion files. A skill's `README.md` is human-facing and never loaded by agents — keep it in sync whenever `SKILL.md` behavior changes.

Before committing a new or changed skill, exercise it against at least one representative prompt to confirm it triggers and behaves as intended.
