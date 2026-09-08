---
name: thought-experiment
version: 0.1.0
description: Runs a rigorous, evidence-based audit of a target — a script, a doc, a config, a whole repo, an enterprise cloud setup, anything — by constructing concrete failure-scenario "thought experiments" and verifying every claim the target makes about a dependency's behavior against a live/authoritative source rather than memory. Applies fixes for confirmed findings, then re-runs the same audit against the fixed state to catch regressions. Triggered by the phrase "thought experiment." Iteration count is open-ended.
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

# thought-experiment — Rigorous Failure-Scenario Audits

**Trigger:** the phrase "thought experiment," or a clear equivalent ask
("find failure scenarios," "stress-test this," "leave no stone
unturned"). Never runs without an explicit ask and a clear target — this
is deliberate, not autonomous.

**Scope:** target-agnostic. A single file, a whole repo, a config, an API
contract, an infrastructure setup — anything that makes claims (about its
own behavior, its structure, or about something it depends on) that could
be wrong.

**What makes this different from a normal review:** two things.
First, it produces concrete scenarios — "given this input/this state,
here's exactly what breaks and why" — not vague "this could be cleaner"
suggestions. Second, it specifically hunts for claims the target makes
about how something *outside itself* behaves, since that class of claim
is the one most likely to be quietly wrong from memory rather than
caught by reading the target's own logic.

## Process

1. **Read the target fresh.** Pull its current, real state — files,
   configs, whatever it consists of — don't rely on earlier context about
   what it's supposed to contain.
2. **Enumerate its dependencies.** Whatever the target treats as ground
   truth outside itself: for a script — imported libraries, APIs called,
   CLI tools and their flags, environment/config assumptions; for a
   service or cloud setup — other services it talks to, permissions/IAM,
   DNS, certs, third-party APIs, network paths; for a document — every
   factual claim it makes about how something else behaves. Build this
   list deliberately — step 4 verifies it, and a skipped dependency is a
   skipped chance to catch a real bug.
3. **Construct concrete failure-scenario thought experiments.** Specific
   inputs or states that lead to a specific wrong output, crash, or
   security hole — not general impressions. Don't fix a scenario count in
   advance; keep generating them until the target's actual risk surface
   feels covered, not until an arbitrary number is hit.
4. **Verify every dependency-behavior claim a scenario hinges on** against
   a live or authoritative source — real docs, an actual API response,
   the tool's real output — rather than trusting memory. This step is
   usually where the highest-value findings are.
5. **Apply fixes** for confirmed findings.
6. **Re-run this same process against the fixed state.** A fix can
   introduce its own new problem — an accuracy fix that makes something
   else inconsistent, a corrected claim that breaks a different
   assumption elsewhere. The loop isn't done until a pass turns up
   nothing new.
7. **Report.** State each scenario's pass/fail plainly. Give full detail
   only for confirmed failures, or when detail is explicitly asked for —
   a clean pass doesn't need an essay written about it.
