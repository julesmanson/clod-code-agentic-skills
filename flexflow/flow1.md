# Instructions for constructing UML diagrams and flowcharts from user directives — applies to edits as well as blank canvases.

## 0. Hoist theme and base size

Declare once, reference everywhere, like a linked stylesheet — every value below is a project-wide single source of truth: tweak it here, never restate or re-derive it elsewhere. Exact numbers vary per diagram; the principle doesn't.

Geometry:
a. Base block size — pick one standard size and aspect ratio for the diagram. Every block uses it exactly, growing past it only along whichever axis its own content actually needs more room on — x and y grow independently, never both by default just because one needed it.
b. Minimum leader segment length — pick one value per diagram and hold every leader to it, direct, mediated, or split-connector stub alike; shorter reads cramped.
c. Split-connector bubble radius — pick one value, reused everywhere a bubble appears.
d. Inter-block spacing — one gap value (Equal, item 1e), held between every pair of sibling blocks in a row or column. Same role CSS flexbox's `gap` plays: one consistent space between children, independent of each child's own size.

Theme:
a. One type scale (title vs. content face/weight/color).
b. One stroke width, one corner radius.
c. One line-style pairing: solid = direct, dashed = mediated.
d. Exactly four colors — ink (structural/text), muted (secondary content, and any element not owned by the system being diagrammed), two branch-outcome accents (ok, warn). Adjust the four later if needed; never add a fifth for one-off use.

## 1. Relations, not coordinates

Build placement from relations — the same sketch-relation model SolidWorks uses (horizontal, vertical, coincident, midpoint, equal, fix) — never typed-in coordinates. A relation determines the coordinate; don't choose both.

a. Horizontal — two or more points share the same y, with or without a drawn reference line — e.g. several boxes centered on one shared imaginary centerline.
b. Vertical — two or more points share the same x, same logic as horizontal.
c. Coincident — a point lies exactly on a specific line or another point — e.g. a leader endpoint landing exactly on a wall.
d. Midpoint — a point sits at the exact midpoint of a segment. Every line enters or exits a block at a wall's midpoint — not an example case, a universal rule with no default exceptions.
e. Equal — a gap, length, or radius matches a reference value exactly, everywhere it recurs.
f. Fix — one point or edge is held in place; everything else may still grow or move around it — an anchored box grows only from its unfixed edge.
g. Grouped — not a native SolidWorks relation, specific to this skill: an element sits wherever makes its own connectors' combined path shortest, not wherever first drawn.

Priority when these compete on inline/sibling blocks: center first (horizontal, vertical, or both — this is the diagram's most important symmetry), hold equal size second (grow only the axis that actually needs it), midpoint entry always (every line, every wall, no exceptions by default). Real builds produce real exceptions to any of this — handle them case by case (item 7), not by hardcoding a carve-out here.

## 2. Diagram modes and their sizing behaviors

a. Structural/class (divider + real content): size to content. Boxes in one row may differ in height.
b. Communication (title only): holds its standard size (item 0), unmodified — title-only content never forces growth.
c. Sequence/lifeline (time flows down the page): boxes along a lifeline size to their own label; the lifeline itself is a line, not a sized block.

Exceptions to any of the above happen often in a real build — items vary, content is uneven, a box needs more room than its neighbor. That's expected and handled case by case (item 7); these three modes describe the default starting behavior, not a hard ceiling.

## 3. Box anatomy — structural/class diagrams

Rhythm from the box's top edge: title → divider → first content row (gap larger than row spacing) → every row gap Equal to that one row-spacing value (item 1e) → bottom padding Equal to it too. Outer diagram margin and inner divider-to-content gap are independent values.

Growth is governed by the fix relation: centerline members grow symmetrically about the shared center; a box fixed on one edge grows only from its unfixed edge.

Typography: title centered, bold, monospace, full-contrast; content sans-serif, muted, left-aligned, indented from the left wall. Items are labeled, not numbered — real bullet characters, never 1/2/3. Sub-list heading matches its list's font, bold only. Multi-column boxes: one type size smaller than single-column.

Exception (logged per item 7): a box holding exactly one list has no second column to indent against, so the block applies the Vertical relation (item 1b) to the box instead — shared x between block and box, found from the block's widest line; items stay left-aligned to each other, only the shared start-x moves. Multi-column boxes keep their shared indent, since there it aligns columns to each other.

## 4. Sequence/lifeline diagram anatomy

a. One lifeline per participant, each a Vertical line (item 1b) running the diagram's full height; column headers above them share a Horizontal relation (item 1a) with each other.
b. Time flows down the page only — a call always arrives later (lower) than it left, never above.
c. A call between two lifelines is a horizontal or elbowed leader, never diagonal, following item 1's horizontal/vertical relations.
d. A branching decision is a diamond, not a box; label the condition inside it and route each outcome leader by its own branch-outcome color (item 0).
e. When an event and its payload are sent together as one package, bundle them into one bordered block instead of two separate labels, so "sent as one unit" reads visually, not just logically.
f. A participant not owned by the system being diagrammed (a native platform object, an external service) gets the muted border treatment, never the primary ink border — same four-color system as item 0, applied to this mode.
g. Label clearance for this mode is its own standard value, set once and held — it doesn't have to match item 5's bus-line clearance, since it's a different line type serving a different purpose.

## 5. Lines, arrows, split connectors

a. One arrowhead marker per diagram.
b. Line style follows the theme pairing (item 0), matched to the relationship's real nature — fix it the moment that's clear.
c. Construction/composition edges: straight — Horizontal or Vertical (item 1a/b), head-on, never diagonal. Injection/dependency edges: elbowed — two segments, each Horizontal or Vertical, meeting at a Coincident bend point (item 1c), entering the side wall's Midpoint (item 1d), never the top.
d. Color encodes meaning only, never decoration.
e. Every line enters and exits at a wall's midpoint (item 1's midpoint relation) — never an arbitrary offset.

Split connectors — split a leader instead of letting it cross another:
a. Matching labeled marker pair (next unused letter), each with a stub into its own nearest wall — a stub may bend, and the two halves of a pair don't need to match each other in length or shape, only in style and label.
b. Stub style follows direct/mediated.
c. Every stub ends in an arrowhead, both ends, no exceptions — an asymmetric connector makes any omission ambiguous.
d. Mirroring a connector's shape ≠ mirroring its arrow direction: the arrow goes on whichever end receives the relationship, not whichever end its twin arrows.

Once a diagram shows runtime communication, label every line — content font, clear of elements — with what passes along it; label a bare signal too ("no args").

Event vs. payload placement is fixed, not per-label judgment: on a Horizontal line (item 1a), event/call name above, payload/argument data below; on a Vertical line (item 1b), event left, payload right. A direct call with no event name still follows the payload-side rule for its arguments. Prefer splitting a combined label into two lines over cramming both onto one side.

Horizontal label clearance measures to the visible glyph edge, never the baseline — SVG's `y` is the baseline, and glyphs' cap-height grows back toward the line on the below side, silently eating the gap. Checking each string for which letters have ascenders/descenders is fragile — silently wrong again the moment the text changes — so use fixed offsets everywhere instead: 16px above a line, 21px below (both target the same real 14px visible clearance; the difference is descender/cap-height padding the baseline doesn't account for).

Vertical label clearance is 12px, both sides, single source of truth — `text-anchor` fixes the horizontal edge exactly, so this case doesn't fight glyph geometry.

## 6. Positions follow relations, not fiat

No position is final by default. Use the grouped relation: shortest combined connector path wins, even after an element is already placed. After moving one, recompute every line/stub on its old walls and reverify the midpoint relation on every wall touched.

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
e. Caption/prose width is never its own cap — a caption reads at the figure's own width, full stop, never a narrower fixed measure. Correct a width rule where the figure's width is set, not with a second independent number that can drift out of sync.

## 9. Project Specific - Blueprint

Let Figures 1 and 2 serve as models for diagrams
Payload events ride at left of or on top of bus line
Payload data like content or components ride at right of on bottom of bus line
Direct communication uses solid bus Line
Mediated communication uses dashed bus Line
