# Clod Code Agentic Skills

A series of agentic developer skills for Claude Code, adaptable to other AI coding assistants with minimal edits.

## Contents

- [What is a skill?](#what-is-a-skill)
- [Further reading](#further-reading)
- [Repository structure](#repository-structure)
- [Installing a skill](#installing-a-skill)
- [Skills](#skills)
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

## Further reading

- [Use Skills in Claude Code](https://code.claude.com/docs/en/skills) — official docs: discovery, invocation, `~/.claude/skills/` vs `.claude/skills/`
- [Introduction to Agent Skills](https://academy.claude.com/courses/introduction-to-agent-skills) — Claude Academy course: building, configuring, and sharing skills, start to finish

## Repository structure

Each skill lives in its own folder, named after the skill, containing a `SKILL.md` (the operative instructions) and a `README.md` (a human-readable guide to the same behavior, with a link back here):

```
skill-name/
  SKILL.md
  README.md
```

## Installing a skill

**Claude Code — personal (all projects on this machine)**
Copy the skill's folder into your personal skills directory:

```sh
cp -r commit ~/.claude/skills/commit
```

That `cp` command needs a Unix-style shell (Git Bash, WSL, macOS/Linux Terminal). In native Windows PowerShell, use:

```powershell
Copy-Item -Recurse commit "$env:USERPROFILE\.claude\skills\commit"
```

Either way, the destination is `%USERPROFILE%\.claude\skills\commit\` on Windows. Claude Code picks it up automatically from there — invoke it explicitly (e.g. `/commit`) or just describe the task; Claude will use it when the description matches.

**Claude Code — project-level (shared via a repo, including cloud sessions)**
Copy the folder into that project's own `.claude/skills/` directory and commit it. Anyone working in that repo — including cloud/Cowork sessions — gets the skill automatically, with no local setup required.

**Other AI coding assistants**
Copy the Markdown body (below the frontmatter) into your assistant's system prompt or custom-instructions field. Treat `user-invocable` and `allowed-tools` as documentation rather than something your tool will enforce, unless you wire up the equivalent yourself.

## Skills

| Skill | Version | Description |
| --- | --- | --- |
| [`commit`](./commit) | `0.6.0-beta` | Commit and push to the appropriate GitHub repo (adaptable to other git services with minimal edits). Prompts before creating a new repo if one doesn't exist. Supports `new repo [name] [visibility] [license] commit` to create a repo and make the first commit in one step. Full usage, examples, defaults, and other-git-host notes: [`commit/README.md`](./commit/README.md). |
| [`autonomon`](./autonomon) | `0.1.0` | Personal, always-on workflow fixes for this repo's author, not intended for general reuse. Currently: `generate file` (save generated output to a `GENERATED` folder instead of leaving it sandboxed) and `terse` (keep responses short by default). Details: [`autonomon/README.md`](./autonomon/README.md). |

More skills will land here as they're written — this list grows with the repo.

## Contributing

This is a personal, evolving collection, but it's public because it might be useful to someone else. Issues and pull requests are welcome — whether that's a fix to an existing skill, a suggestion, or a new one that fits the same format.

## License

[MIT](./LICENSE)
