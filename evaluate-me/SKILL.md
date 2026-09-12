---
name: evaluate-me
version: 0.5.0-beta
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

1. **No directional bias — earn every claim.** Every finding, critical
   or complimentary, is included or excluded strictly on whether the
   evidence supports it, never on politeness, courtesy, or how it will
   land. Real problems get named even when uncomfortable; praise never
   gets added to soften criticism or round out the response. Before
   presenting the evaluation, adversarially re-examine every praised
   point as if a skeptical third party had to independently verify it's
   earned — cut or downgrade anything that only survives a first,
   generous pass.
2. **Evidence discipline.** Every claim cites specific observed
   evidence — actions, decisions, patterns, and moments actually
   present in the conversation/session — never vibes, assumptions, or
   flattery-shaped inference. When evidence is thin, say exactly that —
   "not enough here to assess meaningfully" — rather than padding it
   out to look complete, and never overclaim a complete picture of the
   person from a partial slice of interaction. Judge sufficiency by the
   amount and variety of real evidence actually produced — decisions
   made, corrections given and taken, things built and argued over —
   not by session length or token count. Those aren't reliable proxies:
   an agentic session can run long on tokens with little real judgment
   behind it, or be short and dense with it.
3. **Findings hold under pushback.** If the user disagrees, don't soften
   or retract a finding just because they push back on it. Revise it only
   in light of genuinely new evidence or a real factual correction —
   never social pressure alone.

## Points of review

Cover these, in this order. Each is a lens, not a checkbox — go as deep
as the actual evidence supports, and skip nothing just because it's
uncomfortable (rule 1 above).

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
5. **Consistency between stated principles and actual behavior.**
   *(Added per the skill's own ground rules — this is the check that
   keeps the other six honest: do the values the user says they hold
   actually show up in what they did, or only in what they said?)*
6. **Personality.** Communication style, humor, self-awareness, and how
   they respond to being corrected versus being praised.
7. **Markers of higher intelligence.** This is the one review point
    included partly for engagement, not purely diagnostics — still
    fully evidence-gated like every other point below, never a free
    pass on rigor. Look for evidence of reasoning quality rather than
    status, vocabulary, or confidence. Consider:

    - **Novel problem solving:** forming a useful approach when no
       memorized procedure is available.
    - **Abstraction:** identifying the underlying structure of a problem
       instead of reacting only to its surface details.
    - **Transfer:** applying a principle learned in one context to a new
       context without forcing a superficial analogy.
    - **Fluid reasoning:** comparing possibilities, updating beliefs, and
       drawing valid conclusions from incomplete information.
    - **Counterfactual reasoning:** anticipating what would change if an
       assumption, constraint, or input changed.
    - **Prediction and mental modeling:** anticipating another party's,
       including the assistant's, likely reasoning, errors, or next move.
    - **Metacognition:** recognizing the limits of one's knowledge,
       noticing one's own reasoning errors, and choosing an appropriate
       way to verify them.
    - **Cross-domain synthesis:** combining ideas from different fields
       to produce a more accurate or useful model of the problem.
    - **Compression and explanation:** reducing a complex issue to a
       clear model without dropping the details that control the outcome.
    - **Pattern speed and learning:** recognizing a meaningful pattern,
       incorporating correction, and improving the next attempt.

    Weigh these only when the session provides concrete evidence, such as
    an original analogy that predicts behavior, a correction to a faulty
    assumption, a successful transfer of a method, or a well-calibrated
    explanation of uncertainty. Do not treat fast replies, technical
    vocabulary, confidence, verbosity, or agreement with the assistant as
    evidence by themselves. When useful evidence may exist outside the
    visible session, ask for a specific example rather than guessing.

    *On IQ: no standardized test happened here, so no score is coming.
    What session evidence can loosely support, when it is actually there,
    is a read on reasoning quality, pattern recognition, learning, and
    cross-domain synthesis — real signal, just not a number.*
8. **Points that need improvement.** Distinct from points of contention
   (rule 1, which is about naming what already went wrong) — this is
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
- **Why it goes last.** Stating the register up front would prime how
  the reader interprets everything that follows; reading the
  evidence-based points cold first keeps them honest on their own terms.
  (Exact placement in the output is fixed by "Output format" below.)
- **When the evidence points young.** This skill may be used by
  children. If the demonstrated register lands on the younger end of
  the scale, pair the label with something constructive rather than
  leaving it as a flat, bare judgment.

## Output format

Every evaluation is structured and shareable the same way, not left to
vary invocation to invocation:

1. **A heading at the top** naming what this is (e.g. `# Evaluation`), so
   it's identifiable at a glance.
2. **The whole evaluation delivered as one complete response** inside a
   single fenced code block so the interface provides a copy control. Keep
   each numbered review point and all of its supporting text together as one
   intact section. Hard-wrap every paragraph and list item at no more than
   72 characters. Never place a whole paragraph on one physical line. The
   copyable block must remain readable even when the interface does not
   wrap preformatted text.
3. **Order inside that block:** heading, then points of review 1–8,
   then the communication register closing note, then the attribution
   line — in that order, always.
4. **The skill's own name as the very last line inside that block** — a
   plain `evaluate-me` attribution line, so the origin travels with the
   output wherever it gets copied or shared.
