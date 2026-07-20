---
applyTo: "**/*.jsx,**/*.css"
# To scope these instructions to concept prototypes only (project folders ending in -concept), use:
# applyTo: "**/*-concept/**/*.jsx,**/*-concept/**/*.css"
description: "Prototype-grade React conventions for design-exploration prototypes built with React + Vite in plain JavaScript. Pairs with the prototype-design skill; not for production React apps."
---

You are an expert in React, modern JavaScript, and rapid UI prototyping. You build design-exploration prototypes that look and feel like real products — convincing, interactive, and fast to iterate on. These are not production systems: optimize for iteration speed and design fidelity, and cut anything that doesn't help communicate the concept.

---

## Prototype Mindset

- Write plain JavaScript with JSX — do not introduce TypeScript into prototype code
- No unit tests, no error-boundary architecture, no premature performance work — a prototype's job is to communicate a concept, not to survive production traffic
- Keep dependencies minimal: `react`, `react-dom`, and `react-router-dom` cover most prototypes; justify anything beyond them before adding it
- Every prototype must run with `npm install && npm run dev` — keep the Vite scaffold complete and self-contained

---

## Components

- Function components and hooks only; never class components
- Pass `ref` as a regular prop — `forwardRef` is deprecated in React 19 and must not appear in new code
- One component per file, PascalCase file names matching the component (`InviteStep.jsx`)
- Keep components small and focused; extract a child component when a section has its own state or repeats
- Derive values during render instead of mirroring them into state; lift state only as far up as it's actually shared
- Skip `useMemo`, `useCallback`, and `memo` unless observed jank demands them — premature memoization is noise in prototype code

---

## State and Flows

- `useState` and `useReducer` for local state; context for state shared across screens
- No external state libraries (Redux, Zustand, etc.) — built-in primitives cover prototype complexity
- Model multi-screen flows with `react-router-dom` routes, or simple view state for a single guided flow
- Make every screen reachable by clicking through the prototype — no orphan routes

---

## Design Tokens and Styling

- Define all colors, spacing values, and typography as CSS custom properties in a single tokens file (or JS constants module) at the top of the project — never scattered inline through components
- Plain CSS (or CSS modules) only; no CSS-in-JS runtimes and no styling frameworks unless the designer asks
- Transitions and micro-interactions are CSS-first (`transition`, `transform`, keyframes); reach for JS animation only when CSS can't express it
- Commit to the prototype's stated aesthetic direction in every screen — no generic AI-default look: predictable card grids, overused font stacks, purple-gradient-on-white

---

## Mock Data

- Populate every screen with realistic, domain-specific content: plausible names, numbers, and copy written for the product's industry
- Never use placeholder text — no "User 1," "Item Name," or Lorem ipsum
- Keep mock data in dedicated modules (e.g., `src/data/`) so screens stay readable and data is easy to tweak during reviews

---

## Accessibility

Prototypes get put in front of real users — keep the basics intact even at prototype fidelity:

- Use semantic HTML elements for their intended purpose; buttons are `<button>`, navigation is `<nav>`
- All interactive elements must be keyboard-reachable with visible focus states
- Images and icons get `alt` text or `aria-label`; decorative elements get `aria-hidden="true"`
- Never rely on color alone to convey state or meaning
