# storybook-docs

Turn a design-system component or foundation into Storybook documentation — an MDX Docs page and the Angular stories it embeds as live examples.

---

## Overview

This skill writes design-focused documentation for a Storybook library: how a component is used, how it behaves, where it belongs, what to do and not do, how it works for assistive technology, and how the design maps to code. It deliberately leaves out anatomy, measurements, and redlines — that detail lives in Figma. The result is a consistent set of guideline pages backed by real, rendered examples rather than screenshots.

The pages serve two audiences: people reading Storybook, and AI agents that consume the docs (via the design-system MCP server) to build UI correctly. Prose stays human-readable while symbol names, variant-to-input mappings, and constraints are stated explicitly so an agent can act on them without guessing.

It defaults to Material Design 3 but is pluggable: a repo-level config file sets the base system, so the same skill documents stock Material components, your customized versions, and fully custom components without changing the structure.

---

## When to use it

Reach for it when something in the system needs a docs page. Good triggers include:

- "Document this component for Storybook"
- "Write the MDX docs for the empty-state component"
- "Document our color / typography / spacing foundations"
- "We have Zeroheight markdown for the dialog — turn it into Storybook docs"
- "Write the API docs and coding guidelines for this custom component" (provide the source material)

You can point it at exported reference markdown to reuse existing content, or have it write from scratch.

---

## Setup

Copy `design-system.config.template.md` to the root of your design-system repo as `design-system.config.md` and edit it. It declares the base system (Material 3 by default), the framework, the Storybook version, the accessibility standard, and the output paths, plus prose notes describing where your house system diverges from its base. The skill reads it on every run; if it's missing, the skill will offer to create one.

---

## How to invoke

**In an agent session (Copilot or Claude):** describe what you want documented in natural language. The agent recognizes the intent and runs the skill, asking a focused question or two if the component's purpose or output location is unclear.

**Manually:** add `SKILL.md` as context and name the component or foundation, plus any reference markdown.

---

## What you get

For each component or foundation, two things land in the right place for its type:

- A **docs MDX page** with reference links under the title (the component's Figma frame, plus the Material 3 and Angular Material pages when there's a genuine equivalent — derived and verified, asked for or placeholdered when missing), following a consistent spine — Overview, Usage, Variants, Behavior, Content, Placement, Accessibility, Implementation, Related — including only the sections that apply to the component's archetype. Do/don't guidance isn't a separate section; it's woven into whichever section discusses the relevant use case, with paired right/wrong examples shown inline. The Overview embeds the primary story as a live canvas with an interactive Controls (args) table beneath it, so readers can exercise the component's main props in one place. An Implementation section maps the design to code — which input, class, or token realizes each variant and state, plus the key inputs/outputs and gotchas — derived from the component's actual source, but it appears only when it adds something the rest of the page and stories don't already cover; a page whose examples already make the mapping obvious omits it.
- An **Angular stories file** (CSF3) implementing every example the page embeds via `<Canvas of={...}>`. Every story carries a Dark Mode toggle so examples can be exercised in both themes (do/don't comparisons excepted — they render through a custom Storybook component). Examples that demonstrate an integration pattern worth copying expose their code through whatever code-display mechanism the project sanctions (Storybook's native show-code toggle by default, or a house mechanism named in the config); simple visual variants stay code-free.

Custom components get their files in a `stories/` subfolder inside the component's folder. Base/Material components and foundations go in the shared stories folder named in the config.

When a component's implementation content is substantial — a full API reference, coding guidelines, integration patterns — it moves to a **separate implementation page** (a sibling Docs entry bound to the same stories): import/registration, an API reference generated from the component's Angular metadata via Storybook's `ArgTypes`, enriched by any source material you provide (with mismatches surfaced), and runnable code examples. This is judged by the depth of content not already covered by the docs page, the stories, or upstream documentation — not by component origin. In practice it's usually custom components, since Material-based ones lean on the upstream Angular Material docs already linked from the page.

---

## Good to know

The spine is fixed but the sections flex to the component — a static display element won't carry a content-truncation section, an interactive control will have a fuller behavior section. Consistency comes from the order and the always-present sections (Overview, Usage, Accessibility), not from forcing every page to look identical.

Examples are always real stories, never screenshots, so the docs stay in sync with the components as they change.

---

## Related skills

- **`design-system`** — audit or extend the system before documenting it
- **`accessibility-review`** — run a deeper a11y audit on a component
- **`ux-copy`** — refine the labels and microcopy a component documents
