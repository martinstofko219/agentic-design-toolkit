---
name: storybook-docs
description: Generate Storybook design-system documentation as MDX Docs pages with scaffolded Angular stories and an example plan. Use when a designer or engineer wants to document a component or a foundation (color, typography, spacing, etc.) for Storybook — covering usage, behavior, do's and don'ts, placement, and accessibility, but never specs or measurements. Trigger on "document this component for Storybook", "write the docs page for", "create the MDX for", "document our color/typography/spacing", or any request to turn a design-system component or foundation into Storybook documentation.
---

Your job is to produce design-system documentation for Storybook: an MDX Docs page, the Angular stories that the page embeds as live examples, and a short plan listing the examples to build. You document how a component is used and how it behaves — not how it is built. Anatomy, measurements, redlines, and token-level specs are out of scope; those come from Figma. Keep the writing in the voice of a design-system guideline: clear, prescriptive where it should be, and grounded in why, not just what.

## Before you write

Read the design-system config (see "Configuration" below) to learn the base system, framework, and output paths. If no config exists, create one from the template and confirm the defaults with the user before proceeding.

Establish three things: what you're documenting (a named component, several components, or a foundation topic); whether the user has reference material; and where the output belongs. If the user points you at exported reference markdown — their existing documentation from another platform — read it and reuse its substance, but restructure it to fit the spine below and flag anything missing or contradictory. If there's no reference, write from the base system's published guidance and established design-system practice. Either way, the output structure is the same.

When the request is vague or the component's purpose is unclear, ask a focused question or two before writing rather than guessing. A docs page built on a wrong assumption about what the component is for is worse than no page.

## Configuration

A repo-level config file (`design-system.config.md`, template provided alongside this skill) is the single place that sets the base design system and conventions. Read it every run. It declares the base system (Material Design 3 by default, but it can name any system or "custom"), the component framework, the Storybook version, the accessibility standard to hold the docs to, and the output paths. It also carries prose notes describing where the house system diverges from its base — renamed tokens, added variants, removed patterns, brand rules.

This is what makes the skill portable. The documentation spine never changes; only the base system and the house notes do. When the base is Material, lean on MD3 terminology and patterns. When it's custom or another system, lean on the house notes and general best practice, and don't invent Material-isms that don't apply. If the config and a provided reference disagree, the reference wins for that component and you note the divergence.

## The documentation spine

Every component docs page uses the same top-level skeleton so the library reads consistently. Within that skeleton, include only the sections that are meaningful for the component's archetype — a static display component doesn't need a content-truncation section; a non-interactive one needs less behavior coverage. Decide the archetype first (an input, an action, a navigation element, a selection control, a container or surface, a feedback element, or a data-display element), then let it tell you which conditional sections earn their place. Always include Overview, Usage, Do's and Don'ts, and Accessibility. The rest are included when relevant.

**Overview** — what the component is and the role it plays in the system, in a sentence or two. Frame it in the base system's terms.

**Usage** — when to use it and, just as important, when not to. Describe the purpose of each variant or option at the level of intent, not dimensions — why a designer would reach for one over another.

**Variants and options** — the meaningful variations, described by what they're for and how they differ in behavior or emphasis. Embed an example of each. No measurements.

**Behavior** — states and interaction over time: hover, focus, active, disabled, loading, selected, and the edge cases that quietly break things — empty, error, overflow, very long content, many items. Cover responsiveness where the component adapts.

**Content guidelines** *(when the component carries text)* — labels, capitalization, length, truncation, and voice. Keep it to what affects this component.

**Placement and layout** *(when placement is a real decision)* — where the component belongs on a page, density, what it pairs well with, and what to avoid putting next to it.

**Do's and Don'ts** — a handful of paired recommendations, each with a live example of the right and wrong approach. This is often the most-used section; make the examples specific.

**Accessibility** — keyboard interaction and focus order, screen-reader expectations and roles/labels, color and contrast considerations, and target size. Hold it to the standard named in the config. Be concrete about this component, not generic.

**Related components** — links to neighbors a reader might actually need.

Foundations use a parallel skeleton adapted to the topic: the principles behind it, the scale or set of values and the tokens that name them, usage guidance, do's and don'ts, and accessibility. Document the foundations the system actually has — typically color, typography, spacing, elevation, shape, motion, iconography, and layout/grid, plus any house topics named in the config. Show the values as live examples rendered from the tokens, not as a measurements table.

## Stories and embedding

Examples in the docs must be real, rendered Storybook stories — not screenshots or code blocks. Author them as Angular CSF stories (Component Story Format 3) for Storybook 8: a typed `Meta` default export naming the component, with a named export for each example you document. Use `args` for simple prop-driven variations and a `render` function with a `template` (plus `moduleMetadata` for any required imports) when an example needs composition or surrounding markup. Name stories after what they demonstrate — the variants, the states, and the right/wrong pairs from Do's and Don'ts — so the docs read clearly and every documented example maps to a story.

Attach the docs page to those stories with MDX Docs blocks. Import the stories module and the blocks you need, place `<Meta of={...} />` at the top to bind the page, and embed each example with `<Canvas of={Stories.ExampleName} />` in the section that discusses it. The rule to hold: every `<Canvas>` in the MDX must resolve to a story that actually exists in the stories file. Don't reference examples you haven't scaffolded.

## Output locations

Custom components keep all Storybook content in a `stories/` subfolder inside the component's own folder. Write the component's docs MDX, its stories file, and its example plan there. Default/base components share a single common stories folder (named in the config — `mdc-core/stories` in the current setup) where stories sit as flat files named per component; put that component's docs MDX and example plan in the same flat folder, named to match. Foundations live alongside the base components in that same shared stories folder. When in doubt about a path, read it from the config rather than assuming, and confirm with the user if the component type is ambiguous.

The example plan is a short markdown file, one per component or foundation, listing every story to build and mapping each to the docs section that embeds it. It's the spec the stories implement and a checklist for whoever maintains the examples later. Keep it terse — a table or tight list of story name, what it shows, and which section uses it.

## What to avoid

No anatomy diagrams, no measurements, no spacing or sizing values, no redlines, no token-value tables presented as specs — those belong in Figma and the design tokens themselves. Don't pad pages with sections that don't apply to the component just to make every page look identical; consistency comes from the spine and the section order, not from forcing empty sections. Don't invent variants, states, or guidance that the system doesn't actually have — if you're unsure whether something exists, ask or mark it as a gap rather than fabricating it. Don't restate the base system's generic documentation verbatim; document this system's instance of the component.

## Before you finish

Verify that every `<Canvas of={...}>` in the MDX resolves to a real story export, that the page follows the spine and section order, that no measurement or anatomy content slipped in, and that the accessibility section is specific to this component and meets the configured standard. Confirm the files landed in the right location for the component's type. List for the user what you produced and what examples the plan still expects a human to flesh out, if any.
