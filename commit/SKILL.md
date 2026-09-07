---
name: commit
version: 0.6.0-beta
description: Commit and push to appropriate GitHub repo (can be used with other git services with minimal edits). If repo does not exist AI will prompt user for validation before creating one. User can also command a new repo with: new repo [name] [visibility] [license] commit. This creates a new repo with the given name, visibility (public/private, default public), and license (default none, same as `gh repo create` itself), then commits. Any invalid value is confirmed with the user before creating the repo or committing.
user-invocable: true
allowed-tools:
  - Bash
  - Read
---

# /commit — Commit and Push (v0.6.0-beta)

**Never unprompted:** this skill only runs on an explicit call — the user
says "commit," or a recognized trigger like `new repo ... commit`. Noticing
a good moment to commit and asking "want me to commit this?" is fine, even
welcome — but never run any step of this skill, or stage/commit/push
anything, without that explicit call actually landing first.

**Standing rule, every repo:** when the user says "commit," that means commit
*and* push to the remote. Don't ask separately whether to push — only skip
the push if the user explicitly says "just commit" / "don't push."

**Blanket rule, everything in this skill:** if any part of a request is
missing, ambiguous, or could reasonably be read more than one way — which
files to stage, which remote to push to, what a value means, whether the
user wants X or Y — stop and ask for clarification before taking any
action. Never guess just to keep moving. The specific never-guess rules
below (`[name]`, an unrecognized `[visibility]` or `[license]`, an existing
`origin`, etc.) are instances of this same rule, not exceptions to it —
they're called out individually because they're the cases most likely to
come up, not because ambiguity elsewhere is more tolerable.

**On defaults:** `gh repo create` doesn't set a visibility itself — run
without an explicit flag, it prompts interactively in a real terminal, or
errors outright when run non-interactively, which is how this skill runs
it (via Bash). Either way it never silently assumes one — this is also
why creating a repo by hand on github.com makes you actively pick it.
`[visibility]` defaulting to `public` here is this skill choosing a value
on the user's behalf *because their phrasing left it out*. `[license]`
defaulting to `none`, by contrast, isn't this skill choosing anything — it
just carries `gh`'s own default straight through. See **Defaults** at the
bottom for the full list.

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

## `new repo [name] [visibility] [license] commit` command

Full form: `new repo [name] [visibility] [license] commit`. Minimum form:
`new repo [name]` — `[name]` is the only required piece.

- `[name]` — the new repo's name. **Required, never guessed.**
- `[visibility]` — `public` or `private`. Default `public` if omitted.
- `[license]` — one of GitHub's license template keywords (the exact set
  the `api.github.com/licenses` endpoint returns, which is what `gh` itself
  validates against): `agpl-3.0`, `apache-2.0`, `bsd-2-clause`,
  `bsd-3-clause`, `bsl-1.0`, `cc0-1.0`, `epl-2.0`, `gpl-2.0`, `gpl-3.0`,
  `lgpl-2.1`, `mit`, `mpl-2.0`, `unlicense`, or `none` for no license file
  at all. Default `none` if omitted — same as `gh repo create` itself.
- `commit` — trigger word. If present, run the Steps below after creating
  the repo. If omitted, just create the repo and stop.

Everything else (description, team, etc.) stays at `gh`'s defaults.
`[visibility]` and `[license]` are recognized by keyword (public/private,
or a known license keyword) wherever they appear among the tokens;
whatever's left over is `[name]`.

If the current directory already has a `LICENSE` file and `[license]`
would produce a different one, don't overwrite it silently — ask first.

1. If the directory is already a git repository, check `git remote -v`
   first. If a remote named `origin` already exists, don't silently
   overwrite it — tell the user and ask before replacing or renaming it.
   Otherwise, `git init`.
2. `gh repo create [name] --[visibility] --source=. --remote=origin`,
   adding `--license [license]` only if `[license]` isn't `none` (requires
   the `gh` CLI already authenticated). `--[visibility]` is a placeholder
   — substitute the real flag, `--public` or `--private`.
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
4. Draft a concise commit message (1-2 sentences, focused on *why* not
   *what*). First line: a general summary with just enough detail on the
   most important change to be easily told apart from other commits made
   around the same time — never something generic like "update files."
5. Create the commit. Never `--amend` (unless explicitly asked), never
   `--no-verify` / `--no-gpg-sign`.
6. Push: `git push origin [current-branch]` (or the branch's existing
   upstream if already tracked). If git reports no upstream is set for this
   branch (e.g. a brand-new local branch), use
   `git push -u origin [current-branch]` instead so it gets tracked.
7. If the push is rejected (diverged history) or would need `--force`, stop
   and tell the user — never force-push without explicit approval.

## Defaults

Everything this skill will assume without asking, if the user's request
doesn't say otherwise. Nothing outside this list gets silently assumed —
anything else missing or unclear falls under the blanket rule above.

| Value | Assumed if omitted | Never assumed when |
| --- | --- | --- |
| `[visibility]` (`new repo`) | `public` | The given value isn't `public` or `private` — ask instead. |
| `[license]` (`new repo`) | `none` | The given value isn't a recognized license keyword — ask instead. |
| Remote name | `origin` | A different remote is already configured, or more than one exists — ask which to use. |
| Branch to push | whichever branch is currently checked out | — this isn't a default so much as "operate on what's active"; never switch branches on the user's behalf. |
| `[name]` (`new repo`) | *(never defaulted — always required)* | Always. |