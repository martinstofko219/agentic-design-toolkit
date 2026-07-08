# prototype-audit

Check whether a prototype actually reflects what research found — and get a prioritized plan for closing the gap.

---

## Overview

Research and prototypes drift apart easily: research gets synthesized, a prototype gets built later by someone (or something) working from a summary, and nobody goes back to check whether the two still agree. This skill does that check directly — reading a research-synthesis doc and a working prototype side by side, theme by theme, and writing a prioritized markdown implementation plan that names exactly what needs to change, in what order, and why.

It's an audit, not an implementation step. The output is a plan an agent can pick up and execute — this skill itself never touches the prototype's code.

---

## When to use it

Use this once both a research synthesis and a responding prototype exist. Good triggers include:

- "Does this prototype actually address what we heard from users?"
- "Audit the prototype against the synthesis doc"
- "What are we missing compared to the research?"
- "Turn this research feedback into a plan for the prototype"
- "What should we prioritize before this goes to spec-design?"

If either input doesn't exist yet, this isn't the right skill yet — run `research-synthesis` to get findings, or `prototype-design` to get something to audit, first.

---

## How to invoke

**In an agent session (Copilot or Claude):** Point at the synthesis doc and the prototype (a folder or file path) and describe what you want checked. The skill reads both in full before comparing anything, asks about the prototype's intent where the code alone doesn't explain it, and works through the plan with you before calling it done.

---

## What you get

A single markdown file: a per-theme alignment section (addressed, partially addressed, not addressed, contradicted, or out of scope — each grounded in a specific screen, component, or line of copy, not a vague impression), a prioritized implementation plan ordered for an agent to work through sequentially, a deferred/out-of-scope section for real gaps that don't need fixing right now, and open questions that need a decision before implementation can start.

Priority and effort use the same High/Med/Low scale as `research-synthesis`'s Insights → Opportunities table, so the two documents read as one continuous thread from finding to fix.

---

## Good to know

The skill reads the prototype's actual code — React/Vite, Angular, or a single-file HTML wireframe — rather than working from a description of it. If the prototype is a wireframe built in placeholder mode (bars instead of real copy), it'll say so and scope the audit to structure and flow rather than pretending to assess content it can't see.

It also won't manufacture a gap for every theme just to fill out the template — if the prototype genuinely gets something right, the audit says so.

---

## Related skills

- **`research-synthesis`** — produces the findings doc this skill reads as input
- **`prototype-design`** — produces the React/Vite prototypes this skill can audit, and is typically where the resulting plan gets executed
- **`spec-design`** — where the plan often gets executed for Angular builds, and can also produce the prototype being audited
- **`wireframe-design`** — can produce an earlier-stage HTML prototype this skill is also able to audit
