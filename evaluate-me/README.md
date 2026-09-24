# `evaluate-me`

**Objective Self-Assessment** (`v0.6.0-beta`) - [back to Clod Code Agentic Skills](../README.md)

`evaluate-me` gives you a candid, evidence-based assessment of how you are
working with an AI assistant and how you are handling a project. It is meant
for useful self-review, not for reassurance, diagnosis, or a pretend
psychological test.

The skill is model-agnostic and can be adapted to other AI models or coding
assistants with minimal changes. The complete operating definition is in
[`SKILL.md`](./SKILL.md).

## How to use it

Ask explicitly with the phrase `evaluate-me`. That exact phrase is the
trigger — no inferred equivalents.

The more real work available to inspect, the more useful the result will be.
You can ask for an evaluation based on a conversation, a workspace, a
project, a completed task, or a combination of those sources.

You can also provide context that is not visible in the current session.
The report will identify that context as information you supplied rather
than information that was independently checked.

## What you should expect

The report is direct. It names strengths only when the available evidence
supports them, and it names weaknesses without softening them merely to be
pleasant. It also says when there is not enough evidence to judge something.

The report distinguishes among:

- **Observed:** directly visible in the conversation, workspace, or files
  that were inspected.
- **Reported:** information you supplied that was not independently visible.
- **Unknown:** an area for which the available evidence is too thin.

A short, evidence-light session is judged as exactly that, not stretched
into more than it shows. A dense session with real decisions and
corrections can be more informative than a long session with little
meaningful work.

## What the report covers

Every report considers these nine areas, in this order:

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
6. **Personality** - communication style, humor, temper, warmth, patience,
   self-awareness, independence, and response to correction or praise.
   Includes highlighting humor and other social skills that help
   collaboration, and noting any defensiveness, dismissiveness, or other
   friction points.
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

   You should expect this section to rely on concrete evidence rather than
   fast replies, technical vocabulary, confidence, verbosity, or agreement
   with the assistant. When the available material is too thin, the report
   will identify that limitation instead of guessing, and may ask you for a
   specific example. This section is not an IQ score.
8. **Points that need improvement** - person-scoped, forward-looking
   behavioral or judgment patterns synthesized from points 1-7.
9. **Overall tier** - a holistic synthesis across all eight points above,
   not a computed average or a formula-driven score. You get one label
   from a small qualitative scale - Developing, Competent, Strong, or
   Exceptional - plus a sentence naming which point or two most drove
   the call.

## The communication register

The report closes with a communication-register note: not a fresh test,
but a direct read of the complexity you and the assistant were actually
operating at across the session, using only evidence already established
in the nine points above. It states which register the assistant is
calibrated to write to you at, and names the specific evidence behind
that call.

The scale runs from grammar school through post-grad. This is only an
analogy for demonstrated complexity - not a claim about your actual
schooling, credentials, or intelligence. A sharp child can demonstrate a
high register, and a credentialed adult can write simply.

Because this skill may be used by children, a register landing on the
younger end of the scale is paired with something constructive rather
than left as a flat, bare judgment.

## Report format

The complete evaluation arrives as one visually distinct block — a
Markdown blockquote — so headings, bold text, and bullets render normally
instead of showing as raw markup. Each numbered review point stays
together with its supporting text. It contains:

1. `# Evaluation`
2. The nine review areas in order
3. The communication-register note
4. The final `evaluate-me` attribution

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
to one AI brand. If you adapt the skill elsewhere, keep its evidence
standard, nine-part review order, communication-register note, blockquote
output format, and final `evaluate-me` attribution. Platform-specific
metadata such as `user-invocable` and `allowed-tools` may need to be changed.

## Related skills

- [`autonomon`](../autonomon) contains several personal workflow fixes,
  including how generated files are handled and how concise responses
  stay.

## Disclaimer

Use these skills at your own risk. The repository owner provides them “as is,” without warranties, and is not liable for any loss, damage, claim, or consequence arising from their use, to the fullest extent permitted by law. You are responsible for reviewing outputs, commands, files, and results before relying on them.

---

[Back to Clod Code Agentic Skills](../README.md) | [Read the operating definition](./SKILL.md)
