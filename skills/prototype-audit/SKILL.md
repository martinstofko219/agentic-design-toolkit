---
name: prototype-audit
description: Compare a prototype — React/Vite or Angular code in the workspace, an HTML wireframe, or Figma frames — against a research-synthesis doc to find where the two disagree, then produce a prioritized markdown implementation plan closing the gaps. Use whenever the user has both research findings and a prototype and wants to know whether the prototype reflects what research found — trigger on phrases like "does this prototype hold up against the research," "audit the prototype against our findings," "what are we missing compared to what users told us," "check this against the synthesis doc," "turn this feedback into a plan," or "what should we fix before this goes to spec." Also trigger when a synthesis doc exists and the user is now looking at a prototype built from it, even without naming this skill. Produces the plan only — it does not edit the prototype's code.
---

# prototype-audit

Research tells you what's true about users; a prototype is a bet about how to respond to that truth. This skill checks whether the bet is a good one — reading a research-synthesis doc and a prototype side by side, then writing a prioritized plan that closes whatever gap exists between them. It's a judgment task, not a checklist: the goal is an honest, well-evidenced answer to "does this actually address what we heard," not a mechanical diff.

## Inputs

Two things must already exist: a research synthesis (themes, insights, quotes — typically `research-synthesis` output, though any findings doc will do) and a prototype meant to respond to it. The prototype can be:

- a React/Vite app (`prototype-design` output) or an Angular build (`spec-design` output) in the workspace
- a single-file HTML wireframe (`wireframe-design` output)
- Figma frames, provided as a Figma link

If either input doesn't exist yet, point the user at the right skill instead of auditing something that isn't there.

Ask for the synthesis doc's path and the prototype's location or Figma link if they're not obvious — there's no fixed convention for where either lives. If the workspace has more than one candidate for either, confirm rather than assume; an audit built on the wrong prototype version or a stale synthesis doc wastes everyone's time.

## Read everything before comparing anything

Read the full synthesis doc first — not just the Insights → Opportunities table; the quotes and "why it matters" notes carry nuance a table row strips out. Then read the prototype in full: every screen, every component, the actual copy, the flows a user can walk through. How depends on what it is:

- **React/Vite or Angular codebase** — walk the routes or screen components, note what data and copy each screen actually shows, and pay attention to states: is there an empty state, an error state, or does the happy path stand alone?
- **HTML wireframe** — read the screen data objects and annotations directly, and check whether it was built in placeholder mode (bars instead of real copy) — that limits what you can honestly claim about content later.
- **Figma frames** — use the Figma MCP to pull both the design context (layout structure, component usage, actual text content, and any variants, states, or annotation notes) and a screenshot of each frame, and read them together — the structured context tells you what exists and what things are named, the screenshot confirms what a user actually sees. Walk every frame in the flow, not just the one linked. If the Figma MCP is unavailable, ask for exported screenshots of every frame instead.

If the prototype's intent isn't clear from the code alone — why a screen exists, whether something is finished or a known stub, whether an omission is deliberate — ask the user rather than guessing. Code tells you what's there, not why, and a plan built on a wrong assumption about intent sends the next agent down the wrong path.

## Compare, theme by theme

For each theme or insight in the synthesis doc, work out where the prototype stands: addressed, partially addressed, not addressed, or — worth calling out specifically — actively contradicted. A prototype that does the opposite of what users asked for is more urgent than one that simply hasn't gotten there yet; don't lump both into "not addressed." Some themes won't map onto the prototype at all — business logic, backend behavior, things genuinely out of scope at this stage — and it's fine to say so rather than forcing a verdict.

Ground every status in something specific: which screen, which component, which line of copy. "The onboarding theme is partially addressed" is an assertion; "the invite-step friction theme is unaddressed — `InviteStep.jsx` still requires an email per invitee with no bulk option, which is exactly what P3 and P5 flagged" is evidence a developer can act on.

When a verdict rests on inference rather than something you can point to directly — placeholder copy that can't confirm actual wording, code whose intent stayed unclear even after asking, a screen that plausibly covers a need without matching the mechanism research described — say so in the same breath as the verdict itself. Placeholder-mode wireframes make content-level verdicts inherently uncertain (structure is real, content isn't). Figma frames are the mirror case: content and layout are real, but the design is static, so any verdict about interactive behavior rests on annotations, prototype wiring, and frame order rather than something you can click — flag behavior-level claims accordingly. Flag thin evidence wherever it occurs.

## Build the plan

Turn the gaps into a prioritized, sequential list of concrete tasks — specific enough that an agent picking up the plan (via `prototype-design`, `spec-design`, or general coding help) could act on each line without re-deriving the reasoning, referencing the actual screen, component, or file wherever the prototype's structure makes that clear.

Prioritize on the same two axes `research-synthesis` uses for its Insights → Opportunities table, so the two documents read as a continuous thread: how much the gap matters (tied to prevalence and severity in the research) and how much work closing it looks like. A high-prevalence theme the prototype flatly contradicts belongs at the top; a low-prevalence, high-effort nice-to-have belongs at the bottom or in a deferred section.

Not everything needs to make the plan. A gap can be real and still not worth prioritizing now — put those in a short "deferred" section with the reason rather than forcing them in or dropping them silently. Anything you're genuinely unsure about becomes an open question the user needs to resolve — more useful named than guessed at.

## Work the plan with the user

Don't treat the first draft as final. Walk the user through it, section by section if it's long, and ask whether the priority order matches their sense of what matters, whether each task is described precisely enough to hand off, and whether anything got missed or over-weighted. Revise based on what they say — this is a planning document meant to survive contact with a real implementation pass.

## Scope and output

Produce the plan and nothing else — do not touch the prototype's code, even for an obvious one-line fix. Once the user is happy, the next step is a separate invocation of `prototype-design`, `spec-design`, or whatever coding agent they prefer, handed the finished plan as its brief.

Ask where to save the plan and what to name it if the user hasn't said. A reasonable default, if asked, is `<prototype-name>-audit.md` alongside the prototype or the synthesis doc — wherever the user is more likely to find it later.

```markdown
# Prototype Audit: [Project / Study Name]

**Research source:** [synthesis doc path] · **Prototype:** [path or Figma link, and what it is — React/Vite, Angular, HTML wireframe, Figma frames]
**Date:** [date]

## Summary
[3-5 sentences: overall, how well does the prototype reflect the research, and what are the headline gaps]

## Alignment by Theme

### [Theme name]
**Status:** Addressed / Partially addressed / Not addressed / Contradicted / Out of scope for a prototype
**Research found:** [pull from the synthesis doc]
**Prototype does:** [specific, cited to screen/component/file]
**Gap:** [the delta, if any — omit if fully addressed]

[Repeat per theme]

## Prioritized Implementation Plan

| # | Task | Addresses | Priority | Effort | Notes |
|---|---|---|---|---|---|
| 1 | [Specific, actionable change] | [theme name] | High/Med/Low | High/Med/Low | [file/screen reference, anything an agent would need to know] |

Ordered by priority, not by theme — this is a sequence an agent can work through top to bottom.

## Deferred / Out of Scope
[Real gaps, deliberately not prioritized now, with why]

## Open Questions
[Anything that needs a decision before implementation can start with confidence]
```

## A few things worth getting right

Don't credit the prototype for addressing something it only gestures at. "There's a settings screen" isn't the same as "the settings screen solves the specific configuration pain point research surfaced" — check that the mechanism actually matches what was asked for.

Resist the pull to find a gap for every theme just because the format has a slot for one. If the prototype genuinely nails something, say so plainly — a credible audit reports good news as readily as bad news, and only that credibility makes the bad news worth acting on.

Phrase the plan's tasks as outcomes, not implementation details. "Add a bulk-invite option to the onboarding flow" gives an agent room to build it well; prescribing exact component structure or styling oversteps what an audit should specify and risks conflicting with the target codebase's conventions.
