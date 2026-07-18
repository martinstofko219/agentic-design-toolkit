---
name: spec-design
description: Build production-ready Angular UI pages and sections using the Nextech Design System (@nextech/ui-components). Trigger whenever a designer or developer wants to translate a Figma design or React prototype into spec-quality Angular code, build a page or section with the Nextech component library, spec out a page or feature in Angular, or create handoff-ready Angular components with mock data — including when the user provides a Figma link or points to a React prototype and wants it implemented in Angular.
---

# spec-design

This skill guides building production-ready Angular UI — pages, sections, and reusable components — using the Nextech Design System (`@nextech/ui-components`). The output is structured, accessible Angular code with mock data, ready for developers to wire up real API calls and logic.

Design input may come from Figma frames (via the Figma MCP), React prototypes in the workspace, written descriptions, or a combination. The Nextech Design System MCP server is the single source of truth for available components, patterns, and tokens. One invocation typically produces a complete page or a coherent, self-contained section; complex apps are built incrementally, section by section, across multiple invocations.

**Session mode:** Once invoked, this skill stays active for the rest of the session — apply these guidelines to every subsequent build request without re-invocation. On first load, tell the designer the skill is active and remains so until they say "stop spec-design" or "exit skill mode."

---

## Step 1: Verify Prerequisites

Before doing anything else, confirm the required tools and environment are available.

**Nextech Design System MCP** — attempt to call `getComponentDescriptions()`. If it fails or is unavailable, stop and ask the user to install `@nextech/design-system-mcp`; it is required for every build.

**Figma MCP** — needed only if the user provides a Figma link. If a Figma URL is present but the MCP is unavailable, ask for screenshots or a written description instead.

**Angular workspace** — confirm `@nextech/ui-components` is installed and an Angular app shell is running; if not, ask the user to set one up before proceeding.

---

## Step 2: Understand the Design Input

Gather and synthesize all available design references before writing any code.

**If the concept itself is unclear** — the problem being solved, who the user is, what the layout or behavior should be — suggest running the `design-grill` skill before building, regardless of what artifacts are provided: a vague description, a low-fidelity sketch without interaction notes, or a Figma frame that doesn't communicate intent all qualify. A spec-quality implementation built on an unclear concept is expensive to rework; if you can't yet make confident decisions about component structure and behavior, grill first.

**If the concept is clear**, proceed with whatever design artifacts are available:

**Figma link provided** — use the Figma MCP to pull design context: layout structure, component usage, spacing, typography, color, and any interaction or annotation notes. Component names in Figma often map directly to Nextech library components — note these matches.

**React prototype in the workspace** — read the relevant component files to extract page and section layout, visual hierarchy, component breakdown, user flows and state transitions, and data shapes. The prototype's visual style will intentionally differ from the Nextech design system — extract structure, workflow, and interaction logic; do not carry over styling.

**Written description only** — the concept may be clear even without a design artifact. Ask only the targeted questions needed to understand layout, key interactions, and expected data before proceeding. Focus on what would block the build, not a complete spec.

When multiple sources are available, treat them as complementary: Figma is authoritative on layout intent and visual hierarchy; the React prototype is authoritative on interaction flow and data structure; the Nextech MCP is authoritative on how to implement both.

**Implementation plan from `prototype-audit`** — if the designer has a prioritized plan from the `prototype-audit` skill, treat it as authoritative on what needs to change and why. Build in its priority order unless the designer says otherwise, and use its task descriptions alongside the design references above rather than re-deriving scope.

---

## Step 3: Discover Available Components and Patterns

**On subsequent invocations**, scan the existing workspace first: read the component files already written to learn what's been built, what patterns are established, and what shared components exist. Reuse and stay consistent with what's there — never duplicate an existing component. This replaces a full MCP sweep; scope discovery to the new elements in the current section only.

Before writing any code, use the Nextech Design System MCP to inventory what's available for the specific UI being built:

```
getComponentDescriptions()      → full list of available UI components
getPatternDescriptions()        → UX patterns (forms, navigation, data tables, etc.)
getFoundationDescriptions()     → tokens for spacing, color, typography, elevation
```

For the major elements in the design, find the closest Nextech component or pattern. Always prefer a library component over a custom implementation, even if configuration is needed. If something genuinely has no library equivalent, flag it explicitly and work with the designer to decide whether an existing component can be configured to cover the need or a new custom component is required — agreeing on its behavior and visual approach before writing code.

Use the component-specific `*Docs()` tools for full documentation of anything you plan to use — don't guess at props or configuration.

---

## Step 4: Clarify Before Building

Surface blockers and ambiguities before writing code. Ask the designer about:
- UI elements with no clear Nextech equivalent
- Interactions or behaviors that aren't clear from the design reference
- Data structures that need to be understood to mock correctly
- Edge cases the designer cares about (empty states, error states, loading states)

Keep clarification focused — only ask about things that would block or significantly affect the implementation. Once you have enough to proceed with confidence, confirm the scope (which page or section you're building) and begin.

---

## Step 5: Build the Angular Components

Implement the UI following all conventions below. Structure output as reusable, standalone Angular components with realistic mock data.

### Component Architecture

- Each logical UI section (e.g., a header, a data table, a filter panel) gets its own component file
- Extract any repeated patterns into shared child components
- Use descriptive, hyphenated file names: `patient-summary-card.component.ts`, `appointment-list.component.ts`
- Populate with realistic mock data — the UI should render meaningfully, not show empty shells
- Do not generate unit tests (`*.spec.ts` files) — the output is a handoff spec with mock data, and tests belong to the implementing team once real logic and API calls are wired in

### Angular Conventions

Follow these consistently:

- **Standalone components** — always use `standalone: true`
- **Change detection** — always set `changeDetection: ChangeDetectionStrategy.OnPush`
- **Inputs/outputs** — use `input()` and `output()` functions, not `@Input()`/`@Output()` decorators
- **State** — use signals for local state; `computed()` for derived state; never call `.mutate()` on a signal (use `.set()` or `.update()`)
- **Control flow** — use `@if`, `@for`, `@switch`; never use `*ngIf`, `*ngFor`, `*ngSwitch`
- **Forms** — prefer reactive forms over template-driven forms
- **Class bindings** — use `class` binding instead of `ngClass`, except when binding a `Set`
- **Style bindings** — use `style` binding instead of `ngStyle`
- **Dependency injection** — use `inject()` function, not constructor injection
- **Observables** — use the async pipe in templates; keep templates free of complex logic
- **TypeScript** — use strict typing; avoid `any`; use `unknown` when type is uncertain

### Nextech Design System Usage

The design system is the foundation — never circumvent it.

- Use `@nextech/ui-components` components whenever one fits — do not roll custom implementations for things the library already covers
- Before writing any custom CSS, check the MCP for helper classes or CSS custom properties that address the need
- Allowed customization approaches, in order of preference:
  1. Helper CSS classes documented by the library
  2. SCSS mixins/functions (e.g., `nextech.spacing(2)`, `@include nextech.elevation('elevation-2')`)
  3. CSS custom properties prefixed with `--nextech-` that are part of the component's public API
- **Never** use `::ng-deep` to reach inside component styles
- **Never** set `ViewEncapsulation.None` to pierce component boundaries
- **Never** target internal CSS classes (anything prefixed `--_nuic-`)
- Source all spacing, color, typography, and elevation from design system tokens — no hardcoded values

### Accessibility (WCAG 2.1 AA)

Every component must meet WCAG 2.1 AA. Build this in from the start — it's much harder to retrofit.

- **Keyboard navigation** — all interactive elements must be reachable and operable via keyboard; visible focus states are required
- **Color contrast** — 4.5:1 minimum for body text; 3:1 for large text and UI components
- **Images and icons** — provide `alt` text or `aria-label`; decorative elements get `aria-hidden="true"`
- **Forms** — every field needs an associated `<label>`; error messages must be programmatically associated (e.g., `aria-describedby`)
- **Semantics** — use the right HTML elements for the job; reach for ARIA only when native semantics aren't sufficient
- **Focus management** — move focus appropriately when dialogs open, routes change, or dynamic content appears
- **No color-only communication** — never convey state or meaning through color alone; pair with text, icons, or patterns

