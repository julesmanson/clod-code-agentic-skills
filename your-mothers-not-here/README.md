# ⚠️ UNTESTED — NOT READY FOR PUBLIC CONSUMPTION

# `your-mothers-not-here`

**Claude-Generated Backroom File Cleanup** (`v0.1.0-beta`) — [← back to Clod Code Agentic Skills](../README.md)

Two keyworded operations: **backroom** (old session transcripts, `GENERATED/`-style scratch, Playwright/screenshot artifacts) and **amnesia** (stale/redundant memory cleanup + consolidation). See [`SKILL.md`](./SKILL.md) for the complete behavior definition.

## Where this came from

This came out of an actual cleanup pass on a long-running project: 40+ small memory files consolidated into 3 type-organized ones, superseded component drafts cleared from a `GENERATED/` folder after confirming by content (not filename) that they were dead, and old session transcripts deleted down to a user-chosen depth. Each step started with a listing and a question before anything irreversible happened — this skill generalizes that rhythm into two named operations.

## backroom vs. amnesia

- **`backroom`** — files. Always opens by asking *how deep* (how many old session transcripts to keep) before touching any transcript — that question is never skipped or assumed, even toward "keep only the current one." Standard artifacts (Playwright output, caches, shell snapshots) clear without ceremony; `GENERATED/`-style drafts only get deleted after their content is actually checked, not just their filename.
- **`amnesia`** — memory. Never runs unprompted; needs the keyword named explicitly, or an explicit yes after backroom offers it. Always does three things, in order: removes stale content (verified against the current codebase, not assumed from age), removes redundancies (merges overlapping memories, keeping every distinct fact), and merges many small files into fewer type-organized ones once the count gets unwieldy.

Run both in one call — e.g. *"your mothers not here do amnesia too"* — or either alone.

## Using it

Invoke by name for `backroom`; name `amnesia` explicitly to include memory cleanup, or say yes when `backroom` offers it. Expect a non-destructive listing first, the depth question before any transcript is touched, content checks on anything ambiguous, a two-lens report (prune? what's lost?) at moderate detail, and a clear accounting of what was actually removed once it acts.

## Disclaimer

Use these skills at your own risk. The repository owner provides them “as is,” without warranties, and is not liable for any loss, damage, claim, or consequence arising from their use, to the fullest extent permitted by law. You are responsible for reviewing outputs, commands, files, and results before relying on them.

---
[← back to Clod Code Agentic Skills](../README.md)
