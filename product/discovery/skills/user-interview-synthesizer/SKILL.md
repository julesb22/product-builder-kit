---
name: user-interview-synthesizer
description: Turn raw user interview material (Granola transcripts, files, or pasted text) into structured, compounding insights. Extracts pains, jobs-to-be-done, and workarounds backed by verbatim quotes, and maintains a rolling knowledge base in product/insights/. Use after any user interview, discovery call, or usability session.
---

# User Interview Synthesizer

Turn raw interview transcripts into structured insight that compounds across interviews. One interview is an anecdote. Five interviews, synthesized consistently, are evidence.

## Tool detection (do this first)

The preferred source is Granola via the Granola MCP.

1. Check whether Granola MCP tools are available (search for tools matching `granola`).
2. If available: offer to pull the transcript directly from the user's recent meetings.
3. If not available: say exactly this, then continue with the manual path: "Granola MCP is not connected. To connect it, add the Granola MCP server in your Claude Code settings (see [link placeholder]). In the meantime, paste the transcript or give me a file path."

Never fail silently. If you are working from a pasted transcript, note that at the top of the output.

## Input

- One or more transcripts: Granola meeting link or ID, a file path, or pasted text.
- Optional: the research question or hypothesis being explored. If given, prioritize evidence for or against it.

## Process

1. **Read the existing knowledge base first.** Check `product/insights/` for prior interview files and the rolling `product/insights/INSIGHTS.md`. Frequency ranking must count across ALL interviews processed so far, not just this one.
2. **Extract from the new transcript:**
   - Pains: what is broken, slow, confusing, or costly for the user.
   - Jobs-to-be-done: what the user is trying to accomplish, in their words.
   - Workarounds: what they do today instead (workarounds are the strongest buy signal).
3. **Quote discipline.** Every pain, job, and workaround gets at least one verbatim quote, copied exactly from the transcript. Never paraphrase and present it as verbatim. If you must summarize, label it "paraphrase".
4. **Said vs does.** Flag every place where a stated preference contradicts described behavior (for example: "I love the dashboard" but they describe exporting to a spreadsheet every week). These contradictions are gold; call them out in their own section.
5. **Never fabricate.** If the transcript does not support a claim, do not make it. If a section would be empty, say "no evidence in this interview" rather than inventing content.

## Output

Write two things:

1. `product/insights/{date}-{interviewee-or-topic}.md`: the structured extraction for this interview (pains, jobs, workarounds, quotes, said-vs-does flags, open questions).
2. Update `product/insights/INSIGHTS.md`: the rolling synthesis. Structure:
   - **Top pains, ranked by frequency** (with count: "seen in 4 of 6 interviews") and the strongest verbatim quote for each.
   - **Candidate opportunities** derived from the pains.
   - **Open questions to probe in the next interview** (including any said-vs-does contradictions worth testing).

Create the `product/insights/` folder if it does not exist.

## Handoff

End every run with:

"Interview synthesized and added to the knowledge base ({n} interviews total). When you have 5 or more interviews, run `opportunity-prioritizer` on `product/insights/` to turn these pains into a ranked priority list."
