# spec-design

Build production-ready Angular UI pages and sections using the Nextech Design System — structured, accessible, and ready for developers to wire up real logic.

---

## Overview

This skill bridges the gap between a design reference and a working Angular implementation. It takes Figma frames, React prototypes, or written descriptions as input and produces spec-quality Angular components using `@nextech/ui-components` — the real component library, real design tokens, real accessibility compliance — not a throwaway proof of concept.

The output is meant to be handed directly to developers. Components are structured for reuse, populated with realistic mock data, and built to WCAG 2.1 AA standards. Developers should be able to drop them into the app and focus entirely on wiring up API calls and business logic.

---

## When to use it

Use this skill when you're ready to build production-quality Angular UI from a design reference. Good triggers include:

- "Build this Figma frame in Angular"
- "Implement this section using our design system"
- "Convert this React prototype to Angular"
- "Create the components for this page, ready for dev handoff"
- "Spec this out in Angular"

If the concept is still fuzzy or the problem isn't well defined, run `design-grill` first. Reworking spec-quality Angular is significantly more expensive than reworking a prototype.

---

## Prerequisites

Before invoking this skill, make sure you have:

- An Angular app shell with `@nextech/ui-components` installed
- The `nextech-design-system-mcp-server` MCP configured (install from `@nextech/design-system-mcp` if needed)
- The Figma MCP connected, if you're working from a Figma link

The skill will verify these are available at the start of every session.

---

## How to invoke

**In an agent session (Copilot or Claude):** Provide your design reference — a Figma URL, a path to a React prototype in the workspace, or a written description — and the agent will invoke the skill. It will check prerequisites, read the design input, query the Nextech MCP for available components, and clarify anything unclear before writing code.

**Manually:** Add `SKILL.md` as context, point to your design reference, and describe the scope of what you want built.

---

## What you get

Standalone Angular components written to the project conventions: `OnPush` change detection, signals for state, `input()`/`output()` functions, native control flow, and reactive forms. All theming comes from design system tokens — no hardcoded values, no `::ng-deep`, no style encapsulation overrides.

Each invocation typically produces one complete page or a coherent self-contained section. Complex apps are built incrementally across multiple invocations.

Components are populated with realistic mock data so the UI renders meaningfully and can be reviewed before any API integration work begins. Unit tests are deliberately not included — the output is a handoff spec, and testing belongs to the implementing team once real logic is wired in.

---

## Good to know

The skill reads React prototypes for structure and flow, not for styling. Visual differences between the prototype and the Nextech design system are intentional — the design system wins on theming.

If a UI element has no Nextech equivalent, the skill will flag it and work with you to decide whether an existing component can be configured to cover the need, or whether a custom component is warranted.

---

## Related skills

- **`design-grill`** — run this first if the concept isn't clearly defined
- **`prototype-design`** — use this when you need something interactive to explore or communicate the concept before speccing it out
- **`wireframe-design`** — use this even earlier if you're still exploring structural directions
- **`prototype-audit`** — if there's research findings to check the design against, run this first and hand the resulting plan in as another design input
