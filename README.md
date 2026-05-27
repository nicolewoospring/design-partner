# `/partner`

A Claude Code skill for product designers working natively in AI. `/partner` runs a structured co-design session, all the way from problem definition to prototyping in Verdant Playground.

---

## What a session looks like

`/partner` starts by loading relevant project context, then walks through five gated phases, with each requiring designer input before moving forward. The designer begins a session by presenting a problem, which can be anything from a simple signal to a fully formed solution that needs alternative explorations. The session helps strengthen problem definition, then crafts a set of ranked hypotheses and concrete design directions, and scaffolds selected ideas as prototypes in Verdant Playground.
---

## The five phases

**0 · Load context**
Reads context files in the home directory ~/.claude/context/ (e.g., stakeholder map, member configurations, etc.) before generating anything.

**1 · Problem statement**
The designer presents the problem in as little or as many words as appropriate. `/partner` reflects its understanding back before moving on.

**2 · Context gathering**
`/partner` asks for 2–4 additional pieces of context or relevant inputs, and reflects its analysis of the source material.

**3 · Hypotheses**
For each selected hypothesis, 3–5 solutions are generated, along with estimated effort and impact. Details on supporting signals, a confidence level, and a solution space are all included, and missing context gets flagged with specific suggestions for how to fill it.

**4 · Co-design**
3–5 solutions per selected hypothesis are generated, including effort, impact, stakeholder considerations, and a recommendation for each. Solutions are prioritized by impact-to-effort ratio.

**5 · Prototype**
After designer selection, `/partner` scaffolds a working sandbox in the Verdant Playground with each prototype accessible via a dropdown.

---

## A few things worth knowing

The skill won't push the designer toward a predetermined answer. It's built to surface tradeoffs and expand the option space; designers are expected to decide what to pursue.

If the designer has already explored some directions, they should be shared with `/partner`, and will be integrated into the hypothesis and solution generation steps when applicable, but never forced.

`/partner` is honest when signal is missing, and will surface those gaps throughout the session.

---

## Install

Requires [Claude Code](https://claude.ai/code).

```bash
curl -o ~/.claude/commands/partner.md \
  https://raw.githubusercontent.com/nicolewoospring/design-partner/main/partner.md
```

Then run `/partner` in any session.

---

Phase 5 is scoped to Spring Health's Verdant Playground and `@springcare/verdant-react`. The earlier phases work in any context.

---

## Context files

**`member-configurations.md`** — included in this repo. Covers member cohort configurations, sub-states, and the "Costs and coverage" tab visibility matrix. Place it at `.claude/context/` in your project and Phase 0 will pick it up automatically.

**`stakeholders.md`** — not included. This one should be written by you based on your team's specific stakeholder ecosystem. Place it at `~/.claude/context/stakeholders.md`. The skill will load it in Phase 0 if it exists, and flag the gap if it doesn't.
