# `evaluate-me`

**Objective Self-Assessment** (`v0.5.0-beta`) — [back to Clod Code Agentic Skills](../README.md)

`evaluate-me` produces a candid assessment of a person's demonstrated
performance, judgment, competence, work habits, reasoning, personality,
consistency, and areas for improvement. It is designed for evidence-based
self-review during an AI-assisted work session.

The operative instructions are in [`SKILL.md`](./SKILL.md). This README
explains the purpose, evidence standard, review structure, output contract,
and adaptation requirements without replacing the skill instructions.

## Using `evaluate-me`

Invoke it with either:

- `evaluate me`
- `evaluate-me`
- A clear equivalent request for an honest assessment of your performance
  or competence

The request must be explicit. The skill does not run merely because an
assistant notices that an evaluation might be useful.

The evaluation should use the current conversation, the visible workspace,
provided artifacts, and any other evidence the assistant is actually able to
inspect. It must not invent a longer history or treat assumptions as facts.

## Evidence standard

Every substantive claim should be tied to something observed. Useful
sources of evidence include:

- Decisions made and the reasoning given for them
- Requirements written, clarified, accepted, or rejected
- Code, configuration, documentation, tests, and review comments
- Corrections made after an error or failed validation
- How ambiguity, risk, permissions, and scope were handled
- Persistence across iterations and follow-through on stated standards
- The user's own explanations of work completed outside the visible session

The assistant must distinguish among three different states:

1. **Observed:** directly present in the conversation or inspected files.
2. **Reported:** stated by the user but not independently visible here.
3. **Unknown:** not supported by the available evidence.

Reported work may be considered as context, but it must not be presented as
independently verified. Unknown areas must be identified as thin evidence,
not filled with flattering or critical speculation.

A short session can contain strong evidence if it includes meaningful
choices, corrections, and completed work. A long session is not automatically
strong evidence merely because it contains many messages or tokens.

## Review structure

Every evaluation covers these lenses in this order. The depth of each lens
must match the evidence available.

### 1. Effective use of an AI assistant

Assess how well the user directs, delegates to, and collaborates with an AI
assistant. Consider request clarity, delegation versus micromanagement,
error detection, pushback, correction quality, and whether the user's
communication gives the assistant enough information to act without guessing.

### 2. Project-specific technical judgment

Assess architecture, design choices, testing and verification discipline,
error resolution, risk handling, and the quality of the policies or defaults
governing the project.

### 3. General competence

Assess the baseline technical skill and judgment that can reasonably be
assumed beyond one narrow project. Do not generalize from documentation
ability alone to programming ability, or from one successful task to every
technical domain.

### 4. Work ethic

Assess discipline, follow-through, patience with iteration, and whether the
user's stated standards survive fatigue, friction, and failure rather than
appearing only as intentions.

### 5. Markers of higher intelligence

Assess fluid reasoning, cross-domain synthesis, metacognition, pattern
recognition, and the ability to anticipate another party's reasoning. Do not
assign an IQ score. No session can substitute for a standardized assessment.

### 6. Personality

Assess communication style, humor, self-awareness, independence, and the
user's response to correction or praise. Keep this grounded in observed
interaction rather than personality stereotypes.

### 7. Consistency between principles and behavior

Compare the standards the user says they hold with the behavior actually
shown. Identify both alignment and contradiction. This lens prevents the
other findings from relying only on stated values.

### 8. Points that need improvement

Give specific, forward-looking actions drawn from the earlier findings. Keep
this separate from shortcomings that already occurred. Do not manufacture
improvement tasks merely to make the report look complete.

## Communication register

The communication register is a closing calibration note, not a judgment
about actual schooling or credentials. Use one of these labels:

- Grammar school
- Middle school
- High school
- Undergrad
- Grad
- Post-grad

The label is an analogy for the complexity demonstrated in the available
communication. A sharp child may demonstrate a high register, and a
credentialed adult may write simply. State that limitation every time. Place
this note after all eight review lenses and before the attribution line.

## Output contract

Every evaluation must be delivered as one copyable fenced code block.
Inside that block, use this order:

1. `# Evaluation`
2. Review lenses 1 through 8, in order
3. Communication register
4. The final attribution line: `evaluate-me`

Hard-wrap every paragraph and list item at roughly 72 characters. Do not put
an entire paragraph on one physical line, because some interfaces preserve
horizontal overflow inside fenced code blocks instead of wrapping it.

The block intentionally sacrifices rich Markdown rendering in exchange for
one-click copying. The content inside the block should remain plain,
readable, and shareable.

## What the skill does not do

- It does not claim to measure IQ.
- It does not infer a complete personality from a thin session.
- It does not turn missing evidence into a positive or negative finding.
- It does not treat user reports as independently verified facts.
- It does not soften real criticism merely to sound supportive.
- It does not issue praise merely to balance criticism.
- It does not require every personal project to use production-level process.
- It does not prescribe one universal risk model for every user or project.

## Portability

The Markdown body is model-agnostic and can be adapted to other AI models
or coding assistants with minimal edits. When porting it, preserve the
following behavior even if the host platform uses different metadata or
trigger syntax:

- Explicit invocation
- Evidence tied to observed behavior
- Clear separation of observed, reported, and unknown information
- Honest limits on thin evidence
- All eight review lenses in the stated order
- The communication-register note at the end
- One copyable, hard-wrapped output block
- The final `evaluate-me` attribution line

The YAML frontmatter is platform metadata. Adapt `user-invocable`,
`allowed-tools`, and any equivalent fields to the destination assistant's
format and capabilities. The behavioral instructions below the frontmatter
are the portable core.

## Relationship to other skills

`evaluate-me` is a self-assessment skill. It does not audit a target's
external dependency claims; that is the purpose of
[`thought-experiment`](../thought-experiment). It does not manage generated
files or response length; those are concerns of
[`autonomon`](../autonomon). It does not perform Git repository commits or
pushes; that is the purpose of [`commit`](../commit).

---

[back to Clod Code Agentic Skills](../README.md)
