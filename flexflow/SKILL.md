---
name: flexflow
version: 0.1.0-alpha
description: Relation-based guardrails for hand-authoring a new SVG UML/flowchart diagram — CAD-style placement relations modeled on SolidWorks, three diagram-mode anatomies (structural/class, communication, sequence/lifeline), and flexbox-style inter-block spacing.
user-invocable: true
---

# Flexflow — Release 0.1.0 alpha

**Trigger:** automatically, whenever about to hand-author a new SVG UML/flowchart/sequence diagram from scratch — these are onboarding guardrails, meant to be read before building starts, not fetched only on request. Also triggers by name ("flexflow") to re-apply or review the guardrails against existing diagram work.

Not a spec for automatic generation — a shared placement language so hand-drawn SVG diagrams stay internally consistent without re-deriving the same layout decisions from scratch each time.

**Safety rail:** first time touching a given file, recommend a commit first so the round is rollback-safe. If declined, ask whether to make a working copy instead — user's call either way.

## What it covers

The full rule set lives in `flow1.md`, in this skill's own directory. Read it in full before building. Shape, at a glance:

- **Item 0** — hoisted, project-wide values: base block size, minimum leader length, split-connector bubble radius, inter-block spacing (CSS flexbox `gap` analog), and the theme (one type scale, one stroke width, exactly four meaningful colors).
- **Item 1** — placement by relation, not typed coordinates: Horizontal, Vertical, Coincident, Midpoint, Equal, Fix (all modeled on SolidWorks sketch relations), plus Grouped (specific to this skill, no CAD equivalent). Centering is the top-priority relation; midpoint line-entry is a universal rule.
- **Item 2** — three diagram modes and how each one sizes: structural/class (sizes to content), communication (fixed standard size), sequence/lifeline (lifelines are lines, not blocks).
- **Items 3–4** — box anatomy for structural/class diagrams, and full anatomy for sequence/lifeline diagrams (lifelines, time flowing downward, decision diamonds, bundled event+payload packages, non-owned-participant border treatment).
- **Item 5** — lines, arrows, split connectors, and label placement/clearance rules.
- **Item 6** — positions are never final; re-derive from relations after every move.
- **Item 7** — rules can be broken, under a three-part test (doesn't break the contract, reasoning is logged, doesn't compromise clarity/safety).
- **Item 8** — notes, captions, legends, and prose conventions.

## Status

Actively being edited directly in `flow1.md` as of this version — not yet finalized, not yet applied back to any real diagram. `assets/pages/blueprint/blueprint.html` in Foundry148 is the reference implementation these guardrails were generalized from, and stays untouched until the rules themselves are settled.
