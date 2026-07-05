---
name: user-flow-mapper
description: Turn a PRD or feature description into user flow diagrams in Whimsical (or Mermaid fallback in-repo). Maps the happy path first, then edge cases and error states, and flags every decision the PRD does not cover as a PRD gap. Use after writing a PRD, or whenever a feature needs its journey visualized.
---

# User Flow Mapper

Turn a PRD into user flow diagrams, and use the mapping process itself as a PRD review: every decision the flow needs that the PRD does not cover is a gap worth fixing before build.

## Tool detection (do this first)

The preferred tool is Whimsical via the Whimsical MCP.

1. Check whether Whimsical MCP tools are available.
2. If available: create the flowchart in Whimsical and return the board link.
3. If not available: say exactly this, then continue with the fallback: "Whimsical MCP is not connected. To connect it, add the Whimsical integration in your Claude settings (see [link placeholder]). I will produce Mermaid diagrams in the repo instead; they are versionable in git, and clearly labeled as the fallback."

## Input

- A PRD path. Default: the most recent file in `product/prds/`. Or a feature description if no PRD exists (note in the output that no PRD backs the flow).

## Process

1. **Happy path first.** Map the main journey end to end before touching anything else. Entry point, steps, decisions, success state.
2. **Then edge cases and error states as separate branches.** PMs forget error states; this skill does not. For every step ask: what if this fails, what if the input is empty or invalid, what if the user abandons here, what does the user see.
3. **Trace every decision diamond back to the PRD.** If the flow requires a decision the PRD does not cover ("what happens if the user has no saved payment method?"), do not invent the answer. Flag it as a PRD gap and keep mapping with a placeholder branch labeled "PRD gap #n".
4. **One flow per diagram.** Multiple journeys (first-time user vs returning, admin vs member) get separate diagrams. Never merge them into one spaghetti chart.

## Output

- Whimsical: one board link per flow.
- Fallback: Mermaid files at `product/flows/{feature-slug}.md` (one flow per section, clearly labeled "Mermaid fallback, Whimsical not connected").
- Always: **the list of PRD gaps discovered while mapping**, numbered, each phrased as the question the PRD needs to answer. If there are none, say "no gaps found" explicitly.

## Handoff

End every run with:

"Attach the flow link (or file) to the PRD and resolve the gaps listed above. Then run `prototype-builder` to turn the PRD and flow into a clickable prototype."
