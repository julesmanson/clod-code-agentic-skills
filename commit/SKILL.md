---
name: commit
version: 0.7.0-beta
description: Commits and pushes to the remote using plain git commands, closing with a Failed/Commit/Commit-and-push verdict.
user-invocable: true
allowed-tools:
  - Bash
  - Read
---

# Commit ver 0.7.0 beta — Commit and Push

**Never unprompted:** this skill only runs on an explicit call — the user says "commit." Noticing a good moment to commit and asking "want me to commit this?" is fine, even welcome — but never run any step of this skill, or stage/commit/push anything, without that explicit call actually landing first.

**Standing rule, every repo:** when the user says "commit," that means commit *and* push to the remote. Don't ask separately whether to push — only skip the push if the user explicitly says "just commit" / "don't push."

**Blanket rule, everything in this skill:** if any part of a request is missing, ambiguous, or could reasonably be read more than one way — which files to stage, which remote to push to, whether the user wants X or Y — stop and ask for clarification before taking any action. Never guess just to keep moving.

## If no repo or remote exists

No git repository here: cannot be executed — stop and tell the user, this skill doesn't create one.

A repo exists but has **no remote at all** — check `git remote -v` before step 6 if it's ever empty. Ask the user for an existing remote URL to attach, then proceed.

## Steps

1. Run `git status`, `git diff` (staged + unstaged), and `git log --oneline -5` in parallel to see what changed and match this repo's existing message style. If `git status` shows a clean working tree (nothing staged or unstaged), stop and tell the user there's nothing to commit — never create an empty commit.
2. Stage only the files relevant to the request, by name — never `git add -A` or `git add .` — unless the user has clearly asked for everything.
3. Check staged content for anything that looks like a secret (`.env`, credentials, keys) even if the filename looks innocuous, and for anything else that doesn't belong — scratch notes, stray editor or workspace files, build artifacts, etc. If anything turns up, stop and ask before continuing rather than committing it or silently dropping it.
4. Draft a concise commit message (1-2 sentences, focused on *why* not *what*). First line: a general summary with just enough detail on the most important change to be easily told apart from other commits made around the same time — never something generic like "update files."
5. Create the commit. Never `--amend` (unless explicitly asked), never `--no-verify` / `--no-gpg-sign`.
6. Push: `git push origin [current-branch]` (or the branch's existing upstream if already tracked). If git reports no upstream is set for this branch (e.g. a brand-new local branch), use `git push -u origin [current-branch]` instead so it gets tracked.
7. If the push is rejected (diverged history) or would need `--force`, stop and tell the user — never force-push without explicit approval.
8. Report a closing verdict — exactly one of: Failed (state the reason), Commit (committed, not pushed), or Commit and push to [repo name] (both succeeded, naming the actual remote).

## Defaults

Everything this skill will assume without asking, if the user's request doesn't say otherwise. Nothing outside this list gets silently assumed — anything else missing or unclear falls under the blanket rule above.

| Value | Assumed if omitted | Never assumed when |
| --- | --- | --- |
| Remote name | `origin` | A different remote is already configured, or more than one exists — ask which to use. |
| Branch to push | whichever branch is currently checked out | — this isn't a default so much as "operate on what's active"; never switch branches on the user's behalf. |
