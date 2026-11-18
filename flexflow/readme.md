# Flexflow ver 1.0.0 beta

Relations based instructions for building SVG flowchart diagrams — [← back to Clod Code Agentic Skills](../README.md)

## What this is

Relations based instructions for building SVG flowchart diagrams — CAD style relations for creation and layout of blocks, leaders, and other UML graphics, in place of voiced approximations. Every placement decision reduces to a named relation instead of another voiced guess, the same discipline a CAD sketch uses, so a diagram stays internally consistent without re-deriving the same layout call every time one gets built. Not one-shot — still voiced, prompt by prompt, as a diagram takes shape; the difference is each prompt now names a relation instead of approximating a position, built up in passes the same way any hand-authored work is.

## Where this came from

Generalized out of the layout rules originally written for Foundry148's Blueprint page — a hand-authored architecture diagram of that project's own MVC/DI wiring. Those rules worked for one specific diagram; this skill pulls the same reasoning into something that holds for any new one. A handful of starting values (base block size, font sizes, standard gaps — see `SKILL.md`'s own Defaults section) still trace back to that original diagram as reasonable starting points; everything about how to use them is fully general.

## How it works

Three ideas carry the whole thing:

- **Relations, not coordinates.** Every placement decision is modeled as a named relation — the same sketch-relation vocabulary SolidWorks uses (Horizontal, Vertical, Coincident, Midpoint, Equal, Fix), plus Grouped, this skill's own addition with no SolidWorks equivalent — rather than a typed-in x/y. Centering is the top priority when relations compete; midpoint line-entry is universal; no position is ever final — Grouped keeps recomputing the shortest connector path as a diagram evolves.
- **Three diagram modes, three sizing behaviors.** Structural/class diagrams size to content, communication diagrams hold a fixed standard size, sequence/lifeline diagrams treat the lifeline itself as a line rather than a block.
- **Flexbox-style spacing.** One gap value, held between every sibling block in a row or column, independent of each block's own size — the same job CSS Flexbox's `gap` does.

The actual rule text lives in `SKILL.md`, in this same folder — this file describes it, it doesn't restate it. `flow1.md` was the working draft the rules were developed in; `SKILL.md` is the current, authoritative copy.

## Status — beta

The rules have been applied through multiple real diagram builds and refined against what that use actually surfaced, not just reasoned through in the abstract. Still young enough that edge cases keep turning up — handled case by case as they do, per the rule set's own "rules can be broken" item, not hardcoded in advance.

## Related skills

- [Don't Pollute Comments](../dont-pollute-comments) — same instinct, different medium: a personal standard meant to be invoked, inspected, and edited into your own house style, not accepted as-is.
- [Thought Experiment](../thought-experiment) — the methodology this skill's own rule file gets checked against directly: redundancies, collisions, dangling cross-references, stale claims. Rerun it any time the rules change, or against a diagram built from them.

## Disclaimer

Use these skills at your own risk. The repository owner provides them "as is," without warranties, and is not liable for any loss, damage, claim, or consequence arising from their use, to the fullest extent permitted by law. You are responsible for reviewing outputs, commands, files, and results before relying on them.

## License

[MIT](../LICENSE)

---
[← back to Clod Code Agentic Skills](../README.md)
