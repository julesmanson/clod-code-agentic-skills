---
name: adjudicate-me
version: 1.2.0
description: Evaluates one piece of public-facing content (a comment, post, or article) for US security-clearance disqualification risk at Tier 1, Tier 3, and Tier 5 as an adjudicator would judge it, and for how an aerospace/defense hiring panel would likely perceive it. Triggered by the phrase "adjudicate me" or "ad me."
user-invocable: true
allowed-tools:
  - Read
  - WebFetch
  - Playwright MCP tools (for content WebFetch can't reliably render)
---

# Adjudicate Me ver 1.2.0

**Trigger:** the phrase "adjudicate me" or "ad me," always accompanied by the content itself — a link, a file, pasted text, or a screenshot. No inferred equivalents.

**Scope:** judges one specific piece of content — a comment, post, article, or similar public-facing material — not the user's overall competence, collaboration style, or reasoning across a session. This skill never substitutes for a broader, person-scoped self-assessment.

**Ground rules:**

1. **Content is mandatory, not optional.** The trigger only runs once the content is actually attached — a link, a file, pasted text, or a screenshot. If the trigger arrives with none of those three, stop and ask for one before doing anything else; never adjudicate a paraphrase, a summary, or a vague description — judgment always works from the full content. What gets echoed back in the report differs by type: a **comment** is reflected back in full (short enough to cost nothing, and keeps the report self-contained). A **post or article** is reflected back by **title only** — still judged on the full text, just not reproduced at length in the report. For a link: always try WebFetch first, regardless of platform. A login wall, anti-bot block, or a result clearly shorter than the real content is a hard stop — switch to Playwright when available, or tell the user the fetch failed and ask for a direct paste.
2. **Standing context.** The user is pursuing a mechanical engineering role in US aerospace/defense requiring a security clearance, and posts publicly under an identity traceable back to them. The OPSEC tradeoff in that choice has already been considered and accepted by the user — don't re-raise it as a fresh warning.
3. **Objective.** Tier 3 and Tier 5 share the same rulebook — SEAD 4's thirteen adjudicative guidelines — differing only in margin. Tier 5 applies zero-margin scrutiny to foreign entanglement, coercion/blackmail vulnerability, continuous-evaluation triggers, and handling of protected or export-controlled technical information (Guideline K, ITAR, EAR, CUI). Tier 1 runs on a lower bar: 5 CFR 731 Suitability. Every Red traces to a specific guideline.
4. **Honesty over comfort.** Give the real read, not the comfortable one — don't soften a finding to spare feelings. Other readers' reactions (upvotes, replies, pile-on) are irrelevant to this skill's judgment; the only audiences that matter are a background-investigation adjudicator and a hiring panel.
5. **Calibrate against real adjudication, not maximum paranoia.** Don't fail casual or satirical content for something an actual adjudicator would shrug off. The standard is genuine disqualification risk, not theoretical worst-case caution.

**Process:**

1. Display the content (ground rule 1). **Exchanges, optional:** when asked to also include comment exchanges with others, not just the main piece, select based on user instructions.
2. Classify it as one of three types — **casual/satirical**, **commentary/opinion** (serious but non-technical — politics, career, industry topics), or **technical/professional** — then light-rate Tier 1, Tier 3, and Tier 5 separately as **Green**, **Yellow**, or **Red**:
   - **Green** — clean. Reported with a terse 1-line reason.
   - **Yellow** — not disqualifying, but notable enough to draw a question; survivable if handled honestly. Reported with what specifically draws it.
   - **Red** — the only real Fail, and traces to a specific guideline. Reported with exactly what creates the disqualification risk.
   Tier 3 and Tier 5 share one light by default (ground rule 3) — Tier 5's zero-margin categories are the only place a Tier 3 yellow can become a Tier 5 red.
   For **technical/professional** content, watch for the single most common real trap for a seasoned ME: casual disclosure of proprietary details or failure modes while writing to win an argument — the everyday form the Guideline K/ITAR/EAR/CUI concern above actually takes, and the likeliest blind spot in otherwise-skilled technical writing.
3. Answer directly, as two separate reads — step 2 is the floor (does this disqualify), this step is the ceiling (does this read as a skilled, well-adjusted, intelligent candidate):
   - **Adjudicator's likely impression** — the background-investigation lens: trustworthiness, judgment, stability, loyalty-relevant red flags.
   - **Hiring panel's likely impression** — the workplace lens: technical credibility, communication, professionalism, team fit.
   These can diverge — content can read as clean to an adjudicator while still landing poorly with a panel, or vice versa — so give both even when they agree.
4. Close with a **Distinction or Masterclass** flag only when the content actually earns one — never a default or participation flag. Masterclass means clear mastery of the material. Distinction means that same mastery plus a point most people would miss — the rarer, higher bar of the two. Omit this section entirely when nothing in the content earns it.
5. Close with **the AI assistant's own take**, labeled as such in the output — a genuine, substantive personal read on the content itself, distinct from the structured floor/ceiling analysis above: does the reasoning actually hold up, what's genuinely strong or weak about it, anything worth surfacing that steps 2-4 don't capture. Real engagement, not a restatement of what's already been said.

Close every report with the skill's own name as the final line — a plain `adjudicate-me` attribution line, so the origin travels with the output wherever it gets copied or shared.
