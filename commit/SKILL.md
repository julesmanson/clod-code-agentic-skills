---
name: commit
version: 0.5.0-beta
description: Commit and push to appropriate GitHub repo (can be used with other git services with minimal edits). If repo does not exist AI will prompt user for validation before creating one. User can also command a new repo with: new repo [visibility] [name] [license] commit. This creates a new repo with the given name, visibility (public/private, default public), and license (default MIT), then commits. Any invalid value is confirmed with the user before creating the repo or committing.
user-invocable: true
allowed-tools:
  - Bash
  - Read
---

# /commit — Commit and Push (v0.5.0-beta)

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

**On defaults:** `gh repo create` doesn't default anything itself — run
without an explicit visibility flag, it either prompts interactively or
errors outright, and licensing works the same way (this is why creating a
repo by hand on github.com makes you actively pick both). Any default
mentioned in this file is this skill choosing a value on the user's behalf
*because their phrasing left it out* — not something GitHub or `gh` assumes
on its own. See **Defaults** at the bottom for the full list.

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

## `new repo [visibility] [name] [license] commit` command

Full form: `new repo [visibility] [name] [license] commit`. Minimum form:
`new repo [name]` — `[name]` is the only required piece.

- `[visibility]` — `public` or `private`. Default `public` if omitted.
- `[name]` — the new repo's name. **Required, never guessed.**
- `[license]` — one of GitHub's license template keywords (the same list
  shown in the "Choose a license" dropdown when creating a repo by hand):
  `mit`, `apache-2.0`, `gpl-3.0`, `agpl-3.0`, `lgpl-3.0`, `mpl-2.0`,
  `bsd-2-clause`, `bsd-3-clause`, `unlicense`, `cc0-1.0`, `epl-2.0`, `isc`,
  or `none` for no license file at all. Default `mit` if omitted.
- `commit` — trigger word. If present, run the Steps below after creating
  the repo. If omitted, just create the repo and stop.

Everything else (description, team, etc.) stays at `gh`'s defaults.

**Parsing:** it's the keywords that drive execution, not word position.
Recognize `public`/`private` as `[visibility]` and a known license keyword as
`[license]` wherever they appear in the phrase, and treat whatever single
token is left over as `[name]`. That means `new repo mit my-project public
commit` is just as valid as the canonical order — but write it in the
documented order (`[visibility] [name] [license] commit`) as a matter of
readability best practice, not because the parser requires it.

**Catch-all validation rule:** any value that doesn't cleanly resolve —
zero or more than one leftover token for `[name]`, a `[visibility]` that isn't
`public`/`private`, or a `[license]` that isn't a recognized keyword — is
never guessed or silently defaulted. Stop and ask the user to confirm
before creating the repo or making a commit. The only values assumed
without asking are the two stated defaults: `public` for an omitted
`[visibility]`, and `mit` for an omitted `[license]`.

If the current directory already has a `LICENSE` file and `[license]`
would produce a different one, don't overwrite it silently — ask first.

1. If the directory is already a git repository, check `git remote -v`
   first. If a remote named `origin` already exists, don't silently
   overwrite it — tell the user and ask before replacing or renaming it.
   Otherwise, `git init`.
2. `gh repo create [name] --[visibility] --license [license] --source=.
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

## Defaults

Everything this skill will assume without asking, if the user's request
doesn't say otherwise. Nothing outside this list gets silently assumed —
anything else missing or unclear falls under the blanket rule above.

| Value | Assumed if omitted | Never assumed when |
| --- | --- | --- |
| `[visibility]` (`new repo`) | `public` | The given value isn't `public` or `private` — ask instead. |
| `[license]` (`new repo`) | `mit` | The given value isn't a recognized license keyword — ask instead. |
| Remote name | `origin` | A different remote is already configured, or more than one exists — ask which to use. |
| Branch to push | whichever branch is currently checked out | — this isn't a default so much as "operate on what's active"; never switch branches on the user's behalf. |
| `[name]` (`new repo`) | *(never defaulted — always required)* | Always. |