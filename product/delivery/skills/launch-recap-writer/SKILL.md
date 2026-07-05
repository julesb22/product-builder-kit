---
name: launch-recap-writer
description: Close the loop after a launch. Reads the PRD's success metrics, pulls actuals from Amplitude, compares target vs actual honestly (a miss is a miss), and writes an SCR-form stakeholder recap ending in a keep, iterate, or kill call. Use 2 to 4 weeks after shipping a feature, or whenever a stakeholder asks "how did it do".
---

# Launch Recap Writer

Close the loop: did the feature do what the PRD said it would? Honest answer, SCR form, ends in a keep / iterate / kill call.

## Tool detection (do this first)

Actuals come from Amplitude via the Amplitude MCP (same connection as `funnel-analyst`).

1. Check whether Amplitude MCP tools are available.
2. If not available: say exactly this, then continue with the manual path: "Amplitude MCP is not connected. To connect it, add the Amplitude integration in your Claude settings (see [link placeholder]). Paste the numbers for each success metric and I will write the recap from those." Label the recap "based on numbers provided by the PM".

## Input

- PRD path (the feature being recapped) + launch date.
- Optional: recap audience (team vs exec). Default: team. Exec version is shorter and leads with the business outcome.

## Process

1. **Read the success metrics section of the PRD.** These targets were written before launch; they are the contract. Do not move the goalposts.
2. **Pull the actuals** from Amplitude using the exact events instrumented via the tracking sections of `eng-handoff-writer` tickets (check `product/tickets/{feature-slug}.md` for the event names). Use the launch date as the start of the measurement window and state the window explicitly.
3. **Compare target vs actual per metric, honestly.** A miss is reported as a miss, with the actual number next to the target. No spin, no "directionally positive". If a metric cannot be measured (event never instrumented, too early to tell), say exactly that; it is a finding, not a footnote.
4. **Write the recap in SCR form**, mirroring the PRD it closes:
   - **Situation**: what the PRD said the world looked like, and the targets we set.
   - **Complication**: what we shipped, and what actually happened (target vs actual table).
   - **Resolution**: the keep / iterate / kill recommendation, with reasoning.
5. **End with the evidence gaps**: what we still do not know, and what it would take to know it.
6. **Never fabricate.** No invented numbers, no assumed causality ("signups rose 12% and we shipped in the same week" is a correlation until segmented).

## Output

Stakeholder recap written to `product/recaps/{feature-slug}.md`, containing the target vs actual table, the SCR narrative, the keep / iterate / kill call with reasoning, and the evidence gaps.

## Handoff

End every run with:

- Keep: "Document what worked in product/insights/ so the pattern is reusable."
- Iterate: "Feed the gap between target and actual back into `opportunity-prioritizer` as a new candidate opportunity."
- Kill: "Document the learning in product/insights/ via a short post-mortem note. A killed feature with a captured lesson is a win; the loop is now closed."
