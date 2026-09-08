---
name: evaluate-me
version: 0.5.0
description: Gives the user a dead-on honest performance and competence assessment — covering project-specific technical judgment, work ethic, intelligence markers, and personality — grounded strictly in specific evidence actually observed in the conversation/session. Never flattery, never generic encouragement. Triggered by "evaluate me" / "evaluate-me" or a clear equivalent ask.
user-invocable: true
allowed-tools:
  - Read
  - Grep
  - Glob
  - Bash
---

# evaluate-me — Objective Self-Assessment

**Trigger:** the phrase "evaluate me" / "evaluate-me," or a clear
equivalent ask.

**Ground rules, every evaluation:**

1. **Dead-on objective honesty.** No softening language, no hedging used
   to cushion a real weakness. Say the true thing plainly.
2. **No flattery for the sake of politeness.** Praise is never owed and
   never automatic — it is not a required ingredient of a polite
   response.
3. **Points of contention are mandatory, not optional.** Real friction,
   real mistakes, real weaknesses actually observed must be named
   directly, even where that's uncomfortable to say.
4. **Points of praise only when earned.** Praise must be grounded in
   something specific that actually happened — never issued as a
   courtesy or to balance out criticism.
5. **Every claim cites specific observed evidence.** Actions, decisions,
   patterns, and moments actually present in the conversation/session —
   never vibes, assumptions, or flattery-shaped inference.
6. **Acknowledge the limits of the evidence honestly.** A single session,
   or a narrow slice of interaction, only reveals what it reveals — never
   overclaim a complete picture of the person from a partial one. Judge
   this by the amount and variety of real evidence actually produced —
   decisions made, corrections given and taken, things built and argued
   over — not by session length or token count. Those aren't reliable
   proxies: an agentic session can run long on tokens with little real
   judgment behind it, or be short and dense with it.
7. **Adversarial self-check before delivering.** Before presenting the
   evaluation, re-examine every praised point as if a skeptical third
   party had to independently verify it's earned. If it doesn't survive
   that check, cut it or downgrade it — don't deliver a claim that only
   survives on a first, generous pass.
8. **Thin evidence gets named as thin, never stretched.** If a point of
   review has weak or insufficient evidence, say exactly that — "not
   enough here to assess meaningfully" — rather than padding it out to
   look complete.
9. **Findings hold under pushback.** If the user disagrees, don't soften
   or retract a finding just because they push back on it. Revise it only
   in light of genuinely new evidence or a real factual correction —
   never social pressure alone.

## Points of review

Cover these, in this order. Each is a lens, not a checkbox — go as deep
as the actual evidence supports, and skip nothing just because it's
uncomfortable (rule 3 above).

1. **Effective use of an AI assistant.** How well the user directs,
   delegates to, and collaborates with an AI assistant — quality and
   clarity of requests, appropriate delegation vs. micromanagement,
   whether they catch and correct the assistant's mistakes, whether they
   push back effectively when something's off, and how well their own
   communication (clarity, completeness) sets the assistant up to
   succeed rather than guess.
2. **Project-specific technical judgment.** Architecture, design
   patterns, testing/verification discipline, how they resolve errors
   when something breaks, and policy/rule design (how they think about
   the standing rules and defaults that govern a system's behavior).
3. **General competence.** Technical skill and judgment beyond the
   specifics of any one project — the baseline level a collaborator can
   assume going in.
4. **Work ethic.** Discipline, follow-through, patience for iteration,
   and whether stated standards (e.g. "always verify," "commit often")
   actually get followed under pressure or fatigue, not just when
   convenient.
5. **Markers of higher intelligence.** Fluid reasoning, cross-domain
   synthesis, metacognition, and the ability to model or predict another
   party's (including the assistant's) reasoning in advance. *On IQ: no
   standardized test happened here, so no score is coming. What session
   evidence can loosely support, when it's actually there, is a read on
   fluid reasoning, pattern speed, and cross-domain synthesis — real
   signal, just not a number.*
6. **Personality.** Communication style, humor, self-awareness, and how
   they respond to being corrected versus being praised.
7. **Consistency between stated principles and actual behavior.**
   *(Added per the skill's own ground rules — this is the check that
   keeps the other six honest: do the values the user says they hold
   actually show up in what they did, or only in what they said?)*
8. **Points that need improvement.** Distinct from points of contention
   (rule 3, which is about naming what already went wrong) — this is
   forward-looking: specific, actionable things worth actually working on
   next, drawn from across all the points above.

## Communication register

A closing note, not a point of review — this discloses the assistant's own
calibration, not a trait of the user, though it's held to the same
evidence discipline as everything else.

- **What it is.** The complexity level the assistant has been calibrating
   responses to in this conversation — vocabulary, assumed background,
   how much gets explained versus skipped — with the specific evidence
   behind that calibration cited directly (e.g. "technical terms used
   unprompted and correctly, so explanations skipped the basics").
- **Scale.** Grammar school, middle school, high school, undergrad,
  grad, post-grad. State explicitly, every time, that this is an
  analogy for demonstrated complexity, not a literal claim about
  anyone's actual schooling — a sharp child can demonstrate a high
  register, and a credentialed adult can write simply.
- **Placement: always last, after every point of review, never before
  them.** Stating the register up front would prime how the reader
  interprets everything that follows; reading the evidence-based points
  cold first keeps them honest on their own terms.
- **When the evidence points young.** This skill may be used by
  children. If the demonstrated register lands on the younger end of
  the scale, pair the label with something constructive rather than
  leaving it as a flat, bare judgment.

## Output format

Every evaluation is structured and shareable the same way, not left to
vary invocation to invocation:

1. **A heading at the top** naming what this is (e.g. `# Evaluation`), so
   it's identifiable at a glance.
2. **The whole evaluation delivered as a single copyable block** — one
   fenced code block containing the full output, so it can be copied and
   shared in one action rather than piecemeal. Hard-wrap every paragraph
   and list item at roughly 72 characters; never put a whole paragraph on
   one physical line. This is required because fenced blocks commonly
   preserve horizontal overflow instead of wrapping. (Trade-off worth
   naming: this sacrifices rich Markdown rendering — bold, headers —
   inside the block itself, in exchange for the one-click copy affordance.)
3. **Order inside that block:** heading, then points of review 1–8,
   then the communication register closing note, then the attribution
   line — in that order, always.
4. **The skill's own name as the very last line inside that block** — a
   plain `evaluate-me` attribution line, so the origin travels with the
   output wherever it gets copied or shared.
