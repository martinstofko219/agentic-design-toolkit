---
name: prototype-design
description: Build a realistic, highly interactive React + Vite prototype for design exploration. Use when a designer wants to explore, communicate, or validate a UI concept with something that looks and feels like a real app — not a static mockup. Trigger on "prototype", "build a working version", "interactive mockup", "make this feel real", "concept app", "build this out", or any time the user wants to bring a design idea to life in code. Always use this skill when the request is about making a UI concept interactive and clickable, even if the word "prototype" never comes up. Also trigger when a designer asks to iterate on, revise, or extend an existing prototype in the workspace, even in a fresh session.
---

Your job is to turn a design idea into a realistic, interactive React + Vite prototype that feels like a real product. Not production-ready code — but convincing enough to explore, test, and communicate the concept. It should look and behave like a real app.

**Session mode:** Once invoked, this skill stays active for the rest of the session — apply these guidelines to every subsequent request that builds on or iterates the prototype, without re-invocation. On first load, tell the designer the skill is active and remains so until they say "stop prototype-design" or "exit skill mode."

## Discovery First

If the designer arrives with a vague idea or an underspecified problem, suggest running the `design-grill` skill before prototyping. A prototype built on an unclear concept is expensive to throw away — a grilling session is not.

Before writing any code, have a natural conversation with the designer — not a checklist — to understand:

- the problem the interface is solving
- who uses it and in what context
- the industry or domain it lives in
- any workflow or flow the designer has in mind
- references or directions they're drawn to
- whether there's existing research (interviews, usability findings, a synthesis doc) this prototype is meant to answer to

Follow up where things are unclear and stop when you can make confident decisions — you're understanding the concept, not extracting a spec.

Once you have a clear picture, propose an aesthetic direction before building. If the designer hasn't indicated a visual direction, propose two genuinely distinct approaches — not variations on a theme — each with a name, a clear mood, a typographic character, a color story, and a sense of spatial feeling. Give them something real to react to; they can pick one, blend elements, or use the contrast to articulate what they want. If they've already described a direction, don't accept it at face value — ask what references or textures they're drawn to, what feeling the first screen should create, where they want restraint versus expressiveness, moving from a generic label ("dark and modern") to something distinctive enough to execute with conviction.

Either way, confirm the direction before you start coding.

## Design Direction

Commit to a single aesthetic and pursue it with intention across every screen. The prototype should feel designed specifically for its domain — a fintech tool has different energy than a consumer wellness app or a medical dashboard. Pair a characterful display or heading font with a refined body font; avoid the defaults generated UIs converge on — overused font stacks, predictable card grids, purple-gradient-on-white. Vary between light and dark, choose colors that feel considered rather than safe, and build atmosphere through background treatment — layered gradients, subtle texture, depth — rather than flat solid surfaces. Someone should look at this prototype and immediately feel where it lives; that comes from committing, not hedging.

## Implementation

Scaffold a complete React + Vite project that the designer can run immediately with `npm install && npm run dev`. Create all necessary files — `package.json`, `vite.config.js`, `index.html`, and the full `src/` directory. The deliverable is a working localhost app, not a code snippet.

Structure it as a real multi-screen SPA with client-side routing or view state — the designer should be able to navigate through the concept, not just look at one screen. Where the concept requires it, add lightweight state management to support realistic flows. Keep it simple; this isn't a production architecture problem.

**Design tokens**: Define all colors, spacing values, and typographic decisions as JS constants or CSS custom properties at the top of the project — not scattered inline throughout components. The palette, type scale, and spacing rhythm should be visible, named, and consistent. This makes the design coherent and easy to adjust.

**Realistic data**: Populate every screen with plausible, domain-specific content — real-looking names, real numbers, actual copy for headings, labels, and CTAs; never "User 1," "Item Name," or Lorem ipsum. Placeholder content breaks the illusion and makes the concept harder to evaluate.

**Interactions and motion**: Include transitions between screens, meaningful hover states, and micro-interactions that reinforce the aesthetic direction — not over-engineered, but responsive and polished enough that clicking through communicates the experience, not just the layout.

**Scope**: Match complexity to the concept — a focused single flow or several interconnected screens, whatever communicates the idea. A dashboard concept needs a real dashboard with data; an onboarding concept needs to walk through the steps. Don't pad scope, but don't cut corners that make the concept feel hollow.

## What to Avoid

Generic AI aesthetics: predictable layouts, the same overused fonts, purple color schemes and purple-on-white gradients that have become the default fingerprint of AI-generated UI. Placeholder content in any form. Building something that could be about anything — this prototype should be unmistakably about the specific concept the designer brought you.

## After the Build

If there's research this prototype was meant to respond to, the `prototype-audit` skill can check the finished result against it and produce a prioritized plan for anything that's still missing or off.
