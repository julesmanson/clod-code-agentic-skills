# `commit`

**Commit and Push** (`v0.5.0-beta`) — [← back to Clod Code Agentic Skills](../README.md)

When you explicitly ask for a commit, this skill commits and pushes the
appropriate changes to the configured remote. It can be adapted to other Git
services with minimal edits. If you ask to create a repository that does not
exist, you are prompted for the missing decisions first. See
[`SKILL.md`](./SKILL.md) for the complete behavior definition.

## What to expect

Every way this skill can be invoked, and what happens for each:

| You type | What happens |
| --- | --- |
| `commit` — repo exists | Reviews the repository, stages only relevant files, checks for secrets and stray files, creates a concise commit, and pushes it. If there is no upstream, the branch is set up with `-u`. An empty repository state or rejected push is reported instead of being forced through. |
| `commit` — repo exists, no remote | You are asked whether to create a new GitHub repository or attach an existing remote. |
| `commit` — no repo here | You are asked whether to initialize this folder, and for the repository name and visibility. |
| `new repo` or `new repo commit` | You are asked for the required repository name rather than having one guessed. |
| `new repo [name]` | The repository is created, but no commit is made because you did not include `commit`. |
| `new repo [name] commit` | The repository is created and the normal commit-and-push process follows. |
| `new repo [name] [visibility] [license] commit` | The repository is created with the specified options, then committed and pushed. |
| An ambiguous or unrecognized value | You are asked to clarify it rather than having the choice guessed. |

Nothing is staged, committed, or pushed merely because a good moment is
noticed. You must explicitly say `commit` before those actions occur.

## Asymmetric folder structures

The formal `commit` command does not have built-in `from`/`to` path-mapping
syntax. However, an AI assistant can still be expected to interpret a clear
user command with a trailing `from` source and `to` destination instruction.
If a skill lives outside the repository, such as
`skills-workspace/new-skill/`, and you want it published at the repository
root as `new-skill/`, give an explicit instruction such as:

```text
Commit from skills-workspace/new-skill to the repository root as new-skill.
```

With that additional instruction, the skill can copy the source into the
requested repository destination, verify the destination, and then run the
normal commit-and-push workflow. The source remains outside the repository;
the copied destination is what gets staged. An existing destination should
be identified before it is overwritten.

### The pass before action

For an asymmetric publish, you can request a **pass** before anything is
copied or staged. A pass is a deliberate validation pause that confirms the
source, destination, overwrite risk, and files that would be staged. It is a
checkpoint for reviewing the plan before the commit-and-push work begins.

For example, a request might be phrased like this:

```text
Pass first: interpret this as copying from
skills-workspace/new-skill to the repository root as new-skill.
Show me the source, destination, overwrite risk, and proposed staged files.
Do not copy, stage, commit, or push until I approve the pass.
```

This is an example of a user instruction, not a hardcoded `commit` command
or a new syntax built into the skill. The exact wording can vary as long as
the requested validation pause and its boundaries are clear.

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

The following are the only values supplied automatically when you leave them
out. Ambiguous or missing values outside this list prompt a question:

| Value | Assumed if not given |
| --- | --- |
| `[visibility]` | `public` |
| `[license]` | `none` |
| Remote name | `origin` |
| Branch to push | whichever branch is currently checked out (never switched on your behalf) |

When creating a repository, visibility defaults to `public` and license to
`none`. The remote defaults to `origin`, and the currently checked-out branch
is used without switching branches for you.

> **Tip:** if you create the GitHub repo yourself via the website first, uncheck "Add a README file" and "Choose a license" unless you actually want GitHub's placeholders — otherwise they'll need reconciling with this skill's own README/LICENSE afterward.

## Using `commit` with other git hosts

The ordinary `commit` workflow works with any Git remote. Only repository
creation is GitHub-specific, because the `new repo` command uses GitHub CLI.

| Situation | What to do |
| --- | --- |
| GitLab | Use the GitLab adaptation below; its CLI flags are not identical to GitHub's. |
| No CLI available | Create the empty repository through the host's web interface or other supported method, then add its remote URL. The ordinary commit workflow still works. |
| A remote is not named `origin` | Tell the skill which remote to use. |
| SSH versus HTTPS | Either works once the remote is configured correctly. |

Once the remote is configured, `commit` behaves the same across hosts.
Repository creation is the only GitHub-specific part.

### Adapting to GitLab

Swap `gh repo create` for `glab repo create [name] --[visibility] --remoteName=origin` in the skill body, run from inside the already-`git init`'d directory. Three real differences from `gh`, not just a naming swap:

- No `--source` flag — running from the current directory (or omitting `[name]` to use the folder name) is `glab`'s equivalent of `gh`'s `--source=.`.
- The remote-name flag is `--remoteName`, not `--remote`.
- Visibility flags (`--public`/`--private`) match `gh`'s naming, but `glab repo create` has no `--license` flag at all — the license step has no GitLab equivalent. Add a `LICENSE` file yourself if you need one.

---
[← back to Clod Code Agentic Skills](../README.md)
