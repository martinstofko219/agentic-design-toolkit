---
name: research-plan
description: Plan a user research study and produce a single markdown plan — objectives, research questions, method, participants, themes, test scenarios, and a session guide. Core methods are discovery interviews and prototype-based usability tests; surveys, card sorts, and A/B tests are supported via a companion reference. When the study evaluates a prototype — React/Vite or Angular code, an HTML wireframe, or Figma frames — the skill analyzes it and works with the user to draft themes and test scenarios grounded in what the prototype can actually do. Trigger on phrases like "plan user testing," "draft a research plan," "what should we test with users," "write an interview guide," or "generate test scenarios for this prototype" — and whenever a prototype exists and the user wants user feedback on it, even if they never say "research."
---

# research-plan

A research session is an hour of a stranger's time and can't be re-run. The plan is what makes that hour count: sharp research questions, scenarios that surface behavior instead of polite opinions, and a session structure a moderator can run from directly. Draft it *with* the user, not for them — recommend themes and scenarios confidently, but treat every draft as a proposal: they know the product and its users; the skill knows how to turn that into a study.

## Start from the decision, not the method

Establish what prompted the study and what decision its findings inform. A study run to "learn about users" produces a report nobody acts on; one run to decide "ship the new onboarding flow or rework it" produces answers.

From that decision, write 3–5 research questions with the user — specific, answerable within the study, and non-leading ("how do users currently decide what to reorder," not "do users love the reorder feature"). They are the plan's spine: every theme and scenario must trace back to one. The traceability pays off downstream — `research-synthesis` inherits the themes as candidates when transcripts come back.

## Choose the method

Match the method to the questions, not the other way around:

- **Discovery interviews** — questions about the problem space: current workflows, motivations, unmet needs. No prototype required.
- **Usability test** — questions about whether a specific design works, and a prototype exists to put in front of people.
- **Something else** — if the questions point at surveys, card sorting, or A/B testing, read `secondary-methods.md` in this skill's folder before planning; it covers when each fits and how the plan's sections change. Don't load it otherwise.

A hybrid — interview-style context questions before usability tasks — is common; plan it as a usability test with a longer context phase.

## Analyze the prototype (usability studies)

If the user wants to test a design but hasn't pointed at a prototype, ask whether one exists — scenarios have nothing to anchor to otherwise. If none exists, suggest `wireframe-design` or `prototype-design` first, or pivot to discovery interviews if the questions allow.

The prototype can be a React/Vite app (`prototype-design` output) or Angular build (`spec-design` output) in the workspace, a single-file HTML wireframe (`wireframe-design` output), or Figma frames via a link. Walk it the way `prototype-audit` does:

- **React/Vite or Angular** — walk the routes and screen components; note which flows complete end-to-end, which dead-end, and which states (empty, error, loading) exist.
- **HTML wireframe** — read the screen data and annotations; placeholder mode rules out tasks that depend on participants reading real content.
- **Figma frames** — pull design context and a screenshot per frame via the Figma MCP; note what's wired with prototype interactions versus static. If the MCP is unavailable, ask for exported screenshots of every frame.

The product is a map of what's honestly testable: completable flows, the prototype's edges, real data versus placeholder. Verify scenarios against this map — a participant hitting an unbuilt screen doesn't just lose a task, it breaks their trust in the prototype for the rest of the hour.

## Propose themes, then draft scenarios together

Propose 3–5 themes — the areas the sessions should illuminate — drawn from the research questions, the prototype walk, and what the user says they want tested; name each theme's research question. Iterate until the user agrees the set covers what matters before drafting scenarios against it.

Scenario craft — where sessions are won or lost:

- Write task narratives in the language of the participant's goal, never the UI's: "you're running low on gloves and need more before Friday," not "use the reorder feature." Naming the thing being tested turns the task into reading comprehension.
- Give a motive and context, not a procedure — realistic stakes surface realistic behavior.
- Verify the starting point and every path the task invites against the prototype map; note limitations in the scenario so the moderator isn't surprised mid-session.
- Success criteria must be observable: "reaches the confirmation screen with 2+ items," not "understands the flow."
- Budget 5–8 minutes per scenario against the session length; four done well beat seven rushed.

For interview studies, each theme instead gets an opening question, probes, and what to listen for — same non-leading discipline, no solution language in the questions.

## Session guide and logistics

Structure the session as a timed arc the moderator runs from directly: warm-up and consent, context questions, scenarios or deep-dive, reactions and debrief, wrap-up. Add moderator notes only where they earn their place — when to stay silent, probe a stall ("what did you expect that to do") instead of rescuing. Include logistics — tooling, recording and consent, note-taker roles — and treat the first session as a pilot: scenario wording problems only surface when a real participant hears them.

## Output

One markdown file. Ask where to save it and what to name it if the user hasn't said; a reasonable default, if asked, is `<study-name>-research-plan.md`. When sessions are done, this doc travels with the transcripts to `research-synthesis`.

```markdown
# Research Plan: [Study Name]

**Method:** [Discovery interviews / Usability test / …] · **Status:** Draft / Final
**Prototype:** [path or Figma link — omit for non-evaluation studies] · **Date:** [date]

## Background & Objectives
[2–4 sentences: what prompted this study and what decision it informs]

**Research questions:**
1. RQ1 — […]

## Method & Participants
**Method:** [what and why it fits the research questions]
**Session format:** [length · moderated/unmoderated · remote/in-person]
**Participants:** [target N, segments if any]
**Recruiting criteria:** [must-haves, exclusions, screener notes]
**Incentive:** [if any]

## Themes
| Theme | Traces to | Why it matters |
|---|---|---|
| [name] | RQ[X] | [one line] |

## Scenarios
[Usability studies — repeat per scenario:]

### [Scenario name]
**Tests:** [theme(s)] · **Time:** ~[X] min
**Task narrative:** "[participant-facing wording, read aloud verbatim]"
**Starting point:** [screen / route / frame]
**Success criteria:** [observable outcome]
**Watch for:** [behaviors, hesitations, wrong paths worth noting]
**Probes:** [follow-ups after the task or on a stall]
**Prototype notes:** [limitations to steer around — omit if none]

[Interview studies — repeat per theme instead:]

### [Theme name]
**Traces to:** RQ[X]
**Opening question:** "[…]"
**Probes:** […]
**Listening for:** [what would actually answer the RQ]

## Session Guide
| Time | Phase | Notes for moderator |
|---|---|---|
| 0:00–0:05 | Warm-up & consent | […] |
| 0:05–0:15 | Context | […] |
| 0:15–0:45 | Scenarios / deep dive | [order, what to skip if running long] |
| 0:45–0:55 | Reactions & debrief | […] |
| 0:55–1:00 | Wrap-up | […] |

**Logistics:** [tools, recording & consent, note-taker, pilot-first-session note]

## Open Questions
[Anything unresolved before sessions can run]
```

## A few things worth getting right

Scenarios test the prototype, not the participant — no gotchas, no tasks that depend on remembering an earlier instruction. A failed task should read as data about the design.

Resist coverage greed. A focused session that answers three research questions well beats a tour that grazes six; park the overflow in Open Questions or a follow-up study note.

Walk the user through themes before scenarios, and scenarios before the full doc — a plan the user co-authored is one they'll actually moderate from.
