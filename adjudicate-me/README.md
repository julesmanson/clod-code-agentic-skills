# Adjudicate Me ver 1.1.0

**Public-Content Clearance & Perception Check** - [back to Clod Code Agentic Skills](../README.md)

**Adjudicate Me** checks one piece of public-facing content — a comment, a post, an article — against two separate bars: whether it creates real security-clearance disqualification risk, and how a hiring panel or background-investigation adjudicator would likely read it. Built for aerospace/defense-track engineering job-seekers who post publicly under a traceable identity, but adaptable to any field with a formal vetting process.

## Where this came from

Built for a retired engineer preparing to return to work in US aerospace/defense, doing everything possible to get ready before re-entering the field. The underlying ten-point logic was tested through numerous rounds on Gemini first and less with Claude but climbing, then ported here as its own Claude skill.

## How to use it

Ask with the phrase `adjudicate me` or `ad me`, always paired with the content itself — a link, a file, or pasted text. The trigger doesn't run on its own; without one of those three attached, it asks for the content before doing anything else. Judgment always works from the full content, but the report only reflects it back in full for a **comment** — a **post or article** gets identified by title only, to keep the report from reproducing a long piece at length. For a link, WebFetch is always tried first regardless of platform. A login wall, bot-block, or a suspiciously short result is treated as a failed fetch — it falls back to Playwright, or asks for a direct paste. Full operating definition: [`SKILL.md`](./SKILL.md).

## What it checks

Content is classified first as one of three types — casual/satirical, serious commentary/opinion (politics, career, industry — non-technical), or technical/professional — so a serious non-technical post doesn't get forced into the wrong lens. Then two different questions, answered separately rather than blended into one score:

- **Floor — does this disqualify?** A Green/Yellow/Red light for Tier 1, Tier 3, and Tier 5 — not a bare Pass/Fail, since collapsing "might draw a question" into "disqualifying" would itself violate the real-adjudication standard below. Green is clean; Yellow is notable but survivable, not disqualifying; Red is the only real Fail and names the guideline. Tier 3 and Tier 5 share the same rulebook (SEAD 4's thirteen guidelines) and one light by default — Tier 5's zero-margin categories (foreign entanglement, coercion vulnerability, continuous-evaluation triggers, protected/export-controlled info) are the only place a Tier 3 yellow can become a Tier 5 red. Tier 1 runs on a lower bar (5 CFR 731 Suitability). Technical content gets an explicit watch for the most common real trap: casual ITAR/EAR/CUI disclosure while arguing online.
- **Ceiling — how does this read?** Two separate impressions, since an adjudicator and a hiring panel are checking for different things and can disagree: the **adjudicator's** likely read (trustworthiness, judgment, stability) and the **hiring panel's** likely read (technical credibility, communication, professionalism).

A closing **Distinction or Masterclass** flag calls out a genuinely rare or well-executed point, when the content actually earns one. Masterclass means clear command of the material; Distinction means that plus a point most people would have missed — the rarer, higher bar of the two.

## Including exchanges (optional)

Ask it to also cover exchanges with other people, not just the main piece — which ones to include is completely up to what you ask for.

## What it assumes

- The user is posting under an identity traceable back to them, pursuing a role that requires a formal security clearance. The OPSEC tradeoff in that has already been considered and accepted — this skill doesn't re-litigate it.
- The standard is real-world adjudication risk, not maximum theoretical paranoia. Casual or satirical content isn't failed for something an actual adjudicator wouldn't actually flag.

## What it is not

Not a general self-assessment of the user's skill or collaboration style. This skill judges one piece of content at a time, against one specific real-world consequence (clearance vetting and hiring perception), not the person as a whole.

## Related skills

- [Evaluate Me](../evaluate-me) — the person-scoped counterpart: assesses the user's overall collaboration and reasoning across a session, rather than one piece of public content against a vetting standard.

## Disclaimer

Use these skills at your own risk. The repository owner provides them "as is," without warranties, and is not liable for any loss, damage, claim, or consequence arising from their use, to the fullest extent permitted by law. You are responsible for reviewing outputs, commands, files, and results before relying on them.

---

[Back to Clod Code Agentic Skills](../README.md) | [Read the operating definition](./SKILL.md)
