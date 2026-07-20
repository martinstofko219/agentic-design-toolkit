# Secondary methods

Read this only when a study calls for a method beyond discovery interviews or usability testing. Each section says when the method is the right call and how the plan's spine changes; everything not mentioned (Background & Objectives, Open Questions, the collaborative drafting loop) works exactly as `SKILL.md` describes.

## Surveys

**Right call when** the research questions are about *how many* or *how much* across a population — quantifying attitudes, prioritizing known options, validating a pattern interviews surfaced. Wrong call for discovering unknowns: a survey can only ask about what you already suspect. If the user reaches for a survey to explore an open problem space, recommend interviews first and say why.

**Plan changes:**
- **Method & Participants** — target 100+ responses for anything the team will treat as quantitative; state the distribution channel and its bias (a survey sent to power users answers questions about power users). No session format; state the expected completion time — over ~7 minutes and completion rates fall off.
- **Themes & Scenarios → Question design.** Themes still trace to research questions; each theme becomes a question group. Draft the actual questions in the plan, not placeholders, and review them with the user question-by-question — wording problems that a moderator could recover from live are unrecoverable in a survey. Watch for: leading wording, double-barreled questions, agreement bias (offer construct-specific scales, not agree/disagree everywhere), and missing "not applicable" escapes. One or two open-text questions maximum, placed late.
- **Session Guide → Distribution & analysis plan.** Replace the timed arc with: channel, open/close dates, screener logic, and how results will be analyzed — decide before launch what numbers would change the decision, or the results will be read as confirming whatever anyone already believed.
- **Pilot** still applies: send to 3–5 people watching them fill it in, then fix what confused them.

## Card sorting

**Right call when** the questions are about information architecture — how users group, name, and expect to find things. Open sorts (participants make their own groups) explore mental models; closed sorts (predefined categories) validate a proposed structure. 15–30 participants gives stable agreement patterns.

**Plan changes:**
- **Themes & Scenarios → Card set & sort design.** The core drafting work is the card set: 30–60 items, one concept per card, written in the user's language rather than internal jargon — a card set that leaks the org chart tests whether users can decode the org chart. Draft the full card list in the plan and review it with the user; for closed sorts, also the category labels. If the sort concerns an existing prototype or Figma structure, pull the actual nav labels and section names from it (walk it as `SKILL.md` describes) so the sort tests reality, not an idealization.
- **Session format** — remote unmoderated tools scale better; moderated sorts (5–8 participants, think-aloud) add the *why* behind groupings. Recommend moderated when the research questions ask why, unmoderated when they ask how many agree. 20–30 minutes per sort.
- **Session Guide** — for moderated sorts, keep the arc but replace scenarios with the sort plus a debrief walking through their groups ("what would you call this pile?"). State the analysis method (agreement matrix / dendrogram) and what agreement level the team will act on.

## A/B testing

**Right call when** the questions are about which of two live variants performs better on a metric the product already tracks. It needs real traffic and an instrumented product — a prototype can't be A/B tested, and if that's the situation, recommend a usability test instead.

**Plan changes:**
- This is a quantitative experiment, not a session, so most of the spine compresses: no participants section beyond the traffic split, no session guide.
- The plan's job is the experiment design: hypothesis per research question ("changing X will move metric Y because…"), primary metric and guardrail metrics, minimum detectable effect, and run length from a sample-size calculation — commit to it up front; peeking early and stopping on a good day is the classic way to ship noise.
- If the team lacks experimentation infrastructure, say so early — this method is usually run in a product analytics tool, and the plan should name which one rather than assume.

## Mixing methods

Studies often pair methods — a survey to size a pattern interviews found, a card sort inside a usability session. Plan each method's section per its rules above, keep one shared set of research questions, and state which method answers which question; a method that answers no research question is scope creep wearing a lab coat.
