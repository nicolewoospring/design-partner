# Design Partner — Claude Code Skill for Product Designers

## Overview

This repository contains a Claude Code skill for Spring Health product designers working AI-natively.

**`/partner`** — A structured thought-partner session that moves from problem definition through hypothesis generation, co-design, and live prototyping in a single conversation. Designed for designers who want to think rigorously, not just move fast.

## Core Philosophy

The goal is to expand the option space, not collapse it. `/partner` is built around a few principles:

- **The designer is the decision-maker.** The skill generates and stress-tests ideas; the designer chooses what to pursue.
- **Synthesis over summaries.** It reasons out loud as context comes in — showing what's shaping the hypotheses, not just the hypotheses.
- **Honest about gaps.** Missing signal gets flagged explicitly, with suggestions for how to close it (an event, a study, a report pull).
- **Previously explored concepts are inputs, not anchors.** If the designer has done prior exploration, it integrates those directions — but only where they genuinely fit.

## How it works

The skill runs in five sequential phases. It won't advance without explicit input from the designer.

**Phase 0 — Load context**
Reads any project-specific context files (stakeholder maps, member configs, etc.) before anything else.

**Phase 1 — Problem statement**
A conversational prompt to define the problem. Reflects understanding back for alignment before moving forward.

**Phase 2 — Context gathering**
Asks for the 2–4 most relevant inputs first (funnel data, research, support signals, existing designs, etc.), synthesizes as context comes in, and signals when there's enough to generate strong hypotheses.

**Phase 3 — Hypothesis generation**
4–6 hypotheses, each with a statement, supporting signals, confidence level, and solution space. Ranked by conviction. Flags context gaps with actionable next steps.

**Phase 4 — Co-design**
3–5 design solutions per selected hypothesis, with effort/impact ratings, stakeholder considerations, and a recommended flag. Prioritized by impact-to-effort ratio.

**Phase 5 — Prototype**
Scaffolds a working prototype in the Verdant Playground. Each solution gets its own option file; a sandbox hub wires them together with a dropdown switcher.

## Installation

Requires [Claude Code](https://claude.ai/code).

```bash
curl -o ~/.claude/commands/partner.md \
  https://raw.githubusercontent.com/nicolewoospring/design-partner/main/partner.md
```

Then invoke it in any Claude Code session:

```
/partner
```

## Notes

This skill is scoped to Spring Health's design context — it references the Verdant Playground prototyping environment and Spring Care member surfaces. Some phases (especially Phase 5) assume access to `@springcare/verdant-react` and the playground repo.

Contributions and forks welcome. If you adapt it for a different context, the core phase structure translates well — just swap out the prototype scaffolding section.
