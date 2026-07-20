# research-plan

Plan a user research study — and when a prototype exists, turn it into test scenarios worth an hour of a participant's time.

---

## Overview

A research session can't be re-run once it's spent, so the plan is where a study is won or lost. This skill co-drafts that plan with you: it establishes what decision the study informs, turns that into research questions, recommends themes and test scenarios, and assembles everything into a single markdown plan a moderator can run sessions from directly.

Core methods are **discovery interviews** and **prototype-based usability tests**. Surveys, card sorting, and A/B tests are supported through a companion reference (`secondary-methods.md`) that the agent loads only when one of those methods fits the questions.

When the study evaluates a prototype, the skill analyzes it first — React/Vite or Angular code in the workspace, a single-file HTML wireframe, or Figma frames via the Figma MCP — and maps what's honestly testable so scenarios never dead-end into an unbuilt screen mid-session.

---

## When to use it

Use this skill whenever research sessions need planning — with or without a prototype in hand. Requests like these should trigger it:

- "Help me plan user testing for this prototype"
- "Draft a research plan for the onboarding study"
- "What should we test with users?"
- "Write an interview guide for discovery calls with clinic managers"
- "Generate test scenarios from these Figma frames"

If the ask is to make sense of research that already happened, that's `research-synthesis`. If it's to check a prototype against existing findings, that's `prototype-audit`.

---

## How to invoke

**In an agent session (Copilot or Claude):** Describe what you're trying to learn or decide, and point at the prototype if there is one (a workspace path or a Figma link). If you don't mention a prototype, the skill asks whether one exists before drafting usability scenarios.

Expect a conversation, not a one-shot document: the skill proposes research questions, then themes, then scenarios, and revises each with you before assembling the final plan. It will ask where to save the output and what to name it.

---

## What you get

One markdown research plan containing background and objectives, 3–5 research questions, method and participant criteria, themes (each traced to a research question), fully specified scenarios — participant-facing task narrative, starting point in the prototype, success criteria, what to observe, follow-up probes, and known prototype limitations to steer around — plus a timed session guide with moderator notes, logistics, and open questions.

For interview studies, scenarios become question areas per theme: an opening question, probes, and what to listen for. For secondary methods, the relevant sections adapt (question design for surveys, card sets for sorts).

---

## Good to know

The research-question → theme → scenario traceability is deliberate: when sessions are done, the plan travels with the transcripts to `research-synthesis`, and the planned themes become candidate synthesis themes — one thread from planning through synthesis to the prototype audit.

The skill will push back on coverage greed (a focused session beats a tour) and recommends treating the first session as a pilot, since scenario wording problems only surface when a real participant hears them.

---

## Related skills

- **`prototype-design`** / **`wireframe-design`** — produce the prototypes this skill turns into test scenarios; the skill points you there if no prototype exists yet
- **`research-synthesis`** — takes the transcripts (and this skill's plan) and distills them into themes and insights after sessions run
- **`prototype-audit`** — downstream neighbor that compares the prototype against the synthesis this study feeds
