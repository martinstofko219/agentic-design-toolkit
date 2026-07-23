---
name: storybook-docs
description: Generate design-system documentation for Storybook — an MDX Docs page plus the Angular CSF stories it embeds as live examples. Documents how a component or foundation is used (usage, variants, behavior, content, placement, do/don't guidance, accessibility, implementation mapping) but never specs, anatomy, or measurements. It can also produce a separate implementation page (API reference, coding guidelines) when a component's code-facing content is substantial and not already covered elsewhere in the docs. Use whenever someone wants to document a design-system component or foundation (color, typography, spacing, elevation, motion) for Storybook, or describes the intent — usage guidelines, do's and don'ts, placement rules, or accessibility notes — without naming Storybook or MDX. Don't use it for building a component, one-off stories with no documentation, or general code docs.
---

Produce design-system documentation for Storybook: an MDX Docs page and the Angular stories that the page embeds as live examples. Document how a component is used, how it behaves, and how the design maps to code — not how it is built internally. Anatomy, measurements, redlines, and token-level specs are out of scope; those come from Figma. Write in the voice of a design-system guideline: clear, prescriptive where it should be, and grounded in why, not just what.

These docs serve two audiences at once: people reading Storybook, and AI agents that consume the pages (via the design-system MCP server) to build UI correctly. Write for both — human-readable guideline prose, with symbol names, variant-to-input mappings, and constraints stated explicitly and verbatim so an agent can act on them without guessing. The goals reinforce each other: docs precise enough for an agent are clearer for people too.

## Ground every repo fact in the real files

Every "hard fact" — import paths and package names, component class names and selectors, `@Input`/`@Output`/method/event names, design-token names, and which variants and states actually exist — must be copied verbatim from real source in the repo, never written from memory or inferred from a naming pattern. The authoritative sources are the `*.component.ts` (selector, class name, inputs/outputs, methods, events), the `public-api.ts` / `index.ts` / `ng-package.json` (the public export surface and the package/import path), and the token or theme files (real token names). Existing `*.stories.ts` or docs MDX can show you the project's import *style*, but verify anything you borrow from them against the component source. Match the project's real conventions rather than introducing your own.

If a hard fact can't be verified from a real source, stop and ask the user rather than inventing it — a guessed import looks right and still breaks the build, and one wrong symbol undermines trust in the whole page. The design-guidance prose (when and how to use the component, do's and don'ts, placement, accessibility) is still yours to write, but it must not describe variants, props, states, or behaviors the component doesn't actually have.

## Configuration

A repo-level config file (`design-system.config.md`, template provided alongside this skill) is the single place that sets the base design system and conventions. Read it every run; if it doesn't exist, create one from the template and confirm the defaults with the user before proceeding. It declares the base system (Material Design 3 by default, but it can name any system or "custom"), the component framework, the Storybook version (which determines version-specific details such as the docs-blocks import path), the accessibility standard to hold the docs to, and the output paths. It also carries prose notes on where the house system diverges from its base — renamed tokens, added variants, removed patterns, brand rules.

The documentation spine never changes; only the base system and the house notes do. When the base is Material, lean on MD3 terminology and patterns. When it's custom or another system, lean on the house notes and general best practice — don't invent Material-isms that don't apply. If the config and a provided reference disagree, the reference wins for that component; note the divergence.

## Before you write

Establish three things: what you're documenting (a named component, several components, or a foundation topic); whether the user has reference material; and where the output belongs. If the user points you at exported reference markdown — existing documentation from another platform — read it and reuse its substance, but restructure it to fit the spine below and flag anything missing or contradictory. If there's no reference, write from the base system's published guidance and established design-system practice. Either way, the output structure is the same.

Read the component's own source (per the grounding rules above) before writing anything that references it. When the request is vague or the component's purpose is unclear, ask a focused question or two rather than guessing — a docs page built on a wrong assumption about what the component is for is worse than no page.

## The documentation spine

Every component docs page uses the same top-level skeleton so the library reads consistently. Decide the component's archetype first (an input, an action, a navigation element, a selection control, a container or surface, a feedback element, or a data-display element), then include only the conditional sections that archetype makes meaningful. Always include Overview, Usage, and Accessibility; every other section, Implementation included, has to earn its place.

There is no standalone do's-and-don'ts section. Weave do/don't guidance into the section already discussing the relevant use case — variant choice belongs in Usage or Variants, overflow handling in Behavior, pairing in Placement. Where a point is best made by contrast, embed a paired right/wrong example (two stories shown together) inline next to the guidance it illustrates. Make the examples specific; favor showing the contrast over merely asserting the rule.

**Overview** — what the component is and the role it plays in the system, in a sentence or two, framed in the base system's terms. Embeds the primary (default) story as a live canvas, with the Controls table bound to that same story (`<Controls of={Stories.Default} />`) directly beneath it — this is the canonical interactive playground. Define `argTypes` in the stories file (descriptions, and category grouping where it clarifies) for the primary story's props that aren't self-explanatory, otherwise the table renders as bare prop names. Keep the Controls table here and off all other canvases; add one elsewhere only when the user specifically asks.

**Usage** — when to use it and, just as important, when not to. Describe the purpose of each variant or option at the level of intent, not dimensions — why a designer would reach for one over another.

**Variants and options** — the meaningful variations, described by what they're for and how they differ in behavior or emphasis. Embed an example of each. No measurements.

**Behavior** — states and interaction over time: hover, focus, active, disabled, loading, selected, and the edge cases that quietly break things — empty, error, overflow, very long content, many items. Cover responsiveness where the component adapts.

**Content guidelines** *(when the component carries text)* — labels, capitalization, length, truncation, and voice. Keep it to what affects this component.

**Placement and layout** *(when placement is a real decision)* — where the component belongs on a page, density, what it pairs well with, and what to avoid putting next to it.

**Accessibility** — keyboard interaction and focus order, screen-reader expectations and roles/labels, color and contrast considerations, and target size. Hold it to the standard named in the config. Be concrete about this component, not generic.

**Implementation** *(only when it adds something the rest of the docs don't already cover)* — how the documented design maps to code where that mapping isn't already visible: which input, class, or token realizes each variant and state (e.g. the filled variant is `appearance="filled"`), the key inputs, outputs, and events an integrator actually uses, and gotchas that aren't obvious from the API alone. Before writing it, reread the rest of the page and the stories' code — the other sections and the embedded examples already carry much of this, and an Implementation section that restates what a reader has already seen is padding. Include only the points that are genuinely new; if nothing non-redundant remains, omit the section entirely. Derive what does remain from the component's source and the base library's documentation — the grounding rules above apply, so every symbol and mapping is copied verbatim, never inferred. Keep it a map, not a full API reference; when genuinely new content outgrows the section, move the depth to a separate implementation page (below) and leave a summary here that points to it.

**Related components** — links to neighbors a reader might actually need.

Foundations use a parallel skeleton adapted to the topic: the principles behind it, the scale or set of values and the tokens that name them, usage guidance, do's and don'ts, and accessibility. Document the foundations the system actually has — typically color, typography, spacing, elevation, shape, motion, iconography, and layout/grid, plus any house topics named in the config. Show the values as live examples rendered from the tokens, not as a measurements table.

## Reference links

Directly under the page title — alongside the import statement that binds the stories — include the same short set of links in the same order on every page: the component's Figma frame first, then the Material 3 guideline page, then the Angular Material component page.

For Figma, use the frame the user provides; ask if they haven't given one, and fall back to a clearly-labeled placeholder link so the page still generates and the gap is obvious. For the other two, derive the right page from the component and the base system, and verify the URL actually resolves (or present the candidate for the user to confirm) — documentation sites move, and component names don't map one-to-one between systems. Include them only when the component has a genuine Material 3 / Angular Material equivalent; for a purely custom component, keep only the Figma link. Foundations follow the same pattern: a Figma link, plus the Material 3 page where the topic has a real counterpart.

## Stories and embedding

Examples in the docs must be real, rendered Storybook stories — not screenshots or code blocks. Author them as Angular CSF3 stories: a typed `Meta` default export naming the component, with a named export for each example you document. Use `args` for simple prop-driven variations and a `render` function with a `template` (plus `moduleMetadata` for any required imports) when an example needs composition or surrounding markup. Every story includes a Dark Mode arg — a boolean toggle wired through `argTypes` — so each example can be exercised in both themes. The exception is do/don't comparison stories: those render through the design system's custom do/don't Storybook component and don't take the toggle. Name stories after what they demonstrate. Before scaffolding, plan which examples each section needs so the set is complete and every documented point has a story to back it.

Attach the docs page with MDX Docs blocks: `<Meta of={...} />` at the top to bind the page, and `<Canvas of={Stories.ExampleName} />` for each example in the section that discusses it. Canvases keep Storybook's built-in show-code toggle, so every example's HTML and TypeScript is one click away — don't add expanded code blocks to the design page; expanded `<Source>` blocks belong on the implementation page, where the code itself is the point. Never define stories inline in the MDX — modern Storybook deprecates it — and never reference a story you haven't scaffolded: every `<Canvas>` must resolve to a real export in the stories file. `Meta`, `Canvas`, and `Controls` all come from the same docs-blocks package, whose import path is the one detail that shifts between Storybook major versions — read the version from the config, match whatever the project's existing stories already import when there are any, and flag (rather than guess) if the config's version and the repo's installed Storybook disagree.

Derive the component import from the public API or package definition (`public-api.ts`, `ng-package.json`), not from an existing story; you may mirror a verified existing import style, and ask if nothing verifiable confirms the path.

## When implementation content needs its own page

A component's implementation coverage can outgrow the spine section: a full API reference, coding guidelines, integration patterns, form-control behavior, content-projection slots. When it does — judged by the volume and depth of content the docs page and its stories don't already cover, not by whether the component is custom — move the deep content to a separate implementation page, its own MDX file bound to the same stories with `<Meta of={...} />` so it appears as a sibling Docs entry, and keep the spine's Implementation section as a summary pointing to it. The same redundancy bar applies here as to the section: a page that would mostly re-present the docs page, the stories, or the upstream library's own documentation shouldn't exist. In practice this is usually custom components; a Material-based component's deep API already lives in the upstream Angular Material docs the page links to, so it earns a full page only when the house wrapper meaningfully diverges from upstream.

Cover what an integrator needs: how to import and register the component (module or standalone), the API reference, the coding guidelines and integration patterns, and runnable usage examples. Generate the API reference from the component's Angular metadata with `<ArgTypes of={...} />` (and `<Controls>` where an interactive table helps) — in Angular this pulls descriptions from compodoc, so tell the user if compodoc isn't wired up and fall back to a written table. Derive content from the component's source first; material the user provides (existing coding guidelines, integration notes) enriches it with what metadata can't express — methods, emitted events, content projection slots, form-control integration, usage caveats — and surface any disagreement between that material and the actual metadata rather than silently picking one. Embed code examples with `<Source of={...} />` against the existing stories, or `<Canvas of={...} withSource />` when showing the rendered result and its code together, so snippets stay in sync with the stories rather than drifting as separate copies.

## Output locations

Custom components keep all Storybook content — the design docs MDX, the stories file, and the implementation page MDX when produced — in a `stories/` subfolder inside the component's own folder, with the implementation page named distinctly from the design page. Default/base components and foundations go in the shared common stories folder named in the config (`mdc-core/stories` in the current setup) as flat files named per component, with the docs MDX named to match; an implementation page for a base component, in the rare case one is warranted, lives in that same shared folder. When in doubt about a path, read it from the config, and confirm with the user if the component type is ambiguous.

## What to avoid

No anatomy diagrams, measurements, spacing or sizing values, redlines, or token-value tables presented as specs on the design docs page — those belong in Figma and the design tokens themselves. (The Implementation section and implementation page are the exception and the right home for code contracts — inputs, classes, tokens by name — which are not visual measurements.) Don't pad pages with sections that don't apply; consistency comes from the spine and section order, not from forcing empty sections. Don't invent variants, states, or guidance the system doesn't have — ask or mark it as a gap. Don't restate the base system's generic documentation verbatim; document this system's instance of the component.

## Before you finish

Verify every item before reporting done:

- [ ] Every MDX block reference (`Canvas`, `Controls`, `ArgTypes`, `Source`) resolves to a real story export, and every block used is imported
- [ ] The page follows the spine and section order, with no measurement or anatomy content
- [ ] Overview embeds the primary story with its bound Controls table
- [ ] The accessibility section is specific to this component and meets the configured standard
- [ ] The reference links under the title follow the rules above
- [ ] Every import statement and repo symbol traces to a real file
- [ ] The files landed in the right locations for the component's type
- [ ] Anything unverifiable was raised with the user rather than guessed
- [ ] Implementation content (section or page), if present, says something the rest of the docs and stories don't, and its symbols and variant-to-input mappings are copied verbatim from the component source
- [ ] Every story except do/don't comparisons exposes the Dark Mode toggle
- [ ] Implementation page only: any mismatch between provided material and the component's actual metadata was surfaced

Then list what you produced and note any stubs or incomplete examples a human still needs to flesh out.
