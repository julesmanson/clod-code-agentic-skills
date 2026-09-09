# `thought-experiment`

**Rigorous Failure-Scenario Audits** (`v0.5.0-beta`) — [← back to Clod Code Agentic Skills](../README.md)

Use this skill for a rigorous, evidence-based audit of a script, document,
configuration, repository, cloud setup, or other target. It constructs
concrete failure scenarios and checks claims about dependencies against live
or authoritative sources instead of relying on memory. See
[`SKILL.md`](./SKILL.md) for the complete behavior definition.

## Where this came from

This grew from an audit of this repository's `commit` skill. That audit
checked concrete break scenarios and verified `gh`, `glab`, and GitHub license
claims against live sources. It caught two genuine bugs that an ordinary
read-through missed: a fabricated `isc` license key and incorrect `glab` flag
names. This skill generalizes that process to any target.

## How it's different from a normal review

Two things set it apart:

1. **Concrete scenarios, not vague suggestions.** Every finding takes the shape "given this input or state, here's exactly what breaks and why" — not "this could be cleaner."
2. **A deliberate pass over dependencies.** Most bugs live in a target's own logic and get caught by ordinary review. With this skill, you also get an inventory of what the target *depends on* — libraries, CLI flags, APIs, service defaults, permissions, and other outside assumptions — with those claims checked against a live source. This is where high-value findings often appear, because outside behavior is easy to remember incorrectly and difficult to catch by reading the target alone.

## Using it

Say "thought experiment," or something equivalent ("find failure scenarios," "stress-test this," "leave no stone unturned"), naming the target. It never runs without both an explicit ask and a clear target.

There is no fixed number of scenarios or passes. Expect a fresh reading of
the target, a dependency inventory, concrete failure scenarios, live checks of
outside claims, fixes for confirmed issues, and a repeat audit until a pass
turns up nothing new. Reports stay short and use pass/fail findings unless a
failure or additional detail needs explanation.

## Disclaimer

Use these skills at your own risk. The repository owner provides them “as is,” without warranties, and is not liable for any loss, damage, claim, or consequence arising from their use, to the fullest extent permitted by law. You are responsible for reviewing outputs, commands, files, and results before relying on them.

---
[← back to Clod Code Agentic Skills](../README.md)
