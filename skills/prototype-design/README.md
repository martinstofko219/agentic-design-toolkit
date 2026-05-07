# prototype-design

Turn a design concept into a realistic, clickable app — the kind that actually communicates the experience, not just the layout.

---

## Overview

Static mockups and wireframes are great for structure, but they can't communicate feel. This skill builds a working React + Vite prototype that looks and behaves like a real product — real data, real interactions, a committed visual direction — so you can actually experience the concept and put it in front of people to get meaningful feedback.

This is not about production-ready code. It's about building something convincing enough to explore, test, and communicate an idea.

---

## When to use it

Use this skill when a wireframe or description isn't enough to convey the concept, or when you need something people can actually interact with. Good triggers include:

- "Prototype this"
- "Build a working version of..."
- "Make this feel real"
- "I need something I can click through"
- "Build this out"

If the concept is still fuzzy or the problem isn't well defined, run `design-grill` first. A prototype built on an unclear idea is expensive to throw away.

---

## How to invoke

**In an agent session (Copilot or Claude):** Describe the concept and the agent will invoke the skill. It'll have a short discovery conversation with you to understand the domain, the flow, and any visual direction you have in mind — then propose an aesthetic before writing any code. You'll confirm the direction, and then it builds.

**Manually:** Add `SKILL.md` as context and describe your concept. Expect the same discovery conversation before anything gets generated.

---

## What you get

A complete React + Vite project you can run locally. The output is a multi-screen SPA — not a single static screen — with client-side navigation, realistic domain-specific content (actual names, numbers, and copy, not placeholders), hover states, and transitions that make the thing feel alive.

To run it:

```bash
npm install
npm run dev
```

Everything you need is included: `package.json`, `vite.config.js`, `index.html`, and a full `src/` directory. Design tokens (colors, type, spacing) are defined as named constants at the top of the project, so adjusting the visual direction later is straightforward.

The visual output is deliberately opinionated — the prototype is designed to feel like it belongs to a specific domain and aesthetic, not like a generic AI-generated UI.

---

## Good to know

The skill will push back gently on vague visual directions like "clean and minimal" or "dark and modern." That's intentional — it's trying to get you to something specific enough to execute with conviction. Lean into that conversation; the more specific you are, the better the prototype will reflect what you actually had in mind.

---

## Related skills

- **`design-grill`** — run this first if the concept isn't clearly defined
- **`wireframe-design`** — use this earlier in the process if you're still exploring structural directions
