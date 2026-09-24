# Clod Code Agentic Skills

<img src="./assets/clod.svg" width="208" height="160" alt="Clod, the orange blockhead cartoon character">

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

The `evaluate-me` skill is model-agnostic. Its Markdown instructions can be
used with any AI model or coding assistant, with only minimal edits needed
to satisfy that assistant's skill format and tool requirements.

## Further reading

- [Use Skills in Claude Code](https://code.claude.com/docs/en/skills) — official docs: discovery, invocation, `~/.claude/skills/` vs `.claude/skills/`
- [Introduction to Agent Skills](https://academy.claude.com/courses/introduction-to-agent-skills) — Claude Academy course: building, configuring, and sharing skills, start to finish

## Repository structure

Each skill lives in its own folder, named after the skill, containing a `SKILL.md` (the complete behavior definition) and a `README.md` (a human-readable guide to the same behavior, with a link back here):

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

<table>
<thead>
<tr>
<th width="20%" align="center">Skill</th>
<th width="80%">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center"><a href="./commit"><code>commit</code></a></td>
<td>Commit and push to the appropriate GitHub repo (adaptable to other git services with minimal edits). Prompts before creating a new repo if one doesn't exist. Supports <code>new repo [name] [visibility] [license] commit</code> to create a repo and make the first commit in one step. Full usage, examples, defaults, and other-git-host notes: <a href="./commit/README.md"><code>commit/README.md</code></a>.</td>
</tr>
<tr>
<td align="center"><a href="./autonomon"><code>autonomon</code></a></td>
<td>
Personal, always-on workflow fixes for this repo's author, originally intended for his own personal use, now open to the public for anyone's convenience.
<ul>
<li><code>generate-file</code> — save generated output to a <code>GENERATED</code> folder instead of leaving it sandboxed</li>
<li><code>terse</code> — keep responses short by default</li>
<li><code>verdict-first</code> — state the verdict before the explanation</li>
<li><code>im-thinking</code> — treat a stated impression as an impression, not a claim to cross-examine</li>
<li><code>ballpark</code> — treat a bare figure as illustrative magnitude, not a precision claim</li>
<li><code>load-bearing</code> — in multi-point critique, lead with corrections that actually change the conclusion</li>
</ul>
Details: <a href="./autonomon/README.md"><code>autonomon/README.md</code></a>.
</td>
</tr>
<tr>
<td align="center"><a href="./thought-experiment"><code>thought-experiment</code></a></td>
<td>Runs a rigorous, evidence-based audit of any target — script, doc, config, whole system — by constructing concrete failure-scenario "thought experiments" and verifying every claim about a dependency's real behavior against a live source rather than memory. Triggered by the phrase "thought experiment." Details: <a href="./thought-experiment/README.md"><code>thought-experiment/README.md</code></a>.</td>
</tr>
<tr>
<td align="center"><a href="./evaluate-me"><code>evaluate-me</code></a></td>
<td>Gives an evidence-based assessment across AI-assistant use, technical judgment, competence, work ethic, reasoning, personality, consistency, and improvement areas. Model-agnostic with minimal adaptation.</td>
</tr>
</tbody>
</table>

More skills will land here as they're written — this list grows with the repo.

## Contributing

This is a personal, evolving collection, but it's public because it might be useful to someone else. Issues and pull requests are welcome — whether that's a fix to an existing skill, a suggestion, or a new one that fits the same format.

## Disclaimer

Use these skills at your own risk. The repository owner provides them “as is,” without warranties, and is not liable for any loss, damage, claim, or consequence arising from their use, to the fullest extent permitted by law. You are responsible for reviewing outputs, commands, files, and results before relying on them.

## License

[MIT](./LICENSE)
