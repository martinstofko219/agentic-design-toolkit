# wireframe-design

Rapidly explore a UI design problem through three distinct lo-fi wireframe concepts — without opening a design tool.

---

## Overview

When you have a design problem but aren't sure which direction to take it, this skill generates three meaningfully different structural approaches and lets you click through them right away. The goal isn't polish — it's breadth. You get something to react to, debate, and build on, instead of starting from a blank canvas or committing to a single direction too early.

---

## When to use it

Reach for this skill when you're at the beginning of a design problem and want to explore the solution space before committing to a direction. Good triggers include:

- "Wireframe this for me"
- "Give me a few layout ideas for..."
- "I need to explore some concepts for..."
- "Sketch out a few approaches to..."

If your brief is vague — no clear user, no defined problem — consider running `design-grill` first. Wireframes built on fuzzy thinking tend to explore the wrong space.

---

## How to invoke

**In an agent session (Copilot or Claude):** Just describe the design problem in natural language. The agent will recognize the intent and invoke the skill automatically. It'll ask you a couple of clarifying questions — platform, user, goal — before generating anything.

**Manually:** Add `SKILL.md` as context in your session and describe the problem. Same clarifying questions apply.

---

## What you get

A single self-contained `.html` file you can open in any browser — no build step, no dependencies. Inside it, you'll find three named wireframe concepts (think "Progressive Disclosure" or "Guided Wizard", not "Option 1"), each showing a 2–4 screen clickable flow. A brief panel summarizes the design bet behind each variation, and a toggleable annotation panel explains the thinking behind individual screens.

The experience is meant to feel like three different teams each took a swing at the problem — not one team that made minor adjustments to the same layout. If two variations feel too similar when you're clicking through them, push back and ask for a more structurally different approach.

By default, body copy is represented as placeholder bars. Ask for "realistic copy mode" if you want the wireframes populated with actual content from the domain.

---

## Good to know

The lo-fi aesthetic is intentional — warm tones, hand-drawn-feeling borders, sketch-style typography. It's designed to signal "this is explorable, not final," which makes it easier for stakeholders to give honest feedback without fixating on visual details.

---

## Related skills

- **`design-grill`** — run this first if the problem isn't clearly defined yet
- **`prototype-design`** — once you've picked a direction, use this to build a high-fidelity interactive version
- **`prototype-audit`** — if there's research findings to check against, this can audit a wireframe (built in realistic copy mode) the same way it audits a full prototype
