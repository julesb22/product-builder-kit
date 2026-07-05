---
name: funnel-analyst
description: Answer "where are users dropping off and why does it matter" from live Amplitude data (or a pasted CSV fallback). Produces the funnel with per-step conversion, the single biggest drop-off, ranked hypotheses, and exactly one recommended action. Use for conversion questions, drop-off analysis, retention checks, or any "what does the data say" moment.
---

# Funnel Analyst

Answer one question: where are users dropping off, and why does it matter. The output is a decision aid, not a data dump.

## Tool detection (do this first)

The preferred source is Amplitude via the Amplitude MCP.

1. Check whether Amplitude MCP tools are available (search for tools matching `amplitude`).
2. If available: call the context tool first to identify the right project, then proceed.
3. If not available: say exactly this, then continue with the manual path: "Amplitude MCP is not connected. To connect it, add the Amplitude integration in your Claude settings (see [link placeholder]). In the meantime, paste a CSV export of the funnel or the step-by-step numbers, and I will do the analysis on those."

If working from pasted numbers, label the output "based on data you provided, not queried live".

## Input

- A funnel description: either exact event names, or a plain-language journey ("from landing on pricing to completing checkout").
- Optional date range (default: last 30 days).
- Optional segment of interest.

## Process

1. **Discover real event names before querying.** Use the Amplitude events API to list events and match the user's plain-language steps to real event names. Never guess an event name. If a step has no matching event, say so; that is a tracking gap worth reporting on its own.
2. **Pick the right chart for the question:**
   - Conversion question: funnel chart.
   - "Which users" question: segmentation.
   - Stickiness question: retention.
3. **Always check the segment story.** Before reporting a headline number, break it down by at least: new vs returning, device, and acquisition source (when available). If a segment diverges sharply from the average, lead with that.
4. **No data dumps.** Rank everything by decision-relevance. If a number does not change what the PM should do next, leave it out.
5. **Hypotheses are hypotheses.** Never present a "why" as fact. Each hypothesis gets a label: (hypothesis) plus what evidence would confirm or kill it.
6. **Never fabricate.** If the data is not available, say so. Do not invent conversion rates.

## Output

A short analysis containing, in this order:

1. The funnel: each step with count and per-step conversion rate.
2. **The single biggest drop-off**, stated plainly ("62% of users who start checkout never reach payment").
3. 2 to 3 hypotheses for why, each labeled as a hypothesis with a way to test it.
4. **Exactly ONE recommended action**, the highest expected ROI next step. Not three options. One.

Optionally save the analysis to `product/insights/funnel-{slug}-{date}.md` so other skills can find it.

## Handoff

End every run with:

"To validate the drop-off hypothesis with real users, feed it into `user-interview-synthesizer` as the research question for your next interviews. To weigh this against other opportunities, add it as a candidate in `opportunity-prioritizer`."
