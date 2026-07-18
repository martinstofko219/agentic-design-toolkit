# agentic-design-toolkit

A collection of agentic AI tools — skills and instructions — focused on design workflows.

## Purpose
This toolkit provides reusable, composable components for automating design-related tasks using AI. All tools are built to work with both Claude (via Claude Code / Cowork) and GitHub Copilot (primary consumer).

## Project Structure
- `skills/` — Skill prompt files shared between Claude and Copilot, each scoped to a single design task or workflow
- `instructions/` — VS Code-style instruction files for Copilot only. Each file uses `applyTo` frontmatter to scope instructions to specific file patterns (e.g., `**/*.ts,**/*.html`). Not loaded by Claude.

## Skill Pipeline
The skills compose into a design workflow. Use this map to route a request to the right skill and to suggest the logical next step; contributors use it to see where a new skill fits.

1. `design-grill` — pressure-test a concept before any design work begins
2. `wireframe-design` — explore structural options as interactive lo-fi wireframes
3. `prototype-design` — build a realistic, interactive React + Vite prototype of the chosen direction
4. `research-synthesis` — distill user research into themes, insights, and prioritized opportunities
5. `prototype-audit` — compare a prototype against a research synthesis; produces a prioritized implementation plan
6. `spec-design` — build production-ready Angular UI from a design, prototype, or audit plan
7. `storybook-docs` — document design-system components and foundations in Storybook

Skills are self-contained and can be invoked at any entry point — not every project touches every stage. Cross-references between skills use the skill's folder name.

## Conventions
- Each skill lives in its own folder under `skills/` with a `SKILL.md` as the entry point and a `README.md` describing its purpose, trigger conditions, and expected output
- Each VS Code instruction file lives under `instructions/` and uses an `applyTo` frontmatter key to scope it to the relevant file patterns
- Skills should be self-contained: clear trigger conditions, a defined input/output contract, and step-by-step instructions
- Write skills to be model-agnostic where possible; note Claude- or Copilot-specific behavior explicitly when it diverges
- Match format to content in skill files: use prose for judgment-heavy guidance where the rationale behind a rule matters, and bullet lists, numbered steps, or checklists for enumerable rules, conventions, sequential workflows, and output templates
- Keep skill instructions concise — the file shares the context window with everything else the agent holds. Assume a capable model: don't explain concepts it already knows, and cut any sentence that doesn't change what the agent would do
- Skill frontmatter descriptions are written in third person and state both what the skill does and when to trigger it, including concrete trigger phrases
- Use progressive disclosure: keep `SKILL.md` focused on instructions, and move bulky reference material (templates, config references, long examples) into companion files in the skill's folder, linked at most one level deep from `SKILL.md`
- A skill's `README.md` is human-facing and never loaded by agents; when `SKILL.md` behavior changes, update the `README.md` in the same commit
- `CLAUDE.md` and `.github/copilot-instructions.md` mirror each other; when workspace conventions change, update both in the same commit
- Angular conventions are intentionally defined in two places — `instructions/angular.instructions.md` (Copilot, file-scoped) and `skills/spec-design/SKILL.md` (both platforms) — because Claude never loads `instructions/`. When Angular conventions change, update both

## Platform Notes
Tools in this repo target two AI platforms with different agent models:

| Concept | GitHub Copilot | Claude |
|---|---|---|
| Reusable task prompt | `SKILL.md` in `skills/` | `SKILL.md` in `skills/` |
| File-scoped code conventions | `instructions/*.instructions.md` with `applyTo` | Not used — skills carry their own conventions |
| Workspace instructions | `.github/copilot-instructions.md` | `CLAUDE.md` |

## Audience
Tools in this repo are consumed by:
- **GitHub Copilot** (primary) — via Copilot Workspace and agent mode
- **Claude** (secondary) — via Claude Code and Cowork

## Contribution
When adding a new skill, follow the existing folder structure and the conventions above: trigger conditions, inputs, step-by-step instructions, and expected output format, with a human-facing `README.md` alongside `SKILL.md`. Note where the skill fits in the Skill Pipeline and cross-reference its neighbors. Before committing a new or changed skill, exercise it against at least one representative prompt to confirm it triggers and behaves as intended.
