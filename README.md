# `/partner`

A Claude Code skill for product designers. Runs a structured co-design session — from messy problem to working prototype — without losing the rigor along the way.

---

## What a session looks like

You bring a problem. It might be fully formed or just a signal you can't ignore yet. `/partner` starts by loading any relevant project context, then walks through five gated phases — each one requires your input before it moves forward.

The output isn't a summary or a list of features. It's a set of ranked hypotheses, concrete design directions, and a scaffolded prototype you can actually click through.

---

## The five phases

**0 · Load context**
Reads project files (stakeholder maps, member configs, etc.) before generating anything. Gaps get called out upfront.

**1 · Problem statement**
You describe the problem in your own words. It reflects understanding back before moving on — no skipping ahead.

**2 · Context gathering**
Asks for the 2–4 most relevant inputs first. Synthesizes out loud as things come in. Tells you when it has enough.

**3 · Hypotheses**
4–6 hypotheses, ranked by conviction. Each has supporting signals, a confidence level, and a solution space. Missing context gets flagged with specific suggestions for how to fill it.

**4 · Co-design**
3–5 solutions per selected hypothesis. Effort, impact, stakeholder considerations, and a recommendation for each. Prioritized by impact-to-effort ratio.

**5 · Prototype**
Scaffolds a working sandbox in the Verdant Playground. One file per solution, wired into a hub with a dropdown switcher.

---

## A few things worth knowing

The skill won't push you toward a predetermined answer. It's built to surface tradeoffs and expand the option space — you decide what to pursue.

If you've already explored some directions, share them. It'll integrate what fits, skip what doesn't, and tell you which is which.

It's honest when signal is missing. "I don't have enough to be confident about X" is more useful than a confident-sounding hypothesis with nothing behind it.

---

## Install

Requires [Claude Code](https://claude.ai/code).

```bash
curl -o ~/.claude/commands/partner.md \
  https://raw.githubusercontent.com/nicolewoospring/design-partner/main/partner.md
```

Then run `/partner` in any session.

---

Phase 5 is scoped to Spring Health's Verdant Playground and `@springcare/verdant-react`. The earlier phases work in any context — swap out the prototype scaffolding if you're adapting this elsewhere.
