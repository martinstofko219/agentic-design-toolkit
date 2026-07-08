---
name: prototype-design
description: Build a realistic, highly interactive React + Vite prototype for design exploration. Use when a designer wants to explore, communicate, or validate a UI concept with something that looks and feels like a real app — not a static mockup. Trigger on "prototype", "build a working version", "interactive mockup", "make this feel real", "concept app", "build this out", or any time the user wants to bring a design idea to life in code. Always use this skill when the request is about making a UI concept interactive and clickable, even if the word "prototype" never comes up.
---

Your job is to turn a design idea into a realistic, interactive React + Vite prototype that feels like a real product. Not production-ready code — but convincing enough to explore, test, and communicate the concept. It should look and behave like a real app.

## Discovery First

If the designer arrives with a vague idea or an underspecified problem, suggest running the `design-grill` skill before prototyping. A prototype built on an unclear concept is expensive to throw away — a grilling session is not.

Before writing any code, have a natural conversation with the designer to understand what you're building and why. Don't run through a checklist — ask what you genuinely need to know, follow up where things are unclear, and stop when you have enough to make confident decisions. You're not trying to extract a spec; you're trying to understand the concept well enough that the prototype feels designed for this specific problem.

Understand: the problem the interface is solving, who uses it and in what context, the industry or domain it lives in, any workflow or flow the designer has in mind, any references or directions they're drawn to, and whether there's existing research (interviews, usability findings, a synthesis doc) this prototype is meant to answer to.

Once you have a clear picture, propose an aesthetic direction before building — but how you do this depends on what the designer brought you.

If they haven't indicated a visual direction, propose two distinct aesthetic approaches. Make them genuinely different — not variations on the same theme. Each should have a name, a clear mood, a typographic character, a color story, and a sense of spatial feeling. Give the designer something real to react to, not a menu of safe options. They can pick one, blend elements, or use the contrast to articulate what they actually want.

If they've already described a visual direction, don't just accept it at face value — ask questions to help them make it specific and their own. What references or textures are they drawn to? What feeling should the first screen create? Where do they want restraint versus expressiveness? The goal is to move from a generic label ("dark and modern," "clean and minimal") to something distinctive enough to execute with conviction.

Either way, confirm the direction before you start coding.

## Design Direction

Commit to a single aesthetic and pursue it with intention. The prototype should feel designed specifically for its domain — a fintech tool has different energy than a consumer wellness app; a medical dashboard should feel different from a creative production tool. Name your direction before you build and execute it consistently across every screen.

Typographic choices matter: pair a characterful display or heading font with a refined body font. Avoid the defaults that most generated UIs converge on — overused font stacks, predictable card grids, purple-gradient-on-white. Vary between light and dark. Choose colors that feel considered, not safe. Build visual atmosphere through background treatment — layered gradients, subtle texture, depth — rather than flat solid surfaces.

The goal is for someone to look at this prototype and immediately feel where it lives. That feeling comes from committing to a direction, not hedging.

## Implementation

Scaffold a complete React + Vite project that the designer can run immediately with `npm install && npm run dev`. Create all necessary files — `package.json`, `vite.config.js`, `index.html`, and the full `src/` directory. The deliverable is a working localhost app, not a code snippet.

Structure it as a real multi-screen SPA with client-side routing or view state — the designer should be able to navigate through the concept, not just look at one screen. Where the concept requires it, add lightweight state management to support realistic flows. Keep it simple; this isn't a production architecture problem.

**Design tokens**: Define all colors, spacing values, and typographic decisions as JS constants or CSS custom properties at the top of the project — not scattered inline throughout components. The palette, type scale, and spacing rhythm should be visible, named, and consistent. This makes the design coherent and easy to adjust.

**Realistic data**: Every screen should be populated with plausible, domain-specific content. Real-looking names, real numbers, actual copy for headings, labels, and CTAs — not "User 1," "Item Name," or Lorem ipsum. The prototype should feel inhabited. Placeholder content breaks the illusion and makes it genuinely harder to evaluate the concept.

**Interactions and motion**: Include transitions between screens, meaningful hover states, and micro-interactions that reinforce the aesthetic direction. The prototype should feel alive — not over-engineered, but responsive and polished enough that clicking through it communicates the experience, not just the layout.

**Scope**: Match complexity to the concept. Some prototypes are a focused single flow; others need several interconnected screens. Build what's needed to communicate the idea. A dashboard concept needs a real dashboard with data; an onboarding flow concept needs to actually walk through the steps. Don't pad scope, but don't cut corners that would make the concept feel hollow.

## What to Avoid

Generic AI aesthetics: predictable layouts, the same overused fonts, purple color schemes and purple-on-white gradients that have become the default fingerprint of AI-generated UI. Placeholder content in any form. Building something that could be about anything — this prototype should be unmistakably about the specific concept the designer brought you.

## After the Build

If there's research this prototype was meant to respond to, the `prototype-audit` skill can check the finished result against it and produce a prioritized plan for anything that's still missing or off.
