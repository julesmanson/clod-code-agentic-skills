# Flowchart / UML guardrails

Onboarding guardrails for a new UML diagram, not a spec for automatic
generation. When a rule doesn't fit, see **Rules can be broken**.

## 0. Hoist theme and base size

Declare once, reference everywhere — like a linked stylesheet. Every
number below is a project-wide SSoT: tweak the value here, never restate
or re-derive it somewhere else in a diagram.

**Geometry:**
- Base block size: 4:3. Starter value **220 × 165**. Every other block
  uses it exactly or is explicitly derived from it (§2).
- Minimum leader segment length: **50**. Every leader segment — direct,
  mediated, or a split-connector stub — is at least this long; shorter
  reads as cramped.
- Split-connector bubble radius: **14**.

**Theme:**
- One type scale (title vs. content face/weight/color).
- One stroke width, one corner radius.
- One line-style pairing (solid = direct, dashed = mediated).
- Exactly **four** colors — ink (structural/text), muted (secondary
  content), and two branch-outcome accents (ok, warn). Tweak the four
  later if needed; don't add a fifth for a one-off.

## 1. Relations, not coordinates

Build placement from relations — the CAD model (coincident, concentric,
symmetric, equal) — not typed-in coordinates. A relation determines the
coordinate; don't choose both.

- **Equal** — a gap or connector length matches a reference value exactly,
  everywhere it recurs.
- **Centered** — an element's center sits on a shared axis.
- **Anchored** — one edge is fixed by another relation; grow only from the
  other edge.
- **Midpoint** — a leader touches a wall at its exact midpoint, running
  only vertical or horizontal, never diagonal.
- **Grouped** — an element sits wherever makes its own connectors'
  combined path shortest, not wherever it was first drawn.

## 2. Two diagram modes, two sizing behaviors

- **Structural/class** (divider + real content): size to content. Boxes in
  one row can differ in height.
- **Communication** (title only): every block uses the base size (§0),
  unmodified.

## 3. Box anatomy — structural/class diagrams

Rhythm from the box's top edge: title → divider → first content row (gap
larger than row spacing) → uniform row spacing → bottom padding equal (§1)
to row spacing. Outer diagram margin and inner divider-to-content gap are
independent values.

Growth is the anchored relation: centerline members grow symmetrically
about the shared center; anchored boxes grow only from the unanchored edge.

Typography: title = centered, bold, monospace, full-contrast. Content =
sans-serif, muted, left-aligned, indented from the left wall. Real bullet
characters. Sub-list heading matches its list's font, bold only.
Multi-column boxes: one type size smaller than single-column.

**Exception, logged per §6:** a box holding exactly one list (Fig. 1's
MODEL and CONTROLLER) has no other column to indent against, so
"indented from the left wall" doesn't apply — the block as a whole is
centered in the box instead, using its widest line to find that center.
Items still stay left-aligned to each other; only the block's shared
start-x moves. Multi-column boxes (APP) are unaffected and keep the
box-x+16 indent, since there the indent is what keeps columns aligned to
each other.

## 4. Lines, arrows, split connectors

- One arrowhead marker per diagram.
- Line style = theme pairing (§0), matched to the relationship's real
  nature — fix it the moment that's clear.
- Construction/composition edges: straight, head-on. Injection/dependency
  edges: elbowed, side wall only, never the top.
- Color = meaning only, never decoration.

**Split connectors** — if a leader would otherwise have to cross another
leader, split it instead:

- Matching labeled marker pair (next unused letter), each with a short
  stub into its own nearest wall.
- Stub style follows direct/mediated.
- Every stub ends in an arrowhead, both ends, no exceptions — an
  asymmetric connector makes any omission ambiguous, undermining every
  other intentional-looking distinction in the diagram.
- Mirroring a connector's shape ≠ mirroring its arrow direction: the arrow
  goes on whichever end actually receives the relationship, not whichever
  end its twin happened to arrow.

Once a diagram shows runtime communication, label every line — content
font, placed clear of elements — with what passes along it. Label a bare
signal too ("no args").

**Event vs. payload placement is a fixed side, not per-label judgment:**
the event/call name goes on top of a horizontal line or to the left of a
vertical one; the payload/argument data goes on the opposite side —
bottom (horizontal) or right (vertical). A direct call with no event name
still has a payload half (its arguments), so it still follows the
payload-side rule even though there's no event-side label to pair it
with. Splitting a combined "event + payload" label into two lines, one
per side, is preferred over cramming both onto one line on one side.

**Horizontal-line label clearance is measured to the visible glyph edge,
never to the text baseline** — SVG's `y` sets the baseline, not a visual
edge, so treating "baseline 14px from the line" as "14px of clearance" is
wrong on whichever side the glyphs grow back toward the line. Above a
line, glyphs mostly sit above their own baseline, so baseline-to-line
distance is close enough to real clearance — but below a line, the
glyphs' cap-height grows back *up* toward the line, silently eating into
the gap. Rather than checking each string for which specific letters
have ascenders/descenders (fragile — silently wrong again the moment the
text changes), use two fixed, conservative baseline offsets everywhere:
**16px above** a line (14px clearance + ~2px descender allowance) and
**21px below** (14px clearance + ~7px cap-height allowance). Both target
the same real 14px of visible clearance; the extra is padding for glyph
geometry the baseline itself doesn't account for.

**Vertical-line label clearance is 12px, SSoT, both sides.** Left/right
placement uses `text-anchor` to fix the horizontal edge exactly, so this
one isn't fighting glyph geometry the way the horizontal case is — a
plain symmetric gap from the line is sufficient on both the event (left)
and payload (right) side.

## 5. Positions follow relations, not fiat

No element's position is ever final by default. Use the grouped relation:
shortest combined connector path wins, even after an element's already
placed. After moving one, recompute every line/stub on its old walls, and
reverify the midpoint relation on every wall touched.

## 6. Rules can be broken — three bars

Borrowed from GD&T/ANSI Y14.5 practice. A departure is justified when:

1. It doesn't break the contract.
2. The reasoning is recorded somewhere in the package (a comment is enough).
3. It doesn't compromise clarity or safety.

Log the departure so "why does this look different" has an answer.

## 7. Notes, captions, legends, prose

- Note: real text element, anchored to the diagram's outer frame (not its
  own scaling space), fixed-unit offsets, wraps naturally.
- Caption: "Figure N — Title." Longer explanation goes in a body paragraph.
- Legend: only while a real distinction needs a key; drop it once moot.
- Prose precedes the diagram, establishes vocabulary. Tabular data goes in
  prose as a table, not in the diagram.
- **Caption/prose width is never its own cap.** A figure's caption reads at
  the same width as the figure itself, full stop — never a narrower
  fixed measure (e.g. an em-based reading-width cap) applied just because
  it looks like a paragraph. If the width rule ever needs restating, fix
  it where the figure's own width is set, not by giving caption/prose a
  second, independent number that can drift out of sync with the first.
