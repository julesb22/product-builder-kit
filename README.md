# Product Builder Kit

10 Claude Code skills for product managers, covering the full feature lifecycle: discovery, definition, design and validation, delivery, and post-launch.

These are not 10 disconnected tricks. The outputs chain: interviews feed insights, insights feed priorities, priorities feed the PRD, the PRD feeds flows, the prototype, the build/no-build verdict, the tickets, and the launch recap closes the loop back into insights. Install once and you get the whole system.

Built from a month of iteration on real APM work. You could build these yourself (and my course at Vibe Coding Academy teaches you exactly how), or you can install mine and start from a working baseline you then adapt to your own product.

## Install (2 commands)

```
# 1. Register the marketplace (once per machine)
/plugin marketplace add julesb22/product-builder-kit

# 2. Install the plugin
/plugin install pm-skills@product-builder-kit
```

Then run `/reload-plugins` (or restart Claude Code) and the 10 skills are available in any project.

To pick up updates later: `/plugin marketplace update product-builder-kit`, no reinstall needed.

## The 10 skills

### Phase 1: Discovery (`product/discovery/`)

| Skill | What it does |
|---|---|
| `user-interview-synthesizer` | Turns interview transcripts (Granola or pasted) into ranked pains with verbatim quotes, compounding across interviews in `product/insights/` |
| `funnel-analyst` | Pulls live Amplitude data, finds the biggest drop-off, gives hypotheses and exactly one recommended action |
| `competitor-teardown` | Visits competitor sites, builds a positioning map, feature-gap table, pricing comparison, and 3 ranked takeaways |
| `opportunity-prioritizer` | RICE scoring with a written assumption per score, plus a mandatory "what we are NOT doing" section |
| `prd-writer` | One-page SCR PRD (Situation, Complication, Resolution). Interviews you first, refuses to write on thin evidence |
| `user-flow-mapper` | Whimsical flows (Mermaid fallback), happy path plus the error states PMs forget, flags PRD gaps |

### Phase 2: Design and validation (`product/design-validation/`)

| Skill | What it does |
|---|---|
| `prototype-builder` | Drives Lovable screen by screen to a clickable prototype, with scope guardrails baked into every prompt |
| `lead-dev-validator` | Reads your actual codebase and gives a Green / Orange / Red verdict on whether you can ship the change yourself |

### Phase 3: Delivery and post-launch (`product/delivery/`)

| Skill | What it does |
|---|---|
| `eng-handoff-writer` | Linear-ready tickets with acceptance criteria, edge cases, and an analytics-events section in every ticket |
| `launch-recap-writer` | Compares PRD targets vs Amplitude actuals honestly, ends with a keep / iterate / kill call |

## Opinionated tool choices (by design)

Granola for transcripts, Amplitude for analytics, Whimsical for flows, Lovable for prototypes. Every tool-dependent skill detects whether the integration is connected and degrades gracefully to a manual path (paste the transcript, paste the numbers, Mermaid instead of Whimsical) when it is not. Nothing fails silently, and no skill ever invents data.

## Where outputs go

Skills write their documents to a `product/` folder at the root of whatever project you run them in: `product/insights/`, `product/prds/`, `product/flows/`, `product/tickets/`, `product/recaps/`. That shared convention is how the skills find each other's outputs.

## Repo structure

```
.claude-plugin/marketplace.json    the catalog
product/                           the pm-skills plugin
  .claude-plugin/plugin.json
  discovery/skills/                phase 1 (6 skills)
  design-validation/skills/        phase 2 (2 skills)
  delivery/skills/                 phase 3 (2 skills)
```

## Contributing / adapting

Fork it. Each skill is one `SKILL.md` file; edit the ones that do not match how your team works, delete the ones you do not need, and bump the `version` in `product/.claude-plugin/plugin.json` so installers pick up the change.

## Learn to build your own

These skills are the output of the workflow I teach at Vibe Coding Academy: how to go from PM to product builder with Claude Code. The course teaches you to build skills like these for your own stack; this kit lets you start using them today.

---

**Built by [Jules Boiteux](https://roastmypricingpage.com) as a companion to [Vibe Coding Academy](https://vibecoding.academy) — the course that teaches PMs to ship with Claude Code.**

Explore the full curriculum and learn to build your own PM automation systems at [vibecoding.academy](https://vibecoding.academy).
