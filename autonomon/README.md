# `autonomon`

**2 autonomous skills** (`v0.5.0-beta`) — [← back to Clod Code Agentic Skills](../README.md)

Personal, always-on workflow fixes for this repo's author, originally intended for his own personal use, now open to the public for anyone's convenience. None of these need a keyword to fire; every rule is autonomous. Keywords exist only for identification, and as a reminder if the behavior is ever missed. See [`SKILL.md`](./SKILL.md) for the actual operative instructions.

## 1. `generate file`

When generating any file that would otherwise only exist in a sandboxed preview (e.g. an artifact) and never land on disk, also write it to disk: create a `GENERATED` folder at the project root if it doesn't exist, save the file there under its real name and extension, and report the path.

This runs without asking first, for any file type — not just client-side web files. The reasoning (full version in `SKILL.md`): `GENERATED` is itself a holding cell, so routing every file type through it adds no real risk; the author's actual work is client-side web dev with no compile step; worst case is losing about an hour of work given roughly-hourly git commits; and the author already grants full permissions across their whole Claude ecosystem, so a file-extension filter would be a smaller, redundant safeguard sitting inside a much bigger trust grant.

## 2. `terse`

Keep answers short by default — no preamble, no restating the request, no trailing summary. Expand only when the missing detail would be a real point of failure (genuine ambiguity, an irreversible action, a nuance needed to decide something correctly), or when explicitly asked for a detailed answer.

---
[← back to Clod Code Agentic Skills](../README.md)
