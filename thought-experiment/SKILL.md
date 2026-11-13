---
name: thought-experiment
version: 0.6.0-alpha
description: Runs an evidence-based failure-scenario audit of any target, verifying claims against live sources before fixing. Triggered by "thought experiment."
user-invocable: true
allowed-tools:
  - Read
  - Grep
  - Glob
  - Bash
  - WebFetch
  - WebSearch
  - Edit
  - Write
---

# Thought Experiment ver 0.6.0 alpha — Rigorous Failure-Scenario Audits and Fixes

**Trigger:** the phrase "thought experiment," and only that phrase — no inferred equivalents. Never runs without an explicit ask and a clear target — this is deliberate, not autonomous.

**Scope:** target-agnostic. A single file, a whole project, a config, an API contract, an infrastructure setup — anything that makes claims (about its own behavior, its structure, or about something it depends on) that could be wrong.

**What makes this different from a normal review:** two things. First, it produces concrete scenarios — "given this input/this state, here's exactly what breaks and why" — not vague "this could be cleaner" suggestions. Second, it specifically hunts for claims the target makes about how something *outside itself* behaves, since that class of claim is the one most likely to be quietly wrong from memory rather than caught by reading the target's own logic.

**Pre-round commit check (safety rail):** sternly ask for, and recommend, a commit/push of any existing uncommitted changes before engaging in a round. A clean checkpoint beforehand means the round itself can always be rolled back to it if it does any damage.

## Process

1. **Read the target fresh.** Pull its current, real state — files, configs, whatever it consists of — don't rely on earlier context about what it's supposed to contain.
2. **Enumerate its dependencies.** Whatever the target treats as ground truth outside itself: for a script — imported libraries, APIs called, CLI tools and their flags, environment/config assumptions; for a service or cloud setup — other services it talks to, permissions/IAM, DNS, certs, third-party APIs, network paths; for a document — every factual claim it makes about how something else behaves. Build this list deliberately — step 4 verifies it, and a skipped dependency is a skipped chance to catch a real bug. When the target is headed to deployment specifically, also check: rollback safety, dev/prod config parity, secrets handling, the stated compatibility baseline, and first-load/real-condition performance versus dev-only testing — these don't always surface from a purely generic dependency scan. For paired documentation (a README and its SKILL.md, or docs and the code/config they describe), treat each file's claims about what the other says or does as a dependency to verify — and separately, check whether established formatting conventions (bold/casing treatment of enumerated values, heading style) are applied consistently within the target and across its sibling files, only where such a convention actually exists to check against.
3. **Construct concrete failure-scenario thought experiments.** Specific inputs or states that lead to a specific wrong output, crash, or security hole — not general impressions. Don't fix a scenario count in advance; keep generating them until the target's actual risk surface feels covered, not until an arbitrary number is hit.
4. **Verify every dependency-behavior claim a scenario hinges on** against a live or authoritative source — real docs, an actual API response, the tool's real output — rather than trusting memory. This step is usually where the highest-value findings are.
5. **Ask how fixes should be authorized, once, before applying any — CRUD options.** Read is always freely granted, never gated; only Create/Update/Delete get authorized. Blanket (every confirmed finding, no further asks), process (confirm once per round, not per file within it), file (confirm before moving to the next file's fixes), or every CRUD step (confirm each individual edit) — whichever the user picks holds for the rest of the run. Blanket covers routine confirmed findings, not an unconditional override: a genuinely surprising or higher-risk finding than what the user had in mind when granting it still gets paused on and asked about.
6. **Apply fixes** for confirmed findings, at the authorized granularity.
7. **Re-run this same process against the fixed state.** A fix can introduce its own new problem — an accuracy fix that makes something else inconsistent, a corrected claim that breaks a different assumption elsewhere. The loop isn't done until a pass turns up nothing new.
8. **Report.** State each scenario's pass/fail plainly. Give full detail only for confirmed failures, or when detail is explicitly asked for — a clean pass doesn't need an essay written about it. Tag each failure as blocking (must fix before deploy/ship) or non-blocking (safe to ship, fix after) so the report doubles as a go/no-go input, not just a findings list. Close every run with one consolidated enumerated summary, not just scenario-by-scenario mentions scattered through the process — scaled to scope: a multi-target run (several files, several skills) gets one section per target; a single clean target gets one plain verdict line, not padded ceremony.

New line, close every report with `thought experiment`.
