---
name: research-synthesis
description: Synthesize user research — interview transcripts, usability test notes, survey results, support tickets, or NPS/CSAT responses — into themes, prioritized insights, and recommendations. Use this whenever the user has a folder of markdown interview transcripts or research notes and wants patterns, key findings, user segments, or a synthesis doc pulled out of them, even if they don't say "synthesize" explicitly — phrases like "what are we hearing from users," "pull the themes out of these interviews," "summarize this research," or "what did we learn from these calls" should all trigger this skill. Also trigger when a synthesis doc already exists and needs to be regenerated or extended with new transcripts.
---

# research-synthesis

Turn a stack of raw research — interview transcripts, usability notes, survey exports — into a synthesis document a team can actually act on: named themes, evidence-backed insights, and a prioritized set of opportunities.

## When to use this

Trigger any time someone hands over a set of markdown transcripts, notes, or research exports and wants to know what they mean — whether or not they use the word "synthesis." A team workspace with a folder of interview transcripts (e.g. `research/transcripts/*.md`) and a request like "what patterns are you seeing" or "turn these into insights" is exactly the case this skill is built for.

If there's only one transcript, or the request is really "summarize this one conversation," synthesis still applies — themes just won't have much prevalence data yet. Say so in the output rather than forcing false patterns out of a single data point.

If the underlying research problem or the questions being asked of users seem poorly defined, that's a different problem than this skill solves — flag it, but don't block on it.

## Before synthesizing: read everything first

Read every transcript in full before writing anything. Synthesis is a cross-document task — a theme only becomes a theme when it shows up in more than one place, and the only way to know that is to hold all the transcripts in mind at once. Summarizing transcripts one at a time and stitching the summaries together tends to flatten patterns and lose the specific language participants used, which is exactly what makes a synthesis doc credible.

If it's unclear which files to include (e.g. the folder has transcripts from multiple studies, or mixes interviews with unrelated notes), ask before assuming scope.

## What makes a good theme

A theme is a pattern that recurs across participants, not a single interesting quote. For each theme worth naming, be able to say how many of how many participants raised it — "6 of 8 participants struggled with X" is far more useful than "users struggled with X." When prevalence is genuinely unclear (small sample, ambiguous mentions), say so rather than inventing a number.

Keep observations and interpretations visibly separate. "5 of 8 users clicked the wrong element first" is something that happened. "The layout is confusing" is a conclusion drawn from that. Both belong in the synthesis, but conflating them is how research stops being trustworthy — a reader should be able to tell which claims are direct evidence and which are your read on that evidence.

Pull real quotes, attributed to a participant identifier (P1, P2, or whatever anonymized label the transcripts use — never a real name unless the transcripts already de-anonymize them and the user confirms that's fine). Quotes are what make a theme concrete instead of asserted.

## Output

Ask where the output file should be saved and what it should be named if the user hasn't said — this project doesn't enforce a fixed location or naming convention, and guessing wrong means the doc ends up somewhere the team won't find it. A reasonable default to propose, if asked, is something like `<study-name>-synthesis.md` alongside the source transcripts.

Structure the synthesis with this template. Adjust section presence to what the research actually supports — don't force a "User Segments" table out of five interviews that didn't reveal distinct segments, and don't skip the methodology notes even when they're brief.

```markdown
# Research Synthesis: [Study Name]

**Method:** [Interviews / Usability Test / Survey / etc.] · **Participants:** [N]
**Date range:** [dates] · **Source:** [transcript folder or files used]

## Participants
| ID | Name | Role / Context |
|---|---|---|
| P1 | [name, if the transcript provides one — otherwise leave blank or use "—"] | [role, org size, or other identifying context available in the transcript] |

Give a reader enough here to orient before they hit the themes below — who was in the room shapes how much weight to put on any given finding. Only fill in the Name column when the source material actually names the participant; don't invent one to fill the cell, and apply the same judgment used for quote attribution above — if the transcripts anonymize participants, keep the table anonymized too. Skip the whole table only if the source material genuinely doesn't include role or context per participant.

## Executive Summary
[3-5 sentences: what this research set out to learn and the headline findings]

## Key Themes

### [Theme name]
**Prevalence:** [X of Y participants, or "emerging" if too early to quantify]

**What we heard:** [Plain description of the pattern]

**Evidence:**
- "[Direct quote]" — P[X]
- "[Direct quote]" — P[X]

**Why it matters:** [The implication for the product or the team, kept separate from the observation itself]

[Repeat per theme]

## Insights → Opportunities

| Insight | Opportunity | Impact | Effort |
|---|---|---|---|
| [What the research showed] | [What could be done about it] | High/Med/Low | High/Med/Low |

Write opportunities concretely enough that someone could point them at a specific flow or screen later — "make the checkout flow clearer" is more useful downstream than "improve usability." This doc is often the input to a later comparison against prototypes or designs — see the `prototype-audit` skill — even though that comparison isn't this skill's job.

## User Segments
[Include only if the data actually supports distinct segments]

| Segment | Characteristics | Needs | Rough size |
|---|---|---|---|

## Recommendations
1. **[Highest priority]** — [why, tied to which theme(s)]
2. **[Next priority]** — [why]
3. **[Lower priority]** — [why]

## Open Questions
[What this research didn't answer, or raised without resolving]

## Methodology Notes
[How many transcripts, how they were collected, any gaps or biases worth flagging — e.g. all participants recruited from one channel, a heavily leading question in the guide, uneven interview lengths]
```

## A few things worth getting right

Quantify wherever the data allows it — "most users" is doing work that "6 of 8 users" does better, and it lets a reader judge confidence for themselves. When a theme rests on genuinely thin evidence (one or two mentions), it's fine to include if it's interesting, but label it as emerging rather than presenting it with the same weight as a well-supported pattern.

If transcripts include structured metadata (participant role, session date, recruiting source), use it — segmenting by role or context often surfaces sharper themes than treating all participants as one pool.

Don't editorialize recommendations beyond what the evidence supports. A synthesis doc loses credibility fast if the recommendations section reads like it was written before the research was read.
