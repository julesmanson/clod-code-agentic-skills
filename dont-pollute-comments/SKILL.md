---
name: dont-pollute-comments
version: 1.0.0-beta
description: One person's own comment-writing standard, built from a real project's governing doc and checked against that project's own real files rather than written fresh for a general audience. Covers correcting stale comments, a unified rule set for every language, then specifics for JavaScript, CSS, and HTML. Triggered explicitly by name — not autonomous, so you always know when it's shaping your comments and can adopt it on your own terms.
user-invocable: true
allowed-tools:
  - Read
  - Edit
  - Write
  - Grep
---

# Don't Pollute Comments ver 1.0.0 beta

**Trigger:** explicit only — the phrase "dont-pollute-comments," or a clear equivalent ask. Deliberately not autonomous: unlike a rule baked silently into your own CLAUDE.md, a skill picked up from someone else's repo owes you the courtesy of being called out by name, so you always know when it's active rather than discovering it secondhand in your own diffs.

These are one person's own standing rules, drawn from a real project's own governing doc and verified against that project's actual files rather than written fresh as generic advice for a general audience. Adopt them as given, or edit this file to match your own project's conventions — nothing here assumes you'll keep every line.

## Correcting a stale or inaccurate comment

Never rewrite someone else's existing comment wholesale. Fix only the fact that's gone stale — a wrong file path, a behavior that changed, a reference to code that no longer exists — and preserve everything else about it: the original wording, its terse or list structure, its voice. The correction itself gets no narrative of its own — no "updated to reflect X," no "this used to say Y." The comment should read as if it was always accurate, not as a patched record of having been wrong.

## Unified rules (every language)

A comment block should read structurally the same as prose on an article page: paragraphs separated by a blank line, each paragraph flowing left-to-right and wrapping naturally, nothing indented, nothing manually broken mid-sentence. That one picture covers most of what follows.

1. **Content is current-state facts and usage contract only.** Never debugging or correction narrative ("an earlier version tried X..."), never a cross-reference to a sibling file or an internal project nickname that means nothing to a reader who only has this one file open.
2. **Don't comment the obvious.** If a name, structure, or the code itself already makes something clear, restating it in a comment is noise, not documentation — most well-named classes, ids, variables, and functions need nothing said about them at all. A comment earns its place by adding something the code can't say for itself: a non-obvious why, a tradeoff, a usage contract — not a translation of what's already readable.
3. **Default to the shortest form that preserves every fact.** A multi-line block is the exception to justify, not the default. Compress wording to the shortest sentence that loses no information — merge split sentences, drop restated words ("itself," "own," "already").
4. **A comment block (a long explainer spanning more than one line) sits flush left, zero indentation, regardless of code nesting.** Not roughly aligned, not one space in — literally the first character on the line is where the comment's own text starts, on every line of the block, not just its opening delimiter. This is an accessibility concern, not just a style preference: zooming in heavily is itself an accommodation, and an indented block whose lines soft-wrap at different horizontal starting points reads as jagged and harder to track at high zoom than one that starts at the same column every line. Short inline/trailing comments are exempt — a one-liner that never wraps doesn't have this problem, so it can stay aligned with the code it sits next to.
5. **Never hardwrap a comment block across physical lines, even one that's justified in being long.** Each paragraph is one long line the editor soft-wraps, not several manually broken ones — a fixed line break looks jagged at heavy zoom or in a narrow panel, the same accessibility reasoning as rule 4. A block earning several paragraphs (real mechanism to explain, not padding) separates them with a blank line — multiple paragraphs are fine and often clearer than one wall of text — but it still doesn't hard-wrap within any single paragraph, however long that one line runs.
6. **A longer comment than usual is reserved for genuine variance** — a non-obvious value, a tradeoff, a reason something is tuned the way it is — not applied uniformly to every line regardless of language. Most lines still get the terse default; the longer one earns its length.
7. **A list-like comment can be several short lines, one per item** — but each line has to stay short enough to never wrap under zoom or in a narrow files panel. A long list gets a one-line heading or explainer first.
8. **An unused-looking property or variable sitting among a series of similarly-named ones is left alone, not flagged.** Don't assume dead code from appearance alone.
9. **Page/file heading block** (optional — used selectively, not on every file): exactly one per file, three self-closing lines — border, title, border — flush left, no indent. Title line is `/***** TITLE *****/` (five stars, one space each side); border lines are solid stars matching the title line's full width. Valid in any language whose comment syntax supports `/* ... */`.

## JavaScript specifics

- **Default shape is one trailing `//` comment.** A multi-line block is the exception to justify.
- **A component or module gets one standalone top-of-file comment** — a single soft-wrapped `/* ... */` line stating what it is and its usage contract, written as if for a stranger reusing the file alone with no other context. This doesn't conflict with "don't comment the obvious" above — a real usage contract (settings, extension points, what's required vs. optional) is rarely fully obvious from a tag name alone, even for a simple component.
- **JSDoc exception:** when `@param`/`@returns` need real highlighting, the opening `/**` (not `/*`) is the one load-bearing case where the block gets its own line. Per-line stars or indentation after that opening line aren't required.
- **List-like content** can be several short trailing `//` lines, one per item — but where each item already maps to its own code line, prefer a trailing `//` on that line over a standalone comment-only list.

## CSS specifics

- **Default shape is a trailing `/* ... */` stating where or who uses the rule.** Most classes/ids are already self-documenting by name — restating what a rule visually does is noise.
- **Superseded code gets commented out, not deleted** — wrapped in a `/* ... */` block whose first line says what it is and what replaced it. Keeps the dead code's history inspectable instead of only living in git log.

## HTML specifics

- **Almost no comments at all.** HTML is markup, not logic — there's rarely a non-obvious fact worth recording next to a tag.
- **The one legitimate use: temporarily disabling a tag during active work**, the same way you'd comment out a line of code mid-edit — not a permanent documentation comment. Once the work is done, the commented-out tag either comes back or gets deleted; it doesn't stay parked indefinitely.
