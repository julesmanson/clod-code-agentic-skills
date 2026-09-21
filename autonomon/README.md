# `autonomon`

**5 autonomous skills** (`v0.5.0-beta`) — [← back to Clod Code Agentic Skills](../README.md)

Personal, always-on workflow fixes for this repo's author, originally
intended for personal use and now open to anyone who finds them useful. You
do not need to type a keyword to activate any of these behaviors; the rules
operate automatically. The keywords are names for the behaviors and
reminders in case one is missed. See [`SKILL.md`](./SKILL.md) for the
complete definition.

## 1. `generate-file`

When you ask for a file that might otherwise appear only in a sandboxed
preview, expect it to be written to a `GENERATED` folder at the project root.
If the folder does not exist, it is created. The file keeps its real name
and extension, and you are given the path where it was written.

This applies to any file type and does not require a separate confirmation.
The `GENERATED` folder is a holding cell, so generated work stays separate
from the rest of the project while remaining accessible in the workspace.

This exists because sandboxed files often get stored under long,
hash-based names with no extension — nothing you could easily find or
reuse directly. Generating the real, named file still lets the
sandboxing happen underneath; it just also produces the finished,
usable version in one step instead of leaving you to extract it
yourself.

## 2. `terse`

Expect short answers by default: no unnecessary preamble, repetition, or
trailing summary. More detail is appropriate when leaving it out could cause
a real failure, when a decision is irreversible, or when you ask for a full
explanation.

## 3. `verdict-first`

When you present a claim — a calculation, a fact, a historical account,
an argument, a policy position, a hypothesis, an opinion — expect the
verdict (correct, incorrect, partly right) as the first thing said,
before any alternate framing, reordering, or supporting explanation.

## 4. `im-thinking`

When you frame something as an impression rather than an assertion —
"feels like," "im thinking," "perhaps" — expect it to be treated as
an impression, not cross-examined like a factual claim. Statements
about a real, identifiable person still get a gentle, honest note if
something seems clearly unsupported, just not full cross-examination.

## 5. `ballpark`

When you offer a bare figure or a constructed model without hedging
language, expect it read as an illustrative magnitude or idealized
model by default, not a precise claim to fact-check — unless phrasing
or context signals you mean something exact.

## Disclaimer

Use these skills at your own risk. The repository owner provides them “as is,” without warranties, and is not liable for any loss, damage, claim, or consequence arising from their use, to the fullest extent permitted by law. You are responsible for reviewing outputs, commands, files, and results before relying on them.

---
[← back to Clod Code Agentic Skills](../README.md)
