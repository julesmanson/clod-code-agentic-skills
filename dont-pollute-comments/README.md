# Don't Pollute Comments (ver 1.0.0 beta)

**One person's comment-writing standard** — [← back to Clod Code Agentic Skills](../README.md)

This is built from the comment-style section of a real project's own governing doc, then verified against that project's actual files rather than left as generic "best practices" for a general audience. It's one specific person's own standard, kept in their own voice.

## What this actually fixes

This came out of a recurring, directly observed pattern in one real project, not a formal survey of AI coding assistants generally: manually breaking a long comment into several short physical lines, each roughly the same character count. The habit itself is a well-documented holdover from decades of code written to an 80-column terminal convention. It reads fine in the one exact context it was written for, and breaks the moment that context changes. A hardwrapped line break is fixed; it doesn't know the file panel just got narrower, the font got bigger, or the editor zoomed in — so the comment reflows at the wrong points and the result reads as jagged, broken prose instead of a paragraph. That matters beyond aesthetics: zooming in is a real accessibility accommodation (the same spirit ARIA exists in — adapting to how someone actually needs to read the page, not how it happened to be authored), and a block that only looks right at one specific zoom level fails exactly the people depending on a different one.

The fix is to stop pre-breaking it at all. A comment block gets treated the same as a paragraph of prose on an article page — flush left, one logical line per paragraph, left to the editor's own soft-wrap to reflow at whatever width or zoom it's actually being read at.

The other common habit this pushes back on is over-commenting — a comment on every line regardless of whether the code already says it. If a name or structure already makes something obvious, restating it isn't documentation, it's noise sitting on top of code that didn't need narrating. The default stays terse specifically so a comment still stands out when one is actually warranted; a block is reserved for a real explanation that doesn't fit a short line, not padding to make a file look documented.

**Call it by name, every time** — `dont-pollute-comments`, or a clear equivalent ask. This is deliberately not autonomous, and that's a feature, not an omission. An always-on rule baked into your own `CLAUDE.md` is one thing, because you wrote it and you know it's there. A skill picked up from someone else's repo is different — silently reshaping your comments without you ever having to ask for it would be a bad trade for a convenience you didn't request. Being called out by name is the one courtesy you're owed in exchange.

## Great starter template for one's own style

That courtesy is also what makes this a genuinely good starting template, not just a fixed ruleset to take or leave. Invoke it, see exactly what it does to a real comment in your own codebase, then open [`SKILL.md`](./SKILL.md) and edit it until it's *your* house style instead of someone else's. Nothing here assumes every line survives that trip unchanged — it's meant to be a template for editing in your own rules of comment style.

## Correcting a stale comment

Never rewrite someone else's existing comment wholesale just because part of it is wrong now. Fix the fact that's gone stale — a wrong path, a changed behavior, a reference to code that no longer exists — and leave everything else alone: the original wording, its terse or list structure, its voice. The fix itself doesn't get documented inline either; no "updated to reflect X." A corrected comment should read as if it was always right, not as a visibly patched one.

## The unified rules

A comment block should read structurally the same as prose on an article page: paragraphs separated by a blank line, each one flowing left-to-right and wrapping naturally, nothing indented, nothing manually broken mid-sentence. That picture covers most of what follows.

Before anything language-specific, nine rules apply everywhere:

- Content is current-state facts and usage contract only — never debugging narrative or a cross-reference that means nothing without a sibling file open.
- Don't comment the obvious. If a name or structure already makes something clear, restating it is noise, not documentation — most well-named code needs nothing said about it at all. A comment earns its place with a non-obvious why, not a translation of what's already readable.
- Default to the shortest form that loses no information. Multi-line is the exception, not the default.
- A comment block — a long explainer spanning more than one line — sits flush left, zero indentation, no matter how deeply the code around it is nested, every line included, not just its opening delimiter. This is about accessibility, not just taste: heavy zoom is itself an accommodation, and a block whose lines soft-wrap from different starting columns reads as jagged at high zoom. Short inline/trailing comments are exempt — they never wrap, so this doesn't apply to them.
- Never hardwrap a comment block across physical lines, even one long enough to justify several paragraphs — each paragraph is one long line the editor soft-wraps, separated from the next by a blank line, never manually broken mid-paragraph no matter how long that one line gets. Same accessibility reasoning as the flush-left rule above.
- A longer-than-usual comment is reserved for genuine variance — a non-obvious value, a tradeoff, a reason something is tuned the way it is — not handed out uniformly regardless of language.
- A short list of items can be several short lines, one per item, with a one-line heading if the list runs long.
- An unused-looking property or variable sitting among similarly-named ones gets left alone, not flagged as dead.
- A page/file heading, for CSS, is unconditional — exactly one per file, every file, no exceptions. Three lines (border, title, border), flush left, no indent. Title line is `/***** TITLE *****/` (five stars, one space each side); borders match its width. In other `/* ... */`-capable languages (which excludes HTML) this has only been observed once, on a single exemplar file — a single data point to extend cautiously, not a confirmed rule.

## JavaScript

Trailing `//` is the default shape. A component or module also gets its own standalone top-of-file comment — one soft-wrapped line stating what it is and its usage contract, written for a stranger reusing the file alone with nothing else open. This doesn't conflict with "don't comment the obvious" above — a real usage contract is rarely fully obvious from a tag name alone, even for a simple component. The one exception with its own layout is JSDoc — an opening `/**` earns its own line when `@param`/`@returns` need real highlighting, nothing fancier required after that. A short list can run as several trailing `//` lines, but if each item already has its own code line, a trailing `//` on that line beats a separate comment-only list.

## CSS

Trailing `/* ... */` naming where or who uses a rule is the default — most selectors are already self-documenting by name, so restating what a rule visually does is noise. Superseded code gets commented out rather than deleted, with the block's first line naming what it was and what replaced it — keeps the history inspectable right in the file, not just buried in git log.

## HTML

Almost no comments at all — markup rarely has a non-obvious fact worth recording. The one legitimate use is temporarily disabling a tag mid-edit, the same way you'd comment out a line of code while working. It's not a place to park permanent documentation; once the edit's done, the tag comes back or gets deleted.

## Disclaimer

Use these skills at your own risk. The repository owner provides them "as is," without warranties, and is not liable for any loss, damage, claim, or consequence arising from their use, to the fullest extent permitted by law. You are responsible for reviewing outputs, commands, files, and results before relying on them.

---
[← back to Clod Code Agentic Skills](../README.md)
