---
name: flexflow
version: 1.0.0-beta
description: Relations based instructions for building SVG flowchart diagrams — CAD style relations for creation and layouts of blocks, leaders, and other UML graphics.
user-invocable: true
---

# Flexflow ver 1.0.0 beta

**Trigger:** automatically, whenever about to hand-author a new SVG UML/flowchart/sequence diagram from scratch — meant to be read before building starts, not fetched only on request. Also triggers by name ("flexflow") to re-apply or review these relations against existing diagram work.

A placement language for generating SVG UML/flowchart diagrams — every placement decision reduces to a named relation instead of a typed-in coordinate, the same discipline a CAD sketch uses; sizes and gaps hoist to single-source-of-truth values instead of getting re-chosen box by box. Not one-shot: expect iterative refinement through further prompts as a diagram takes shape, the same way any hand-authored work gets built up in passes.

**Safety rail:** first time touching a given file, recommend a commit first so the round is rollback-safe. If declined, ask whether to make a working copy instead — user's call either way.

## Defaults

Starting values for a new diagram — item 0 covers how to hold them, item 7 covers when to depart. Reach for these first; override only when content demands it.

- Title font 11.5px (bold, monospace); content 9px (sans-serif, muted), one size down (8px) in a multi-column box (item 4).
- Block aspect ratio 16:10.
- Base block size 220×137.5 — 220 is the baseline width, height derived from the ratio above.
- Minimum leader length 50px.
- Inter-block gap 50px — between every sibling pair in a row or column (item 0d).
- Leader clearance gap 50px — leader to nearest parallel line: another leader or a block edge.

## 0. Hoist theme and base size

Declare once, reference everywhere, like a linked stylesheet — tweak here, never restate elsewhere. Exact numbers vary per diagram; the principle doesn't.

Geometry:
a. Base block size — pick one size and ratio per diagram. Every block uses it exactly, growing only along the axis its content needs — x and y grow independently, never both by default.
b. Minimum leader length — one value per diagram, held by every leader: direct, mediated, split-connector stub alike; shorter reads cramped.
c. Split-connector bubble radius — pick one value, reused everywhere a bubble appears.
d. Inter-block spacing — one gap value (Equal, item 1e) between every sibling pair in a row or column. Same role CSS flexbox's `gap` plays: one space between children, independent of size.
e. Leader clearance gap — one value between a leader and the nearest parallel line: another leader or a block edge.

Theme:
a. One type scale (title vs. content face/weight/color).
b. One stroke width, one corner radius.
c. One line-style pairing: solid = direct, dashed = mediated.
d. Exactly four colors — ink (structural/text), muted (secondary content, anything not owned by the system), two branch-outcome accents (ok, warn). Adjust later if needed; never add a fifth.

## 1. Relations, not coordinates

Build placement from relations — SolidWorks's own sketch-relation model (horizontal, vertical, coincident, midpoint, equal, fix) — never typed coordinates. A relation determines the coordinate; never both.

a. Horizontal — two or more points share y, with or without a drawn reference line — e.g. boxes centered on one shared centerline.
b. Vertical — two or more points share x, same logic as Horizontal.
c. Coincident — a point lies exactly on a line or another point — e.g. a leader endpoint on a wall.
d. Midpoint — a point sits at a segment's exact midpoint. Every line enters/exits a block at a wall's midpoint — universal, no default exceptions. More than one leader on the same edge: partition it into equal lengths instead of stacking all on the midpoint — e.g. 2 leaders land at 1/3 and 2/3. Blocks may adjust as rows/columns to allow this, balanced per the priority order below.
e. Equal — a gap, length, or radius matches a reference value exactly, everywhere it recurs.
f. Fix — one point or edge held in place; everything else may grow or move around it — an anchored box grows only from its unfixed edge.
g. Grouped — not a native SolidWorks relation, this skill's own: an element sits wherever its connectors' combined path is shortest, not wherever first drawn.

Priority when these compete on sibling blocks: center first (horizontal, vertical, or both — the diagram's most important symmetry), equal size second (grow only the needed axis), midpoint entry always. Real builds produce real exceptions — handle case by case (item 7), not hardcoded here.

Think CSS Flexbox for blocks, SolidWorks relations for leaders.

## 2. Positions follow relations, not fiat

No position is final by default. Use the Grouped relation (item 1g): shortest combined connector path wins, even after placement. After moving one, recompute every line/stub on its old walls and reverify Midpoint (item 1d) on every wall touched.

## 3. Diagram modes and their sizing behaviors

a. Structural/class (divider + real content): size to content. Boxes in one row may differ in height.
b. Communication (title only): holds standard size (item 0), unmodified — title-only content never forces growth.
c. Sequence/lifeline (time flows down the page): boxes along a lifeline size to their own label; the lifeline itself is a line, not a sized block.

Exceptions happen often in a real build — items vary, content is uneven, a box needs more room than its neighbor. Expected, handled case by case (item 7); these three modes are starting behavior, not a hard ceiling.

## 4. Box anatomy — structural/class diagrams

Rhythm from the box's top edge: title → divider → first content row (gap larger than row spacing) → every row gap Equal to it (item 1e) → bottom padding Equal too. Outer margin and inner divider-to-content gap are independent values.

Growth is governed by the Fix relation (item 1f): centerline members grow symmetrically about the shared center; a box fixed on one edge grows only from its unfixed edge.

Typography: title centered, bold, monospace, full-contrast; content sans-serif, muted, left-aligned, indented left. Items are labeled, not numbered — real bullet characters, never 1/2/3. Sub-list heading matches its list's font, bold only. Multi-column boxes: one type size smaller than single-column.

Exception (item 7): a one-list box has no second column to indent against, so the block applies the Vertical relation (item 1b) to the box instead — shared x found from the block's widest line; items stay left-aligned, only the shared start-x moves. Multi-column boxes keep their shared indent, since that aligns columns to each other. A one-item box skips list treatment entirely — no bullet, no divider-relative indent — just center the single line, like a title-only block's subtitle.

## 5. Sequence/lifeline diagram anatomy

a. One lifeline per participant, each a Vertical line (item 1b) running the diagram's full height; column headers above share a Horizontal relation (item 1a).
b. Time flows down the page only — a call always arrives later (lower) than it left, never above.
c. A call between two lifelines is horizontal or elbowed, never diagonal, per item 1's Horizontal/Vertical relations.
d. A branching decision is a diamond, not a box; label the condition inside it and route each outcome leader by its own branch-outcome color (item 0).
e. An event and its payload sent as one package bundle into one bordered block instead of two labels, so "sent as one unit" reads visually, not just logically.
f. A participant not owned by the system diagrammed (a native platform object, an external service) gets the muted border, never ink — same four-color system as item 0.
g. Label clearance for this mode is its own standard value, set once and held — needn't match item 6's (16/21px horizontal, 12px vertical); different line type, different purpose.

## 6. Lines, arrows, split connectors

a. One arrowhead marker per diagram.
b. Line style follows the theme pairing (item 0), matched to the relationship's real nature — fix it once that's clear.
c. Construction/composition edges: straight — Horizontal or Vertical (item 1a/b), head-on, never diagonal. Injection/dependency edges: elbowed — two segments, each Horizontal or Vertical, meeting at a Coincident bend point (item 1c), entering the side wall's Midpoint (item 1d), never the top.
d. Color encodes meaning only, never decoration.
e. Midpoint entry/exit, always (item 1d) — never an arbitrary offset.

Split connectors — split a leader instead of letting it cross another:
a. Matching labeled marker pair (next unused letter), each with a stub into its own nearest wall — a stub may bend; the two halves needn't match in length or shape, only style and label.
b. Stub style follows direct/mediated.
c. Every stub ends in an arrowhead, no exceptions — an asymmetric connector makes any omission ambiguous.
d. Mirroring a connector's shape ≠ mirroring its arrow direction: the arrow goes on whichever end receives the relationship, not wherever its twin's arrow happens to point.

Once a diagram shows runtime communication, label every line — content font, clear of elements — with what passes along it; label a bare signal too ("no args").

Event/payload placement is fixed, not per-label judgment: on a Horizontal line (item 1a), event above, payload below; on a Vertical line (item 1b), event left, payload right. A direct call with no event name still follows the payload-side rule for its arguments. Prefer splitting a combined label into two lines over cramming one side.

Horizontal label clearance measures to the visible glyph edge, never the baseline — SVG's `y` is the baseline, and cap-height grows back toward the line on the below side, silently eating the gap. Checking each string for ascenders/descenders is fragile — wrong again the moment text changes — so use fixed offsets instead: 16px above a line, 21px below (both target the same 14px visible clearance; the gap is descender/cap-height padding the baseline doesn't account for).

Vertical label clearance is 12px, both sides, single source of truth — `text-anchor` fixes the horizontal edge exactly, so this case doesn't fight glyph geometry.

## 7. Rules can be broken — three bars

A departure is justified when:
a. It doesn't break the contract.
b. The reasoning is recorded somewhere in the package (a comment is enough).
c. It doesn't compromise clarity or safety.

Log the departure so "why does this look different" has an answer.

## 8. Notes, captions, legends, prose

a. Note: real text element, Fixed (item 1f) to the diagram's outer frame rather than its own scaling space, fixed-unit offsets, wraps naturally.
b. Caption: "Figure N — Title"; longer explanation goes in body prose.
c. Legend: only while a real distinction needs a key; drop it once moot.
d. Prose precedes the diagram, establishes vocabulary; tabular data goes in prose as a table, never in the diagram.
e. Caption/prose width is never its own cap — a caption reads at the figure's own width, never a narrower fixed measure. Fix a width rule where the figure's width is set, not a second number that can drift.
