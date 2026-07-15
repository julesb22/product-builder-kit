---
name: opportunity-prioritizer
description: Turn a messy list of ideas, requests, and insights into a ranked, defensible priority list using RICE with explicit written assumptions per score. Includes a mandatory "what we are NOT doing and why" section. Use when deciding what to build next, preparing a roadmap discussion, or after accumulating interview insights and funnel findings.
---

# Opportunity Prioritizer

Turn a messy list of opportunities into a ranked, defensible priority list. The framework is RICE, but the real product is the written assumptions: every score comes with a one-liner a stakeholder could challenge.

## Input

- A list of opportunities: pasted, from a file, or auto-read from `product/insights/` (check that folder first and offer to include what is there).
- **A single bubbled-up request** — a GitHub issue, support ticket, sales-call ask, or forum thread. One item is a valid input: score it, then slot it into the existing ranked list (read `product/priorities-*.md` if one exists) rather than ranking it in isolation. A request nobody has placed against the rest of the roadmap is not yet prioritized.
- Optional: team capacity context (people, weeks, constraints).

If `product/insights/` exists, read `INSIGHTS.md` and any funnel analyses so evidence-backed opportunities can be identified. If it does not exist, say so; scores will lean on the PM's judgment and confidence will reflect that.

### Reading demand signals from a public request

When the opportunity comes from a tracker (GitHub issue, Canny board, forum), pull the raw signals before scoring — for GitHub, `gh issue view <n> --repo <owner/repo> --json title,reactionGroups,comments,createdAt,labels`. What each signal feeds:

- **Reactions / upvotes (👍)** → a *floor* on Reach, never the Reach itself. Public upvoters are a vocal, self-selected minority; most affected users never find the issue. Write the assumption that way: "Reach: 254 👍 over 3 yrs is a floor, not the count — extrapolate from active-user base, not from the thread."
- **Comment volume + "any update?" pile-ups + duplicate/linked issues** → sustained demand. Many duplicates closed into one issue is stronger than a single high count.
- **Age (open since…)** → longevity of the pain, and a reason the not-doing line must be honest if it keeps getting deferred.
- **Requester association** (`NONE` / `CONTRIBUTOR` / `MEMBER`) and whether concrete use cases or reference products appear in the thread → sharpens Impact and Confidence.

Public-request signals are real evidence, but they measure who showed up to ask, not who is affected. Keep that caveat in every score derived from them.

## Process

Score each opportunity on RICE:

1. **Reach**: how many users per time period. Write the assumption: "Reach 800/mo: assumes all checkout users hit this step."
2. **Impact**: how much it moves the needle per user (3 massive, 2 high, 1 medium, 0.5 low, 0.25 minimal). Write the assumption.
3. **Confidence**: be honest and cite the evidence class.
   - Backed by interview evidence (from `user-interview-synthesizer`) or funnel data (from `funnel-analyst`): high confidence, and say which source.
   - Backed by a **public request with strong, quantified demand** (e.g. a long-standing GitHub issue with hundreds of reactions, heavy comment traffic, and duplicates): medium-to-high — cite the counts, and note it measures askers, not the affected population.
   - Backed by one anecdote, a single ticket, or competitor behavior: medium.
   - Gut feel: low, and label it "gut feel" in writing.
4. **Effort**: person-weeks, roughest credible estimate. Write the assumption.

Rules:

- **Every single score gets a one-line written assumption.** No naked numbers.
- **Never fabricate evidence.** If there are no interviews or data behind an opportunity, its confidence is low and the table says why.
- **RICE is a conversation starter, not objective truth.** Say this explicitly in the output. The ranking is a structured way to argue, not a verdict.

## Output

1. **Ranked table**: opportunity, R, I, C, E, RICE score, and the assumption lines under each row.
2. **"What we are NOT doing and why"**: mandatory section. List the opportunities that fell below the line and one honest sentence each on why. A priority list without a not-doing list is a wish list.
3. **The top opportunity as a one-line problem statement**, phrased and ready to hand to `prd-writer` (problem, who has it, evidence).

Save to `product/priorities-{date}.md` so the PRD writer can find it.

## Handoff

End every run with:

"Take the #1 opportunity into `prd-writer`. It will interview you before writing anything; bring the evidence behind the confidence score."
