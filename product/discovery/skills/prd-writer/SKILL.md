---
name: prd-writer
description: Produce a one-page PRD that an engineering team respects, structured on the SCR framework (Situation, Complication, Resolution). Interviews the PM first with the 5 questions a good EM would ask, refuses to write on thin evidence, and keeps scope to one page. Use when defining a feature, writing a PRD, or turning a prioritized opportunity into a spec.
---

# PRD Writer

Produce a one-page PRD an engineering team respects. The narrative spine is SCR: Situation, Complication, Resolution. The discipline is: interview first, evidence before prose, one page or split.

## Step 1: Interview the PM first (non-negotiable)

Do NOT write anything from a one-sentence prompt. Before drafting, ask the 5 questions a good EM would ask, one block, wait for answers:

1. Who exactly is this for? (segment, not "users")
2. What evidence do we have that this problem is real? (interviews, funnel data, support tickets; "I think" is an answer, but it gets recorded as such)
3. What does success look like in numbers? (a metric and a target)
4. What are we explicitly NOT doing in this version?
5. What is the riskiest assumption, the thing that, if wrong, kills the feature?

Before asking, check for existing evidence yourself: read `product/insights/INSIGHTS.md`, recent funnel analyses in `product/insights/`, and `product/priorities-*.md` if they exist. Pre-fill what you can and confirm rather than re-ask.

## Step 2: Gate on evidence

- If the Situation and Complication cannot be grounded in real evidence (quotes from interviews, numbers from analytics), do not fake it. Say: "This PRD is weak here: [gap]. Consider running `user-interview-synthesizer` or `funnel-analyst` first." Then either stop or write the PRD with the gap clearly marked as a risk.
- Never invent quotes, numbers, or research results. An honest "evidence: none yet, founder conviction" beats a fabricated statistic every time.

## Step 3: Write the one-page SCR PRD

Structure:

1. **Situation**: what is true today, grounded in evidence. Metrics (from `funnel-analyst` outputs), verbatim quotes (from `product/insights/`). No opinions in this section.
2. **Complication**: the tension that makes the status quo untenable. Why now. The cost of doing nothing, quantified if possible.
3. **Resolution**: the proposed direction, NOT a full solution spec. Plus:
   - **Success metrics**: measurable in the analytics stack. If Amplitude MCP is connected, cross-check that the events needed to measure them exist (or flag them as "needs instrumentation"). Never assume event names.
   - **Non-goals**: always present. What this version deliberately does not do.
   - **Open questions**: always present. What we still need to learn.
   - **Riskiest assumption**: stated plainly, with how we will find out.

Rules:

- **One page.** If the PM keeps adding scope, push back and propose splitting into two PRDs. Say which half ships first and why.
- PM language throughout. No implementation detail beyond what shapes the decision.

## Output

Written to `product/prds/{feature-slug}.md`. Create the folder if needed.

## Handoff

End every run with:

"PRD saved. Next: run `user-flow-mapper` to visualize it (it will also surface gaps in the PRD), then `lead-dev-validator` to find out whether you can build this yourself or need engineering."
