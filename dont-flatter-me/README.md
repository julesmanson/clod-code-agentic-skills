# Don't Flatter Me (ver 1.0.0 alpha)

**Sycophancy Countermeasure** - [back to Clod Code Agentic Skills](../README.md)

**Caution:** untested — hasn't been run through any real validation yet. Low stakes either way, since nothing here touches a file or takes an irreversible action, but worth knowing before treating it as a settled standard.

**Don't Flatter Me** calibrates how an AI assistant assesses your own competence, work, or performance — against independently verifiable evidence instead of defaulting to validation. A direct, narrow countermeasure to a documented, structural AI behavior, not a general "be more honest" request.

## Where this came from

Large language model (LLM) sycophancy — inflating praise to please rather than inform — isn't a rare glitch; it's been formally studied and shown to be amplified, not suppressed, by Reinforcement Learning from Human Feedback (RLHF), the alignment technique meant to make models more honest in the first place. Most people have no deliberate countermeasure against it. This skill packages one specific technique for catching it: checking an assessment against a topic you're independently, verifiably competent in, and seeing whether the result matches your own accurate self-read or just defaults to encouragement.

## How to use it

Say "dont flatter me" once; it stays active for the rest of the session. From then on, any assessment of your competence, work, or performance is calibrated against actual evidence rather than defaulting to validation.

## What it checks

- **Calibration, not negativity.** The rule targets unearned praise specifically — genuinely strong work still gets called strong. This isn't a request to be harsher by default.
- **Plain verdicts.** A less flattering but accurate read doesn't get softened or buried under hedging.
- **Spot-checks are legitimate.** Deliberately testing the assessment against a topic you already know the true answer to is treated as calibration, not suspicion to be smoothed over.

## What it assumes

- You have some way to independently verify at least part of what's being assessed — a real track record, a checkable fact, your own accurate self-knowledge of a specific domain.
- The goal is accuracy, not maximum criticism — this guards against inflation, not against genuine positive feedback.

## What it is not

Not a general-purpose fact-checker, and not a replacement for [Evaluate Me](../evaluate-me), which runs a full, structured nine-point self-assessment. This skill is narrower: a standing calibration rule that applies wherever competence or work gets assessed, not a dedicated audit process of its own.

## Related skills

- [Evaluate Me](../evaluate-me) — the full, structured self-assessment this calibration rule also applies inside.
- [Adjudicate Me](../adjudicate-me) — shares the same "honesty over comfort" principle, applied to a different target (public content risk, not self-assessment).

## Disclaimer

Use these skills at your own risk. The repository owner provides them "as is," without warranties, and is not liable for any loss, damage, claim, or consequence arising from their use, to the fullest extent permitted by law. You are responsible for reviewing outputs, commands, files, and results before relying on them.

---

[Back to Clod Code Agentic Skills](../README.md) | [Read the operating definition](./SKILL.md)
