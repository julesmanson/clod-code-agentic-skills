---
name: your-mothers-not-here
version: 0.1.0-beta
description: Cleans up Claude-Code-generated backroom files. Two keyworded operations — "backroom" (old session transcripts, GENERATED/-style scratch, Playwright/screenshot artifacts) and "amnesia" (stale/redundant memory file cleanup + consolidation). Backroom always asks how deep to go before touching transcripts; amnesia never runs unprompted.
user-invocable: true
allowed-tools:
  - Bash
  - Read
  - Glob
  - Grep
  - Write
  - Edit
---

# your-mothers-not-here — Claude-Generated Backroom File Cleanup (v0.1.0-beta)

**Trigger:** explicit only. Invoking the skill by name (or describing backroom-file cleanup) runs **backroom**. Naming **amnesia** explicitly — alone or alongside backroom, e.g. "your mothers not here do amnesia too" — also runs the memory cleanup. Never runs autonomously just because something looks like clutter; every action here is a deletion.

Two keyworded operations, independently addressable:

## backroom

Cleans old session transcripts and project-level AI scratch output.

**Always begins by asking how deep, before touching anything.** Never assume a depth, even "keep only the current session" — ask ("how deep?" / "how many to keep?") and get a concrete answer (e.g. "keep last 2 chats") before deleting any transcript. This question is never skipped, regardless of how the skill was invoked.

**Covers:**
- **Session transcripts** (`.claude/projects/<project>/*.jsonl`) — retained count set by the user's answer to "how deep," every time.
- **`GENERATED/`-style folders** — keep real work product; delete superseded drafts (literally named `temp`/`old`/`draft` and replaced by a current file) only after reading the file's own content to confirm it's actually dead, never by filename alone.
- **Standard backroom artifacts** — `.playwright-mcp/`, ad hoc screenshots, shell snapshots, caches, orphaned session folders, dead locks. Delete on sight, no confirmation needed.
- **The `memory/` folder itself is never touched by backroom** — only `amnesia` touches memory content.

**Offering amnesia:** if the user invokes backroom without naming amnesia, it's fine to ask once ("amnesia too?") — but never run it without an explicit yes. If they decline or don't answer, proceed with backroom alone.

## amnesia

Cleans the memory system (`memory/*.md`). **Never runs unprompted** — requires either the keyword "amnesia" named explicitly, or an explicit yes after backroom asked and offered it. Always performs, in this order:

1. **Remove stale content** — verify every factual claim (file paths, function names, "still planned" vs. already-shipped) against the current codebase/filesystem before deleting or editing anything. Never assume a memory is outdated just because it's old; never assume it's current just because it hasn't been flagged. A memory describing a feature that's since shipped (the prototype it was tracking got built, matches production code now) is deleted outright, not just edited — don't carry forward notes about a prototype once the real thing replaced it.
2. **Remove redundancies** — multiple memories covering the same ground get merged into one, keeping every distinct fact and dropping the repetition.
3. **Merge files** — consolidate many small memory files into fewer, type-organized ones (e.g. one per category: user/feedback/project) once the count is unwieldy. This changes file structure, not just content — fine to do as a matter of course, since it's part of amnesia's standing job, not an extra step to ask about separately.

## Shared process (both operations)

1. **Enumerate before touching anything.** List candidates non-destructively first.
2. **Verify by content, not filename or age.** A suspicious name or an old timestamp is a reason to check, not a reason to delete.
3. **Check for live use.** Don't touch a lock file, cache, or transcript an actively running process is currently writing to.
4. **Confident vs. uncertain.** Confident = matches a rule above exactly (standard backroom artifacts, a content-verified dead draft, a confirmed-shipped feature's memory). Uncertain = anything needing a guess about intent or scope — ask, don't guess. Session-transcript depth is never "confident" — it's asked every time per backroom's own rule above.
5. **Report at moderate detail, two lenses:** **Housekeeping** (can it be pruned, why — regenerable vs. irreplaceable) and **Understanding** (what it is, what's lost if pruned). A handful of labeled bullets, not a narrated essay.
6. **After deleting, report exactly what was removed** (paths, approximate sizes) so there's a clear record to object to if something was misjudged.

## Why this exists

Built from a real cleanup pass: consolidating 40+ small memory files down to 3 type-organized ones (amnesia's shape), clearing superseded component drafts from a `GENERATED/` folder after reading their content rather than trusting their names, and deleting old session transcripts for one project down to a user-specified depth (backroom's shape) — all after first listing contents and confirming scope rather than guessing.
