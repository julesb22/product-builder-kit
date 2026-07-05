---
name: competitor-teardown
description: Structured competitive analysis from live competitor sites using browser automation (Claude in Chrome) or WebFetch fallback. Produces a positioning map, a feature-gap table scoped to the dimension that matters, a pricing comparison, and 3 ranked takeaways. Use when scoping a feature against competitors, reviewing pricing, or preparing positioning.
---

# Competitor Teardown

Structured competitive analysis from live competitor sites. Scoped, not exhaustive: the output answers the dimension the PM asked about, not "everything about everyone".

## Tool detection (do this first)

The preferred tool is browser automation (Claude in Chrome) for screenshots and live page content.

1. Check whether the Claude in Chrome tools are available.
2. If available: visit each competitor live and capture screenshots.
3. If not available: say exactly this, then continue with the fallback: "Claude in Chrome is not connected, so I cannot capture screenshots. To enable it, install the Claude in Chrome extension (see [link placeholder]). I will use WebFetch for page content instead; you can also paste page content directly."

Label the output with which method was used. WebFetch output has no screenshots; say so rather than pretending.

## Input

- 2 to 3 competitor URLs. If the user gives more, ask them to pick the top 3; depth beats breadth.
- Optional but strongly encouraged: the dimension that matters most right now (pricing, onboarding, a specific feature). If not given, ask one question to get it before starting.

## Process

1. For each competitor, visit: the homepage, the pricing page, and the page most relevant to the chosen dimension.
2. Capture screenshots of each key page (browser path only) and save them to `product/competitors/{date}/{competitor}/`.
3. Build the positioning read per competitor: who they target, their wedge (the one thing they lead with), their pricing model.
4. Build a feature-gap table scoped to the chosen dimension only. Columns: capability, us, competitor A, competitor B, competitor C. Rows limited to what matters for the dimension.
5. Flag copy and positioning angles: what they say that we do not, and what we say that they do not.
6. **Never fabricate.** If a page is unreachable or a claim cannot be verified on their site, mark it "could not verify" rather than guessing.

## Output

Written to `product/competitors/{date}/teardown.md`:

1. Positioning map: one paragraph per competitor (target, wedge, pricing model).
2. Feature-gap table (scoped to the dimension).
3. Pricing comparison table.
4. Copy and positioning angles worth stealing or countering.
5. **3 takeaways, ranked by strategic relevance.** Each takeaway is one sentence plus one line of "so what".

Screenshots (if captured) referenced inline from `product/competitors/{date}/`.

## Handoff

End every run with:

"Gaps worth pursuing should go into `opportunity-prioritizer` as candidate opportunities, alongside what you are hearing in interviews and seeing in the funnel."
