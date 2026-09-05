---
name: commit
description: Commit and push to appropriate GitHub repo (can be used with other git services with minimal edits). If repo does not exist AI will prompt user for validation before creating one. User can also command a new repo with: new repo [scope] [name] [license] commit. This creates a new repo with the given name, scope (public/private, default public), and license (default MIT), then commits. Any invalid value is confirmed with the user before creating the repo or committing.
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

This is different from a repo that exists locally but has **no remote at
all** — check `git remote -v` before step 6 if it's ever empty. In that
case, don't just let the push fail silently: ask whether to create a new
GitHub repo (the `new repo` flow) or attach an existing remote URL, then
proceed.

## `new repo [scope] [name] [license] commit` command

Full form: `new repo [scope] [name] [license] commit`. Minimum form:
`new repo [name]` — `[name]` is the only required piece.

- `[scope]` — `public` or `private`. Default `public` if omitted.
- `[name]` — the new repo's name. **Required, never guessed.**
- `[license]` — a license keyword (`mit`, `apache-2.0`, `gpl-3.0`,
  `unlicense`, etc.). Default `mit` if omitted.
- `commit` — trigger word. If present, run the Steps below after creating
  the repo. If omitted, just create the repo and stop.

Everything else (description, team, etc.) stays at `gh`'s defaults.

**Parsing:** tokens between `repo` and `commit` (or the end of the phrase,
if `commit` is omitted) aren't strictly positional — recognize `public`/
`private` as `[scope]` and a known license keyword as `[license]` wherever
they appear, and treat whatever single token is left over as `[name]`.

**Catch-all validation rule:** any value that doesn't cleanly resolve —
zero or more than one leftover token for `[name]`, a `[scope]` that isn't
`public`/`private`, or a `[license]` that isn't a recognized keyword — is
never guessed or silently defaulted. Stop and ask the user to confirm
before creating the repo or making a commit. The only values assumed
without asking are the two stated defaults: `public` for an omitted
`[scope]`, and `mit` for an omitted `[license]`.

If the current directory already has a `LICENSE` file and `[license]`
would produce a different one, don't overwrite it silently — ask first.

1. If the directory is already a git repository, check `git remote -v`
   first. If a remote named `origin` already exists, don't silently
   overwrite it — tell the user and ask before replacing or renaming it.
   Otherwise, `git init`.
2. `gh repo create [name] --[scope] --license [license] --source=.
   --remote=origin` (requires the `gh` CLI already authenticated).
3. If the command included `commit`, continue with the Steps below —
   staging, drafting the message, committing, and pushing. Since this
   remote has no commits yet, the push in step 6 will hit the "no
   upstream" case and use `git push -u origin [current-branch]`.

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