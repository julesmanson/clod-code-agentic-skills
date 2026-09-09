# `evaluate-me`

**Objective Self-Assessment** (`v0.5.0-beta`) - [back to Clod Code Agentic Skills](../README.md)

`evaluate-me` gives you a candid, evidence-based assessment of how you are
working with an AI assistant and how you are handling a project. It is meant
for useful self-review, not for reassurance, diagnosis, or a pretend
psychological test.

The skill is model-agnostic and can be adapted to other AI models or coding
assistants with minimal changes. The complete operating definition is in
[`SKILL.md`](./SKILL.md).

## How to use it

Ask explicitly with a phrase such as:

- `evaluate me`
- `evaluate-me`
- "Give me an honest assessment based on this session."
- "Evaluate my work on this project so far."

The more real work available to inspect, the more useful the result will be.
You can ask for an evaluation based on a conversation, a workspace, a
project, a completed task, or a combination of those sources.

You can also provide context that is not visible in the current session.
That context can be included, but the report should make clear that it was
reported by you rather than independently checked.

## What you should expect

The report is direct. It names strengths only when the available evidence
supports them, and it names weaknesses without softening them merely to be
pleasant. It also says when there is not enough evidence to judge something.

The report distinguishes among:

- **Observed:** directly visible in the conversation, workspace, or files
  that were inspected.
- **Reported:** information you supplied that was not independently visible.
- **Unknown:** an area for which the available evidence is too thin.

This prevents a short session from being inflated into a complete judgment
and prevents missing evidence from being mistaken for evidence of failure.
A dense session with real decisions and corrections can be more informative
than a long session with little meaningful work.

## What the report covers

Every report considers these eight areas, in this order:

1. **Effective use of an AI assistant** - how clearly you communicate,
   delegate, review, correct, and push back.
2. **Project-specific technical judgment** - architecture, design choices,
   verification, error handling, risk, and governing rules.
3. **General competence** - what technical skill and judgment can reasonably
   be inferred beyond one narrow task.
4. **Work ethic** - discipline, follow-through, iteration, and behavior when
   work becomes tiring or difficult.
5. **Consistency between principles and behavior** - whether the values and
    standards you state appear in your actual decisions and actions.
6. **Personality** - communication style, self-awareness, independence,
   humor, and response to correction or praise.
7. **Markers of higher intelligence** - evidence of reasoning quality rather
    than status, vocabulary, or confidence. This includes:

    - **Novel problem solving:** forming a useful approach when no memorized
       procedure is available.
    - **Abstraction:** identifying the underlying structure of a problem
       instead of reacting only to surface details.
    - **Transfer:** applying a principle learned in one context to a new
       context without forcing a superficial analogy.
    - **Fluid reasoning:** comparing possibilities, updating beliefs, and
       drawing valid conclusions from incomplete information.
    - **Counterfactual reasoning:** anticipating what would change if an
       assumption, constraint, or input changed.
    - **Prediction and mental modeling:** anticipating another party's,
       including the assistant's, likely reasoning, errors, or next move.
    - **Metacognition:** recognizing the limits of your knowledge, noticing
       reasoning errors, and choosing an appropriate way to verify them.
    - **Cross-domain synthesis:** combining ideas from different fields to
       produce a more accurate or useful model of the problem.
    - **Compression and explanation:** reducing a complex issue to a clear
       model without dropping details that control the outcome.
    - **Pattern speed and learning:** recognizing meaningful patterns,
       incorporating correction, and improving the next attempt.

    These markers require concrete evidence. Fast replies, technical
    vocabulary, confidence, verbosity, or agreement with the assistant do
    not count as evidence by themselves. If the available material is too
    thin, the report should say so or request a specific example rather than
    guessing. This section does not provide an IQ score.
8. **Points that need improvement** - specific, practical next steps drawn
   from the preceding evidence.

## The communication register

The report ends with a communication-register note. This places the
complexity of the language and reasoning demonstrated in the session on a
scale from grammar school through post-grad.

This is only an analogy for demonstrated complexity. It is not a claim about
your actual schooling, credentials, or intelligence. A sharp child can
demonstrate a high register, and a credentialed adult can write simply.

## Report format

The complete evaluation arrives as one readable block with natural wrapping
and a copy control. Each numbered review point stays together with its
supporting text so the report is easy to copy and paste. It contains:

1. `# Evaluation`
2. The eight review areas in order
3. The communication-register note
4. The final `evaluate-me` attribution

The output remains wrapped for readability while retaining the copy feature.

## What it is not

`evaluate-me` does not provide an IQ score, a clinical diagnosis, or a
complete personality profile. It does not pretend that a thin session is a
complete history. It does not require a personal toy project to follow
production-level process, and it does not treat one universal risk model as
appropriate for every person or project.

It is also not a replacement for feedback from people who have actually
worked with you over time. It is a structured reading of the evidence made
available to the AI assistant at the time of the request.

## Portability

The behavioral instructions are written in ordinary Markdown and are not tied
to one AI brand. When adapting the skill elsewhere, preserve its evidence
standard, eight-part review order, communication-register note, copyable
output format, and final `evaluate-me` attribution. Platform-specific
metadata such as `user-invocable` and `allowed-tools` may need to be changed.

## Related skills

- [`thought-experiment`](../thought-experiment) stress-tests a target by
  constructing concrete failure scenarios and checking outside claims
  against authoritative sources.
- [`autonomon`](../autonomon) contains small personal workflow fixes for
  generated files and concise responses.
- [`commit`](../commit) handles repository commits and pushes.

## Disclaimer

Use these skills at your own risk. The repository owner provides them “as is,” without warranties, and is not liable for any loss, damage, claim, or consequence arising from their use, to the fullest extent permitted by law. You are responsible for reviewing outputs, commands, files, and results before relying on them.

---

[Back to Clod Code Agentic Skills](../README.md) | [Read the operating definition](./SKILL.md)
