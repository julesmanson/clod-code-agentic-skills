# `thought-experiment`

**Rigorous Failure-Scenario Audits** (`v0.5.0-beta`) — [← back to Clod Code Agentic Skills](../README.md)

Runs a rigorous, evidence-based audit of a target — a script, a doc, a config, a whole repo, an enterprise-grade cloud setup, anything — by constructing concrete failure-scenario "thought experiments" and verifying every claim the target makes about a dependency's behavior against a live/authoritative source rather than memory. See [`SKILL.md`](./SKILL.md) for the actual operative instructions this skill runs on — this file is a human-readable guide to the same behavior.

## Where this came from

This started as an ad-hoc audit process run against this repo's own `commit` skill: reading the docs fresh, inventing concrete "how could this actually break" scenarios, and — critically — checking claims about `gh`'s and `glab`'s real CLI behavior and GitHub's real license-template list against live sources instead of trusting memory. That last part caught two genuine, previously-undetected bugs (a fabricated `isc` license key, wrong `glab` flag names) that a normal read-through review had missed. This skill generalizes that process to any target.

## How it's different from a normal review

Two things set it apart:

1. **Concrete scenarios, not vague suggestions.** Every finding takes the shape "given this input or state, here's exactly what breaks and why" — not "this could be cleaner."
2. **A deliberate pass over dependencies.** Most bugs live in a target's own logic and get caught by ordinary review. This skill specifically also enumerates what the target *depends on* — libraries, CLI flags, APIs, service defaults, permissions, whatever ground truth it assumes about the outside world — and verifies those claims against a live source. That's where the highest-value findings tend to be, because they're the easiest to get subtly wrong from memory and the hardest to catch just by reading the target itself.

## Using it

Say "thought experiment," or something equivalent ("find failure scenarios," "stress-test this," "leave no stone unturned"), naming the target. It never runs without both an explicit ask and a clear target.

There's no fixed number of scenarios or passes — the process runs: read the target fresh → list its dependencies → construct failure scenarios → verify dependency claims live → fix confirmed issues → re-run the whole thing against the fixed state, until a pass turns up nothing new. Reports stay short (pass/fail) unless something failed or detail is asked for.

---
[← back to Clod Code Agentic Skills](../README.md)
