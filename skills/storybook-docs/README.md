# storybook-docs

Turn a design-system component or foundation into Storybook documentation — an MDX Docs page, the Angular stories it embeds as live examples, and a plan of the examples to build.

---

## Overview

This skill writes design-focused documentation for a Storybook library: how a component is used, how it behaves, where it belongs, what to do and not do, and how it works for assistive technology. It deliberately leaves out anatomy, measurements, and redlines — that detail lives in Figma. The result is a consistent set of guideline pages backed by real, rendered examples rather than screenshots.

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

For each component or foundation, three things land in the right place for its type:

- A **docs MDX page** with reference links under the title (the component's Figma frame, plus the Material 3 and Angular Material pages when there's a genuine equivalent — derived and verified, asked for or placeholdered when missing), following a consistent spine — Overview, Usage, Variants, Behavior, Content, Placement, Accessibility, Related — including only the sections that apply to the component's archetype. Do/don't guidance isn't a separate section; it's woven into whichever section discusses the relevant use case, with paired right/wrong examples shown inline.
- An **Angular stories file** (CSF3) implementing every example the page embeds via `<Canvas of={...}>`. CSF3 is stable across modern Storybook; the skill reads the Storybook version from the config only to pick version-specific details like the docs-blocks import path.
- An **example plan** — a short markdown file mapping each story to the docs section that uses it, as a spec and a maintenance checklist.

Custom components get all three in a `stories/` subfolder inside the component's folder. Base/Material components and foundations go in the shared stories folder named in the config.

For **custom components only**, when you supply source material — existing coding guidelines, integration notes, or the component's TypeScript — the skill also produces a **separate developer docs page**: import/registration, an API reference (inputs/outputs generated from the component's Angular metadata via Storybook's `ArgTypes`, enriched with your provided context, with any mismatches surfaced), coding guidelines and patterns, and runnable code examples bound to the same stories. Material/base components rely on the upstream library's API docs and don't get this page.

---

## Good to know

The spine is fixed but the sections flex to the component — a static display element won't carry a content-truncation section, an interactive control will have a fuller behavior section. Consistency comes from the order and the always-present sections (Overview, Usage, Accessibility), not from forcing every page to look identical.

Examples are always real stories, never screenshots, so the docs stay in sync with the components as they change.

---

## Related skills

- **`design-system`** — audit or extend the system before documenting it
- **`accessibility-review`** — run a deeper a11y audit on a component
- **`ux-copy`** — refine the labels and microcopy a component documents
