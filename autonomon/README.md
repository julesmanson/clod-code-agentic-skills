# Autonomon (ver 0.9.0 beta)

**9 autonomous skills** — [← back to Clod Code Agentic Skills](../README.md)

Personal, always-on workflow fixes for this repo's author, originally intended for personal use and now open to anyone who finds them useful. You do not need to type a keyword to activate any of these behaviors; the rules operate automatically. The keywords are names for the behaviors and reminders in case one is missed. See [`SKILL.md`](./SKILL.md) for the complete definition.

## 1. `generate file`

When you ask for a file that might otherwise appear only in a sandboxed preview, expect it to be written to a `GENERATED` folder at the project root. If the folder does not exist, it is created. The file keeps its real name and extension, and you are given the path where it was written.

This applies to any file type and does not require a separate confirmation. The `GENERATED` folder is a holding cell, so generated work stays separate from the rest of the project while remaining accessible in the workspace.

This exists because sandboxed files often get stored under long, hash-based names with no extension — nothing you could easily find or reuse directly. Generating the real, named file still lets the sandboxing happen underneath; it just also produces the finished, usable version in one step instead of leaving you to extract it yourself.

## 2. `terse`

Expect short answers by default: no unnecessary preamble, repetition, or trailing summary. More detail is appropriate when leaving it out would be a real point of failure: genuine ambiguity about what's meant, an irreversible action, a nuance you need to decide something correctly, or when you ask for a full explanation.

## 3. `verdict first`

When a response judges a claim you've presented — a calculation, a fact, a historical account, an argument, a policy position, a hypothesis, an opinion — Claude leads with the verdict (correct, incorrect, partly right), stated plainly, before any alternate framing, reordering, or supporting explanation.

## 4. `im thinking`

When you frame something as an impression rather than an assertion — "feels like," "im thinking," "perhaps" — expect it to be treated as an impression, not cross-examined like a factual claim. Statements about a real, identifiable person still get a gentle, honest note if something seems clearly unsupported, just not full cross-examination.

## 5. `ballpark`

When you offer a bare figure or a constructed model without hedging language, expect it read as an illustrative magnitude or idealized model by default, not a precise claim to fact-check — unless phrasing or context signals you mean something exact.

## 6. `load bearing`

When a response critiques or corrects several points at once — a debate, a review, an audit — expect the corrections that actually change the argument's strength or conclusion to come first, with accurate-but-inconsequential nitpicks compressed to a clause or left out rather than given equal billing. This doesn't apply when a task explicitly calls for exhaustive coverage regardless of weight (an `evaluate me` report, for instance).

## 7. `memory cap [N]`

Expect Claude to stay aware of a cap on the memory system — `[N]`, defaulting to 3 until you set otherwise — and mention it, rather than silently creating a new file, any time adding one would push the count past it. N is a ceiling, not a target: a high value, even set by accident, is never a reason to create files more freely toward it. What to do once flagged (fold the new content into an existing file, raise the cap, consolidate) is entirely your call.

Set the cap with `set memory files [N]` or a clear equivalent. N at or above the current file count is honored immediately, no confirmation needed. N below the current count isn't set right away — you'll get the current count reported first, since going lower means merging files, which is Your Mother's Not Here's amnesia operation to carry out, or a direct instruction from you.

## 8. `enumerate`

Multi-point responses always number their top-level points — never bullets, regardless of count. Subpoints nested under one of those points can stay as bullets for up to 3 items; past that, they switch to enumeration too, using a different scheme than the top level (letters, roman numerals, decimal sub-numbers) so the two levels don't visually blur together.

## 9. `settings report`

At the start of a new session or project, expect one terse rundown of autonomon's current settings — which mini-skills are active, current values for anything parameterized (memory-cap's N). If you don't respond, or only respond to some of it, everything else is treated as accepted as-is — this never blocks waiting on a full reply, and never re-asks.

## Related skills

- [Lern My Speak](../lern-my-speak) — the opposite direction of autonomon's always-on fixes: a session-triggered glossary that shapes how your input gets read, not how the assistant's own output gets shaped.
- [Your Mother's Not Here](../your-mothers-not-here) — memory-cap's lowering case hands off to amnesia for the actual consolidation rather than duplicating that logic here.

## Disclaimer

Use these skills at your own risk. The repository owner provides them "as is," without warranties, and is not liable for any loss, damage, claim, or consequence arising from their use, to the fullest extent permitted by law. You are responsible for reviewing outputs, commands, files, and results before relying on them.

---
[← back to Clod Code Agentic Skills](../README.md)
