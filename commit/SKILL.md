---
name: commit
description: Commit and push to appropriate GitHub repo (can be used with other git services with minimal edits). If repo does not exist AI will prompt user for validation before creating one. User can also command a new repo with: new repo [scope] [name] commit. This creates new repo with given name and sets scope with public or private (public is default and applies all other defaults) and then commits.
user-invocable: true
allowed-tools:
  - Bash
  - Read
---

# /commit — Commit and Push

**Standing rule, every repo:** when the user says "commit," that means commit
*and* push to the remote. Don't ask separately whether to push — only skip
the push if the user explicitly says "just commit" / "don't push."

## If no repo exists yet

Check with `git rev-parse --is-inside-work-tree` before step 1. If the
current directory isn't a git repository:

- Don't create one silently — ask the user whether to initialize a repo
  here, and if so, what name and visibility (public/private, default
  public) to use.
- Once confirmed, follow the **`new repo` command** flow below, then
  continue with the normal Steps.

## `new repo [scope] [name]` command

Explicit shorthand: `new repo [scope] [name] commit`. `[scope]` is optional
— `public` or `private`, default `public` if omitted. `[name]` is the new
repo's name. Everything else (license, description, team, etc.) stays at
`gh`'s defaults.

1. `git init` if the directory isn't already a repository.
2. `gh repo create [name] --[scope] --source=. --remote=origin` (requires
   the `gh` CLI already authenticated).
3. Continue with the Steps below — staging, drafting the message,
   committing, and pushing. Since this remote has no commits yet, the push
   in step 6 will hit the "no upstream" case and use
   `git push -u origin [current-branch]`.

## Steps

1. Run `git status`, `git diff` (staged + unstaged), and `git log --oneline -5`
   in parallel to see what changed and match this repo's existing message style.
   If `git status` shows a clean working tree (nothing staged or unstaged),
   stop and tell the user there's nothing to commit — never create an empty
   commit.
2. Stage only the files relevant to the request, by name — never `git add -A`
   or `git add .` — unless the user has clearly asked for everything.
3. Check staged content for anything that looks like a secret (`.env`,
   credentials, keys) even if the filename looks innocuous.
4. Draft a concise commit message (1-2 sentences, focused on *why* not *what*).
5. Create the commit. Never `--amend` (unless explicitly asked), never
   `--no-verify` / `--no-gpg-sign`.
6. Push: `git push origin [current-branch]` (or the branch's existing
   upstream if already tracked). If git reports no upstream is set for this
   branch (e.g. a brand-new local branch), use
   `git push -u origin [current-branch]` instead so it gets tracked.
7. If the push is rejected (diverged history) or would need `--force`, stop
   and tell the user — never force-push without explicit approval.