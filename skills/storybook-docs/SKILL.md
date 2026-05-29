---
name: storybook-docs
description: Generate Storybook design-system documentation as MDX Docs pages with scaffolded Angular stories and an example plan. Use when a designer or engineer wants to document a component or a foundation (color, typography, spacing, etc.) for Storybook — covering usage, behavior, do's and don'ts, placement, and accessibility. For custom components it can also produce a separate developer docs page with the API reference and coding guidelines when source material is provided. Trigger on "document this component for Storybook", "write the docs page for", "create the MDX for", "document our color/typography/spacing", "write the API docs / coding guidelines for this component", or any request to turn a design-system component or foundation into Storybook documentation.
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

## Developer docs for custom components

Custom components often need developer-facing documentation alongside the design guidelines: the component's API and the coding guidelines for using it. Produce this only for custom components, only when the user provides source material for it (existing coding guidelines, integration notes, or the component's TypeScript), and keep it on a separate page from the design docs so the two concerns stay distinct. Material/base components rely on the upstream library's own API docs and don't get this page.

Write it as its own MDX file bound to the same stories with `<Meta of={...} />`, so it appears as a sibling Docs entry to the design page. Cover the things an engineer needs: how to import and register the component (module or standalone import), the API reference, the coding guidelines and integration patterns, and runnable usage examples.

For the API reference, draw from both sources and reconcile them. Generate the inputs, outputs, and their types and descriptions from the component's Angular metadata using Storybook's `<ArgTypes of={...} />` (and `<Controls>` where an interactive table helps) — in Angular this pulls descriptions from compodoc, so note in the config or to the user if compodoc isn't wired up, and fall back to a written table sourced from the provided context when it isn't. Enrich the generated reference with anything the metadata can't express — methods, emitted events, content projection slots, form-control integration, and usage caveats — taken from the material the user supplied. Where the provided context and the actual component metadata disagree, surface the mismatch to the user rather than silently picking one.

The coding guidelines themselves come from the source material the user provides: how to wire the component up, common patterns and anti-patterns at the code level, accessibility responsibilities that fall on the consumer, and gotchas. Embed real code examples with `<Source of={...} />` against the existing stories, or `<Canvas of={...} withSource />` when showing the rendered result and its code together, so the snippets stay in sync with the stories rather than drifting as separate copies.

## Output locations

Custom components keep all Storybook content in a `stories/` subfolder inside the component's own folder. Write the component's design docs MDX, its stories file, its example plan, and — when produced — its developer docs MDX there, with the developer page named distinctly from the design page so the two read as separate Docs entries. Default/base components share a single common stories folder (named in the config — `mdc-core/stories` in the current setup) where stories sit as flat files named per component; put that component's docs MDX and example plan in the same flat folder, named to match. Foundations live alongside the base components in that same shared stories folder. When in doubt about a path, read it from the config rather than assuming, and confirm with the user if the component type is ambiguous.

The example plan is a short markdown file, one per component or foundation, listing every story to build and mapping each to the docs section that embeds it. It's the spec the stories implement and a checklist for whoever maintains the examples later. Keep it terse — a table or tight list of story name, what it shows, and which section uses it.

## What to avoid

No anatomy diagrams, no measurements, no spacing or sizing values, no redlines, no token-value tables presented as specs on the design docs page — those belong in Figma and the design tokens themselves. (The developer docs page is the exception and the right home for the technical API; that's specs of a different kind — code contracts, not visual measurements.) Don't pad pages with sections that don't apply to the component just to make every page look identical; consistency comes from the spine and the section order, not from forcing empty sections. Don't invent variants, states, or guidance that the system doesn't actually have — if you're unsure whether something exists, ask or mark it as a gap rather than fabricating it. Don't restate the base system's generic documentation verbatim; document this system's instance of the component.

## Before you finish

Verify that every `<Canvas of={...}>` in the MDX resolves to a real story export, that the page follows the spine and section order, that no measurement or anatomy content slipped in, and that the accessibility section is specific to this component and meets the configured standard. If you produced a developer docs page, confirm its `<Source>`/`<Canvas>` references resolve to real stories, its `<ArgTypes>` binds to a real story, and that you surfaced any mismatch between the provided context and the component's actual metadata rather than burying it. Confirm the files landed in the right location for the component's type. List for the user what you produced and what examples the plan still expects a human to flesh out, if any.
