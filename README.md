# Clod Code Agentic Skills

A series of agentic developer skills for Claude Code, adaptable to other AI coding assistants with minimal edits.

## Contents

- [What is a skill?](#what-is-a-skill)
- [Repository structure](#repository-structure)
- [Installing a skill](#installing-a-skill)
- [Skills](#skills)
- [Using `commit`](#using-commit)
- [Using `commit` with other git hosts](#using-commit-with-other-git-hosts)
- [Contributing](#contributing)
- [License](#license)

## What is a skill?

A skill is a single `SKILL.md` file: YAML frontmatter followed by a plain-Markdown body of instructions.

```yaml
---
name: skill-name
description: What it does and when to use it.
user-invocable: true
allowed-tools:
  - Bash
---
```

The frontmatter fields (`user-invocable`, `allowed-tools`) are Claude Code-specific — they control how the skill is triggered and what it's permitted to run. The Markdown body underneath is plain prose describing the steps to follow, which is why these skills are portable: any assistant can read and follow the instructions even if it has no concept of the frontmatter.

## Repository structure

Each skill lives in its own folder, named after the skill, containing a single `SKILL.md`:

```
skill-name/
  SKILL.md
```

## Installing a skill

**Claude Code — personal (all projects on this machine)**
Copy the skill's folder into your personal skills directory:

```sh
cp -r commit ~/.claude/skills/commit
```

On Windows, that's `%USERPROFILE%\.claude\skills\commit\`. Claude Code picks it up automatically from there — invoke it explicitly (e.g. `/commit`) or just describe the task; Claude will use it when the description matches.

**Claude Code — project-level (shared via a repo, including cloud sessions)**
Copy the folder into that project's own `.claude/skills/` directory and commit it. Anyone working in that repo — including cloud/Cowork sessions — gets the skill automatically, with no local setup required.

**Other AI coding assistants**
Copy the Markdown body (below the frontmatter) into your assistant's system prompt or custom-instructions field. Treat `user-invocable` and `allowed-tools` as documentation rather than something your tool will enforce, unless you wire up the equivalent yourself.

## Skills

| Skill | Version | Description |
| --- | --- | --- |
| [`commit`](./commit) | `0.5.0-beta` | Commit and push to the appropriate GitHub repo (adaptable to other git services with minimal edits). Prompts before creating a new repo if one doesn't exist. Supports `new repo [scope] [name] [license] commit` to create a repo and make the first commit in one step. |

More skills will land here as they're written — this list grows with the repo.

## Using `commit`

Every way this skill can be invoked, and what happens for each:

| You type | What happens |
| --- | --- |
| `commit` — repo exists | Runs straight through: status/diff/log → stage relevant files by name → check for secrets → draft a message → commit → push (falling back to `-u origin [branch]` if there's no upstream yet). No confirmation prompt, unless there's nothing to commit (it stops and says so) or the push is rejected (it stops rather than force-pushing). |
| `commit` — no repo here | Won't silently `git init`. Stops and asks whether to create a repo in this folder, and if so, what name and visibility to use. Once you answer, it follows the same flow as `new repo [scope] [name] commit` below, using your answers. |
| `new repo` (alone) | `[name]` is required and never guessed. Stops and asks for a name. |
| `new repo commit` | Same as above — `commit` is present but `[name]` is still missing, so it stops and asks for one rather than assuming. |
| `new repo [name] commit` | `[scope]` is optional and defaults to `public` when omitted. Runs `git init` (if needed) → `gh repo create [name] --public --source=. --remote=origin` → then the normal commit flow, pushing with `-u` since the remote has no commits yet. |
| `new repo [scope] [name] commit` | Same as above, but `--[scope]` is passed explicitly (`public` or `private`) instead of defaulting. Everything else (description, license, team, etc.) stays at `gh`'s defaults. |

Examples:

```
new repo my-project commit
```
Public repo named `my-project`, created from the current directory, then committed and pushed.

```
new repo private my-project commit
```
Same, but private.

## Using `commit` with other git hosts

Plain "commit" is host-agnostic — it's just `git push`, which works against any remote regardless of provider. The **only** GitHub-specific part is the `new repo` command's repo-creation step, which shells out to the GitHub CLI (`gh repo create`).

| Situation | What to do |
| --- | --- |
| GitLab | Swap `gh repo create` for `glab repo create [name] --[visibility] --source=. --remote=origin` in the skill body — GitLab's CLI (`glab`) mirrors `gh`'s flags closely. |
| Bitbucket, or another host without a solid CLI | Create the empty repo manually via the provider's web UI, then run `git remote add origin [url]` yourself. Plain "commit" works normally after that. |
| `gh` not installed or not authenticated | Same fallback: create the repo manually on github.com, `git remote add origin [url]`, then "commit." |
| Self-hosted / bare git server | Same fallback — there's no CLI to assume, so create the remote out-of-band and point `origin` at it. |
| Existing repo with a non-`origin` remote name | The skill assumes `origin`. Run `git remote -v` first and say which remote to push to if it's named something else. |
| SSH vs. HTTPS remote URL | Doesn't matter — `git push` behaves the same either way once `origin` is set correctly. |

Once a remote named `origin` exists, on any host, "commit" behaves identically. Repo *creation* is the only part tied to GitHub.

## Contributing

This is a personal, evolving collection, but it's public because it might be useful to someone else. Issues and pull requests are welcome — whether that's a fix to an existing skill, a suggestion, or a new one that fits the same format.

## License

[MIT](./LICENSE)
