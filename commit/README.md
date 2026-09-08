# `commit`

**Commit and Push** (`v0.5.0-beta`) — [← back to Clod Code Agentic Skills](../README.md)

Commits and pushes to the appropriate GitHub repo, adaptable to other git services with minimal edits. Prompts before creating a new repo if one doesn't exist. See [`SKILL.md`](./SKILL.md) for the actual operative instructions this skill runs on — this file is a human-readable guide to the same behavior.

## Using `commit`

Every way this skill can be invoked, and what happens for each:

| You type | What happens |
| --- | --- |
| `commit` — repo exists | Runs straight through: status/diff/log → stage relevant files by name → check for secrets and errant files → draft a message → commit → push (falling back to `-u origin [branch]` if there's no upstream yet). No confirmation prompt, unless there's nothing to commit (it stops and says so) or the push is rejected (it stops rather than force-pushing). |
| `commit` — repo exists, no remote | Won't let the push fail silently. Stops and asks whether to create a new GitHub repo or attach an existing remote URL. |
| `commit` — no repo here | Won't silently `git init`. Stops and asks whether to create a repo in this folder, and if so, what name and visibility to use. Once you answer, it follows the same flow as `new repo` below. |
| `new repo` (alone) | `[name]` is required and never guessed. Stops and asks for a name. |
| `new repo commit` | Same as above — `commit` is present but `[name]` is still missing, so it stops and asks for one rather than assuming. |
| `new repo [name]` (no `commit`) | Creates the repo — `git init` (if needed) → `gh repo create` — then stops. No commit made; you didn't ask for one. |
| `new repo [name] commit` | Same creation, then runs the normal commit flow on top, pushing with `-u` since the remote has no commits yet. `[visibility]` defaults to `public`, `[license]` defaults to `none`. |
| `new repo [name] [visibility] commit` | Same, with `[visibility]` given explicitly instead of defaulted. `[license]` still defaults to `none`. |
| `new repo [name] [visibility] [license] commit` | Full form — nothing defaulted. `[visibility]` and `[license]` are recognized by keyword wherever they appear; whatever's left is `[name]`. |
| Any value that doesn't resolve cleanly | Stops and asks — an unrecognized `[visibility]`/`[license]`, an existing `origin` remote, more than one leftover token for `[name]` — nothing here is guessed. |

Never runs unprompted, either — see the **Never unprompted** rule at the top of [`SKILL.md`](./SKILL.md). Claude may ask "want me to commit this?" but won't stage, commit, or push without an explicit "commit" call landing first.

Examples:

```
new repo my-project commit
```
Public repo named `my-project`, no license file, created from the current directory, then committed and pushed.

```
new repo my-project private apache-2.0 commit
```
Same, but private and Apache-2.0 licensed.

### Defaults

The **only** values this skill assumes without asking — everything else ambiguous or missing gets a clarifying question instead, per the blanket rule in the skill file:

| Value | Assumed if not given |
| --- | --- |
| `[visibility]` | `public` |
| `[license]` | `none` |
| Remote name | `origin` |
| Branch to push | whichever branch is currently checked out (never switched on your behalf) |

`gh repo create` doesn't set a visibility itself — run it without an explicit flag and it prompts in an interactive terminal, or errors outright when run non-interactively (which is how this skill runs it) — either way, it never silently assumes one. `[visibility]` defaulting to `public` is this skill's own choice when your phrasing leaves it out, the same choice GitHub's own website makes you pick explicitly when creating a repo by hand. `[license]` defaulting to `none` isn't this skill choosing anything — it's just `gh`'s own default carried straight through.

> **Tip:** if you create the GitHub repo yourself via the website first, uncheck "Add a README file" and "Choose a license" unless you actually want GitHub's placeholders — otherwise they'll need reconciling with this skill's own README/LICENSE afterward.

## Using `commit` with other git hosts

Plain "commit" is host-agnostic — it's just `git push`, which works against any remote regardless of provider. The **only** GitHub-specific part is the `new repo` command's repo-creation step, which shells out to the GitHub CLI (`gh repo create`).

| Situation | What to do |
| --- | --- |
| GitLab | See **Adapting to GitLab** below — `glab`'s flags don't map 1:1 onto `gh`'s. |
| No CLI available (Bitbucket, self-hosted/bare server, or `gh` not installed/authenticated) | Create the empty repo manually — via the host's web UI, or out-of-band for a bare server — then run `git remote add origin [url]` yourself. Plain "commit" works normally after that. |
| Existing repo with a non-`origin` remote name | The skill assumes `origin`. Run `git remote -v` first and say which remote to push to if it's named something else. |
| SSH vs. HTTPS remote URL | Doesn't matter — `git push` behaves the same either way once `origin` is set correctly. |

Once a remote named `origin` exists, on any host, "commit" behaves identically. Repo *creation* is the only part tied to GitHub.

### Adapting to GitLab

Swap `gh repo create` for `glab repo create [name] --[visibility] --remoteName=origin` in the skill body, run from inside the already-`git init`'d directory. Three real differences from `gh`, not just a naming swap:

- No `--source` flag — running from the current directory (or omitting `[name]` to use the folder name) is `glab`'s equivalent of `gh`'s `--source=.`.
- The remote-name flag is `--remoteName`, not `--remote`.
- Visibility flags (`--public`/`--private`) match `gh`'s naming, but `glab repo create` has no `--license` flag at all — the license step has no GitLab equivalent. Add a `LICENSE` file yourself if you need one.

---
[← back to Clod Code Agentic Skills](../README.md)
