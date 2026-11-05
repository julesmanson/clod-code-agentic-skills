<p align="center">
  <img src="./assets/clod-scolded.svg" width="400" height="440" alt="A 1950s-catalog-style mother stands with hands on hips, looking sternly down at Clod, the blocky orange-headed cartoon character, who sits on the floor playing amid scattered toy blocks and a ball.">
</p>

# Your Mother's Not Here (ver 1.0.5 beta)

# ⚠️ Read carefully before use — every action is a deletion

**Claude-Generated Backroom File Cleanup** — [← back to Clod Code Agentic Skills](../README.md)

Two keyworded operations: **backroom** (old session transcripts, sandbox-style scratch, Playwright/screenshot artifacts) and **amnesia** (stale/redundant memory cleanup + consolidation). The specifics below reflect one person's workflow, not a universal standard. Backroom defaults to keeping the last two chat logs. Amnesia's own calls — what counts as "stale" memory content, whether merging those memory files is worth it — are left as judgment, not given a default. Read [`SKILL.md`](./SKILL.md) in full and edit it to match your own situation before trusting it with anything you can't afford to lose.

## Where this came from

This came out of an actual cleanup pass on a long-running project: 40+ small memory files consolidated into 3 type-organized ones, superseded component drafts cleared from a `GENERATED/` folder after confirming by content (not filename) that they were dead, and old session transcripts deleted down to a user-chosen set. Each step started with a listing and a question before anything irreversible happened — this skill generalizes that rhythm into two named operations.

## What backroom and amnesia do

- **`backroom`** — files. Always lists available chat logs and asks *which to keep* before touching any transcript — never skipped, though it defaults to the last two if you don't specify otherwise. Standard artifacts (Playwright output, caches, shell snapshots) clear without ceremony; sandbox-style drafts (`tmp/`, `scratch/`, or similar) only get deleted when literally named `temp`/`old`/`draft` and superseded by a current file — and even then, only after their content is actually checked to confirm it's dead, not just their filename. A folder literally named `GENERATED/` is never touched at all — deletion rights there belong to the user alone, same standing as `memory/`.
- **`amnesia`** — memory. Never runs unprompted; needs the keyword named explicitly, or an explicit yes after backroom offers it. Removes stale content and redundancies automatically once triggered (both verified against the current codebase, not assumed from age), then reports the resulting file count and average length, then asks a plain yes/no on merging the rest into fewer type-organized files — asked after the safe cleanup, with real numbers, not blind upfront.

## Using it

Invoke by name — "your mother's not here," or either alternative phrasing "your mother isn't here" / "your mother is not here." That alone opens a dialog for specifics on both operations: which chat logs `backroom` should keep (default: last two), and whether to also run `amnesia` (no default — a judgment call). Skip any part of that dialog by giving specifics directly in the call itself — name `amnesia` explicitly (e.g. *"your mothers not here do amnesia too"*), say which logs to keep, or both — and only what's left unanswered gets asked. Expect a non-destructive listing first, content checks on anything ambiguous, a two-lens report (prune? what's lost?) at moderate detail, and a clear accounting of what was actually removed once it acts. Every run closes with one consolidated summary report, then a new line with `your mothers not here`.

## Related skills

- [Commit](../commit) — the same discipline from the other direction: an irreversible action (deletion here, a push there) that only ever runs behind an explicit ask, never on a good moment alone.
- [Thought Experiment](../thought-experiment) — shares the "verify by content or a live source, never by assumption" discipline that governs both backroom's content-before-filename rule and amnesia's stale-content check.
- [Don't Pollute Comments](../dont-pollute-comments) — the same stale-content discipline from a different angle: amnesia's "verify before deleting or editing, never assume stale from age alone" and that skill's "fix only what's gone stale, preserve everything else" are the same instinct applied to memory files versus code comments.
- [Autonomon](../autonomon) — its memory-cap mini-skill flags before a new memory file would exceed a set ceiling; when lowering that ceiling means consolidating below the current file count, that's amnesia's job to actually carry out, not memory-cap's.

## Disclaimer

Use these skills at your own risk. The repository owner provides them "as is," without warranties, and is not liable for any loss, damage, claim, or consequence arising from their use, to the fullest extent permitted by law. You are responsible for reviewing outputs, commands, files, and results before relying on them.

---
[← back to Clod Code Agentic Skills](../README.md)
