---
name: prototype-builder
description: Go from PRD plus flows to a clickable Lovable prototype the PM can put in front of users. Encodes the prompt patterns that produce good Lovable output, builds screen by screen following the flow, and knows when to stop. Use when a PRD needs to become something testable, or to pressure-test a concept before engineering touches it.
---

# Prototype Builder

Go from PRD and flows to a clickable prototype in Lovable that a PM can put in front of users this week. A prototype demonstrates the flow; it is not the product.

## Tool detection (do this first)

This skill is Lovable-specific, via the Lovable MCP (create_project, send_message, preview URL).

1. Check whether Lovable MCP tools are available.
2. If not available: say exactly this: "Lovable MCP is not connected. To connect it, add the Lovable integration in your Claude settings (see [link placeholder])." Then, instead of failing, output the full sequence of Lovable prompts (initial message plus per-screen follow-ups) that the PM can paste into Lovable manually, in order. Label it "manual prompt sequence".

## Input

- PRD path (default: most recent in `product/prds/`).
- Optional: flow diagram (from `user-flow-mapper`).
- Optional: design constraints (brand colors, reference screenshot, tone).

## Process (the prompt patterns that make Lovable output good)

1. **Scope guardrails in every message.** The initial Lovable message states: "This is a prototype, not production. No auth. No real backend. Hardcode realistic sample data." Repeat the guardrail when Lovable starts adding infrastructure on its own.
2. **Design constraints up front.** Lovable has no tech-stack selector, so stack preferences, visual references, brand colors, and any screenshot go into the FIRST message, not a later correction.
3. **Screen by screen, following the flow.** One screen (or one flow step) per message, in the order of the user flow. Never one giant everything-prompt. Review the preview between iterations before sending the next message.
4. **Realistic sample data.** Names, numbers, and content that look like the real product. "Lorem ipsum" kills user tests.
5. **Translate PM feedback into concrete instructions.** "It feels cramped" becomes "increase section padding, reduce to one CTA per screen". "It looks cheap" becomes specific type, spacing, and color changes. Never forward vague feedback verbatim.
6. **Know when to stop.** The prototype is done when it demonstrates the flow well enough to test, not when it is pixel-perfect. When that point is reached, say so explicitly and stop iterating. Polishing a prototype is procrastination with extra steps.

## Output

1. Lovable preview URL (to share with test users) and editor URL (for the PM).
2. A short note saved to `product/prototypes/{feature-slug}.md`: **"What this prototype does and does not demonstrate"**, for whoever runs the tests. Includes: the flow it covers, what is hardcoded or fake, and what feedback would be meaningful vs noise.

## Handoff

End every run with:

"Test this with 3 to 5 users. Record the sessions and feed them back into `user-interview-synthesizer` so the evidence compounds. When you are ready to build the real thing, run `lead-dev-validator` to find out how much of it you can ship yourself."
