---
name: your-mothers-not-here
version: 1.0.2-beta
description: Cleans up Claude-Code-generated backroom files. Two keyworded operations — "backroom" (old session transcripts, sandbox-style scratch, Playwright/screenshot artifacts) and "amnesia" (stale/redundant memory file cleanup + consolidation). Backroom asks which chat logs to keep (default: last two) before deleting any; amnesia removes stale/redundant memory content automatically, then reports the resulting file count/average length and asks whether to merge.
user-invocable: true
allowed-tools:
  - Bash
  - Read
  - Glob
  - Grep
  - Write
  - Edit
---

# Your Mother's Not Here — Claude-Generated Backroom File Cleanup (v1.0.2-beta)

**⚠️ Warning and disclaimer — read this entire file before invoking.** Every action this skill takes is a deletion, or an edit to memory content that can't be recovered once overwritten. The defaults below (keep the last two chat logs, what counts as "stale," when merging is worth it) reflect one person's workflow, not a universal standard. Read the whole file carefully and make any edits your own situation needs — file paths, defaults, what counts as "safe to delete" — before trusting it with anything you can't afford to lose.

**Trigger:** explicit only. Invoking the skill by name (or describing backroom-file cleanup) runs **backroom**. Naming **amnesia** explicitly — alone or alongside backroom, e.g. "your mothers not here do amnesia too" — also runs the memory cleanup. Never runs autonomously just because something looks like clutter; every action here is a deletion.

Two keyworded operations, independently addressable. Each gates its own riskiest action with a question — backroom before touching anything, amnesia before merging files — rather than a single blanket confirmation.

## backroom

Cleans old session transcripts and project-level AI scratch output.

**Always begins by listing available chat logs and asking which to keep, before touching anything.** Default: the last two, if the user doesn't specify otherwise — the default answers the question, it doesn't skip it. This question is never skipped, regardless of how the skill was invoked.

**Covers:**
- **Session transcripts** (`.claude/projects/<project>/*.jsonl`) — which logs survive is set by the user's answer, defaulting to the last two if unspecified, every time.
- **Sandbox-style scratch folders** (`tmp/`, `scratch/`, or similar holding areas) — keep real work product; delete superseded drafts (literally named `temp`/`old`/`draft` and replaced by a current file) only after reading the file's own content to confirm it's actually dead, never by filename alone.
- **Standard backroom artifacts** — `.playwright-mcp/`, ad hoc screenshots, shell snapshots, caches, orphaned session folders, dead locks. Delete on sight, no confirmation needed.
- **A folder literally named `GENERATED/` is never touched, under any circumstance** — real project work product lives there, and deletion rights belong to the user alone, not delegated even with a yes.
- **The `memory/` folder itself is never touched by backroom** — only `amnesia` touches memory content.

**Offering amnesia:** if the user invokes backroom without naming amnesia, it's fine to ask once ("amnesia too?") — but never run it without an explicit yes. If they decline or don't answer, proceed with backroom alone.

## amnesia

Cleans the memory system (`memory/*.md`). **Never runs unprompted** — requires either the keyword "amnesia" named explicitly, or an explicit yes after backroom asked and offered it.

Once triggered, always performs, in this order:

1. **Remove stale content** — verify every factual claim (file paths, function names, "still planned" vs. already-shipped) against the current codebase/filesystem before deleting or editing anything. Never assume a memory is outdated just because it's old; never assume it's current just because it hasn't been flagged. A memory describing a feature that's since shipped (the prototype it was tracking got built, matches production code now) is deleted outright, not just edited — don't carry forward notes about a prototype once the real thing replaced it.
2. **Remove redundancies** — multiple memories covering the same ground get merged into one, keeping every distinct fact and dropping the repetition.
3. **Report the resulting state** — after 1 and 2, report the current file count and their average length (word/line count). This is the number the merge question below depends on, not a courtesy status update.
4. **Ask whether to merge** — only now, armed with that count. Plain yes/no, no default: whether consolidation is still worth it after stale/redundant content is already gone is exactly what this question exists to surface, and it can go either way depending on what step 3 just showed.
5. **Merge, if yes** — consolidate into fewer, type-organized files (this project's existing `memory/` shape — one per category — unless the user specifies otherwise when answering yes).

## Shared process (both operations)

1. **Ask the relevant question before the step it gates, not before everything.** Backroom's "which to keep" gates its one and only action, asked before anything is touched. Amnesia's "merge?" gates only the merge step — stale/redundancy removal run first since they're always safe once amnesia itself was invoked; merge is asked afterward, informed by the resulting count.
2. **Enumerate before touching anything.** List candidates non-destructively first.
3. **Verify by content, not filename or age.** A suspicious name or an old timestamp is a reason to check, not a reason to delete.
4. **Check for live use.** Don't touch a lock file, cache, or transcript an actively running process is currently writing to.
5. **Confident vs. uncertain.** Confident = matches a rule above exactly (standard backroom artifacts, a content-verified dead draft, a confirmed-shipped feature's memory). Uncertain = anything needing a guess about intent or scope — ask, don't guess. Which chat logs to keep and whether to merge memory files are never "confident" — both are asked every time per each operation's own rule above.
6. **Report at moderate detail, two lenses:** **Housekeeping** (can it be pruned, why — regenerable vs. irreplaceable) and **Understanding** (what it is, what's lost if pruned). A handful of labeled bullets, not a narrated essay.
7. **After deleting, report exactly what was removed** (paths, approximate sizes) so there's a clear record to object to if something was misjudged.

## Why this exists

Built from a real cleanup pass: consolidating 40+ small memory files down to 3 type-organized ones (amnesia's shape), clearing superseded component drafts from a `GENERATED/` folder after reading their content rather than trusting their names, and deleting old session transcripts for one project down to a user-specified depth (backroom's shape) — all after first listing contents and confirming scope rather than guessing.
