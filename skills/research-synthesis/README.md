# research-synthesis

Turn raw user research — interview transcripts, usability notes, survey exports — into a synthesis doc the team can act on.

---

## Overview

Research is only useful once it's been read, cross-referenced, and distilled into patterns. This skill takes a set of markdown transcripts or notes and produces a structured synthesis: named themes with prevalence and supporting quotes, an insights-to-opportunities table, and prioritized recommendations — separating what was observed from what it means, and flagging what's still unknown.

---

## When to use it

Use this skill whenever there's a folder of interview transcripts, usability test notes, or similar research artifacts in markdown, and the ask is some version of "what are we hearing" or "pull the patterns out of this." It doesn't need to be invoked by name — requests like these should trigger it:

- "What patterns are you seeing in these interviews?"
- "Synthesize the research in `research/transcripts/`"
- "What did we learn from these usability sessions?"
- "Turn these notes into a findings doc"

If the underlying research questions seem poorly formed, or the study design itself seems off, that's outside this skill's scope — it synthesizes what's there rather than critiquing how it was collected (though methodology gaps worth flagging still show up in the output's Methodology Notes section).

---

## How to invoke

**In an agent session (Copilot or Claude):** Point at the transcripts (a folder, a set of files, or paste them directly) and describe what you want to learn. The skill reads every transcript before writing anything — cross-document patterns are the whole point, so it won't summarize file-by-file and stitch the results together.

It will ask where to save the output and what to name it if that isn't specified — this project doesn't enforce a fixed location or naming convention for synthesis docs.

---

## What you get

A single markdown file with a participants table (ID, name if the transcripts provide one, and role/context) so a reader can orient before diving in, an executive summary, named themes (each with a prevalence count, supporting quotes attributed to participant IDs, and a "why it matters" note kept distinct from the raw observation), an insights-to-opportunities table, recommendations in priority order, open questions, and methodology notes.

Themes are only included if they actually recur across participants — thin evidence gets labeled as emerging rather than inflated to match the format. Opportunities are written concretely enough to point at a specific flow or feature later, since this doc is commonly the input to further design work even though that comparison isn't done here.

---

## Good to know

The skill will ask before assuming which files belong to the study if a transcripts folder mixes multiple projects or includes unrelated notes. It will also say so explicitly if a "pattern" is really just one or two mentions — synthesis loses credibility fast when speculative themes are presented with the same confidence as well-supported ones.

---

## Related skills

A companion skill for comparing a synthesis doc against prototypes to surface gaps and opportunities is a natural next addition to this toolkit — not yet built.
