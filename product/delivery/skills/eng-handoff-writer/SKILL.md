---
name: eng-handoff-writer
description: Convert a PRD into scoped, testable, Linear-ready tickets engineers do not have to rewrite. Every ticket includes an "analytics events to instrument" section so tracking is never forgotten. Slices vertically into thin end-to-end slices. Use when handing a feature to engineering, or automatically after a Red verdict from lead-dev-validator.
---

# Eng Handoff Writer

Convert a PRD into scoped, testable tickets engineers do not have to rewrite. Format: Linear-ready markdown (Jira as secondary format on request).

## Input

- PRD path (default: most recent in `product/prds/`).
- Optional: the `lead-dev-validator` output for this feature (from `product/validations/`), which tells you what is backend and why.

## Process

1. **Slice vertically.** Thin end-to-end slices a user can experience ("user can save one item and see it on reload"), not horizontal layers ("build the frontend" + "build the backend"). Explain the slicing in one paragraph at the top so engineering understands the intent and can push back.
2. **Each ticket contains:**
   - **User story**: as a [who], I want [what], so that [why]. The who comes from the PRD, not "as a user".
   - **Acceptance criteria**: testable, binary, no vague words ("fast", "intuitive", "clean" are banned). Someone must be able to say pass or fail to each line.
   - **Edge cases**: from the flow diagram's error branches if `user-flow-mapper` ran; otherwise derive them (empty states, failures, permission denied, concurrent edits).
   - **Out of scope**: what this ticket deliberately does not cover, so scope cannot silently grow.
   - **Analytics events to instrument** (THE DIFFERENTIATOR, never omitted): for each event, the event name following the project's existing naming convention (inspect existing events via Amplitude MCP or the codebase; never invent a new convention), the trigger, and the properties. The success metrics in the PRD must be measurable from these events. Most PMs remember tracking after launch; this section makes forgetting impossible.
3. **Dependencies between tickets flagged explicitly** ("blocked by #2"), so sequencing is visible before sprint planning.
4. **Never fabricate.** If the PRD is missing something a ticket needs (an unanswered PRD gap, an unknown API), the ticket says "open question for engineering" rather than inventing an answer.

## Output

- Ticket set written to `product/tickets/{feature-slug}.md`, formatted for direct paste into Linear.
- If the Linear MCP is connected: offer to create the issues directly in Linear (ask which team and project first). If it is not connected, do not mention an error; the markdown is the primary deliverable.

## Handoff

End every run with:

"Tickets ready at product/tickets/{feature-slug}.md. After launch, run `launch-recap-writer` against the success metrics in the PRD; the analytics events in these tickets are what will make that recap possible."
