**WARNING: DO NOT USE — NOT PRODUCTION READY, IT IS A WORK IN PROGRESS**

# Flexflow — Release 0.1.0 alpha

A reference skill, not (yet) a generator — [← back to Clod Code Agentic Skills](../README.md)

## What this is

A set of onboarding guardrails for hand-drawing a new SVG UML/flowchart diagram — not a tool that generates one automatically, but a shared placement language that keeps hand-authored diagrams internally consistent without re-deriving the same layout decisions every time one gets built.

## Where this came from

Generalized out of the layout rules originally written for Foundry148's Blueprint page (`assets/pages/blueprint/blueprint.html`) — a hand-authored architecture diagram of that project's own MVC/DI wiring. Those rules worked for one specific diagram; this skill is the attempt to pull the same reasoning out into something that holds for any new one, stripped of the specific numbers and examples that only made sense for that one reference implementation.

## How it works

Three ideas carry the whole thing:

- **Relations, not coordinates.** Every placement decision is modeled as a named relation — the same sketch-relation vocabulary SolidWorks uses (Horizontal, Vertical, Coincident, Midpoint, Equal, Fix) — rather than a typed-in x/y. Centering is the top priority when relations compete; midpoint line-entry is universal.
- **Three diagram modes, three sizing behaviors.** Structural/class diagrams size to content, communication diagrams hold a fixed standard size, sequence/lifeline diagrams treat the lifeline itself as a line rather than a block.
- **Flexbox-style spacing.** One gap value, held between every sibling block in a row or column, independent of each block's own size — the same job CSS Flexbox's `gap` does.

The actual rule text lives in `flow1.md` in this same folder; this file and `SKILL.md` describe it, they don't restate it.

## Status — not ready to publish

This exists right now specifically to check interpretation, not to ship. `flow1.md` is still being edited directly, exceptions and edge cases are being worked out as they come up rather than hardcoded in advance, and nothing has been applied back to a real diagram yet. Treat everything here as a snapshot of one point in an ongoing draft, not a finished skill.

---
[← back to Clod Code Agentic Skills](../README.md)
