---
name: prototype-audit
description: Compare a working prototype in the workspace (React/Vite, Angular, or an HTML wireframe) against a research-synthesis doc to find where the two disagree, then produce a prioritized markdown implementation plan closing the gaps. Use whenever the user has both research findings and a prototype and wants to know whether the prototype actually reflects what research found — trigger on phrases like "does this prototype hold up against the research," "audit the prototype against our findings," "what are we missing compared to what users told us," "check this against the synthesis doc," "turn this feedback into a plan," or "what should we fix before this goes to spec." Also trigger when a synthesis doc already exists and the user is now looking at a prototype that was built from it, even if they don't name this skill directly. This skill only produces the plan — it does not edit the prototype's code.
---

# prototype-audit

Research tells you what's true about users; a prototype is a bet about how to respond to that truth. This skill checks whether the bet is a good one — reading a research-synthesis doc and a code-based prototype side by side, then writing a prioritized plan that closes whatever gap exists between them.

## When to use this

This skill needs two things to exist already: a research synthesis (themes, insights, quotes — typically the output of the `research-synthesis` skill, though any research findings doc will do) and a prototype that's meant to respond to that research, sitting in the workspace as actual code — a React/Vite app (`prototype-design` output), an Angular build (`spec-design` output), or a single-file HTML wireframe (`wireframe-design` output). If either one doesn't exist yet, that's a different job: point the user at `research-synthesis` or `prototype-design` first rather than trying to audit something that isn't there.

This is a judgment task, not a checklist — the goal is an honest, well-evidenced answer to "does this actually address what we heard," not a mechanical diff.

## Locate both inputs

Ask for the synthesis doc's path and the prototype's location if they're not obvious from context — this project (like `research-synthesis`) has no fixed convention for where either lives. If the workspace has more than one candidate for either, confirm rather than assume; an audit built on the wrong prototype version or a stale synthesis doc wastes everyone's time.

## Read everything before comparing anything

Read the full synthesis doc first — not just the Insights → Opportunities table, the whole thing, including quotes and the "why it matters" notes, since those carry nuance a table row strips out. Then read the prototype in full: every screen, every component, the actual copy, the flows a user can walk through. A comparison built from a skim of either side will miss the gaps that matter and invent ones that don't exist.

How you read the prototype depends on what it is. For a React/Vite or Angular codebase, walk the routes or screen components, note what data and copy each screen actually shows, and pay attention to states — is there an empty state, an error state, or does the happy path stand alone? For a single-file HTML wireframe from `wireframe-design`, read the screen data objects and annotations directly, and check whether it was built in placeholder mode (bars instead of real copy) — that determines what you can honestly claim later, see below.

If something about the prototype's intent isn't clear from the code alone — why a screen exists, whether something is genuinely finished or a known stub, whether an omission is deliberate or just not-built-yet — ask the user rather than guessing. Code tells you what's there; it doesn't always tell you why, and a plan built on a wrong assumption about intent sends the next agent down the wrong path.

## Compare, theme by theme

For each theme or insight in the synthesis doc, work out where the prototype stands: does it address what research found, partially address it, not address it at all, or — worth calling out specifically — actively contradict it? A prototype that does the opposite of what users asked for is a more urgent problem than one that simply hasn't gotten there yet, and lumping both into "not addressed" hides that.

Ground every status in something specific: which screen, which component, which line of copy. "The onboarding theme is partially addressed" is an assertion; "the invite-step friction theme from research is unaddressed — the prototype's `InviteStep.jsx` still requires an email per invitee with no bulk option, which is exactly what P3 and P5 flagged" is evidence a developer can act on without re-reading the whole synthesis doc themselves.

Not every theme will map cleanly onto the prototype, and that's fine to say. Some research findings are about business logic, backend behavior, or things genuinely out of scope for a prototype at this stage — note those rather than forcing a verdict the prototype was never going to earn.

Some verdicts rest on something you can point to directly — a component that plainly doesn't exist, a screen that plainly does what research asked for. Others rest on inference — a wireframe's placeholder copy that can't confirm actual wording, code whose intent isn't fully clear even after asking, a screen that plausibly covers a need without quite matching the mechanism research described. When a verdict is the second kind, say so in the same breath as the verdict itself, rather than stating it with the confidence you'd give something you could point to directly. This comes up most often with placeholder-mode wireframes (structure is real, content isn't, so content-level verdicts can't be confident), but it isn't limited to that case — flag it wherever the evidence is thinner than the status label alone would suggest.

## Build the plan

Turn the gaps into a prioritized, sequential list of concrete tasks — specific enough that an agent picking up the plan (via `prototype-design`, `spec-design`, or general coding help) could act on each line without re-deriving the reasoning. Reference the actual screen, component, or file where the change belongs whenever the prototype's structure makes that clear.

Prioritize on two axes, the same ones `research-synthesis` uses for its Insights → Opportunities table so the two documents read as a continuous thread: how much the gap matters (tied to prevalence and severity in the research) and how much work closing it looks like. A high-prevalence theme the prototype flatly contradicts belongs at the top; a low-prevalence, high-effort nice-to-have belongs at the bottom or in a deferred section.

Not everything needs to make the plan. A gap can be real and still not worth prioritizing right now — put those in a short "deferred" section with the reason, rather than either forcing them into the main plan or dropping them silently. The same goes for anything you're genuinely unsure about: an open question the user needs to resolve before an agent could implement it confidently is more useful named than guessed at.

## Work the plan with the user

Don't treat the first draft as final. Walk the user through it, section by section if it's long, and ask directly whether the priority order matches their sense of what matters, whether any task is described precisely enough to hand off, and whether anything got missed or over-weighted. Revise based on what they say. This is a planning document meant to survive contact with a real implementation pass, not a report to be filed — it's worth getting genuinely right before calling it done.

## Scope

This skill produces the plan and nothing else — it does not touch the prototype's code, even for an obvious one-line fix. Once the user is happy with the plan, the next step is a separate invocation of `prototype-design`, `spec-design`, or whatever coding agent the user prefers, handed the finished plan as its brief.

## Output

Ask where to save the plan and what to name it if the user hasn't said. A reasonable default, if asked, is `<prototype-name>-audit.md` alongside the prototype or the synthesis doc — wherever the user is more likely to find it later.

```markdown
# Prototype Audit: [Project / Study Name]

**Research source:** [synthesis doc path] · **Prototype:** [path, and what it is — React/Vite, Angular, HTML wireframe]
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

Don't credit the prototype for addressing something it only gestures at. "There's a settings screen" isn't the same as "the settings screen solves the specific configuration pain point research surfaced" — check that the mechanism actually matches what was asked for, not just that a plausible-looking screen exists in the right general area.

Resist the pull to find a gap for every theme just because the format has a slot for one. If the prototype genuinely nails something, say so plainly and move on — a credible audit reports good news as readily as bad news, and only that credibility makes the bad news worth acting on.

Keep the plan's tasks phrased as outcomes, not implementation details — "add a bulk-invite option to the onboarding flow" gives an agent room to build it well; prescribing exact component structure or styling decisions oversteps what an audit should specify and risks conflicting with whatever conventions the target codebase already has.
