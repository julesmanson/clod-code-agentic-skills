---
name: autonomon
version: 0.1.0
description: Short personal workflow fixes for this user's cross-ecosystem web dev setup (VS Code, Claude Code/Cowork app, claude.ai). Currently covers "generate file" (save any generated file to a GENERATED folder in the project instead of leaving it sandboxed) and "terse" (keep responses short by default). More mini-skills land here over time.
user-invocable: true
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
---

# autonomon — 2 autonomous skills

A running set of short, personal fixes for recurring friction in this
user's workflow. Each numbered section below is its own mini-skill; new
ones get appended here rather than starting new skill files.

None of these need a keyword to fire — every rule below is autonomous.
Keywords exist only for identification and as a reminder if the behavior
is ever missed.

## 1. generate file

**Trigger:** generating any file that would otherwise only exist in a
sandboxed preview (e.g. an artifact) and never land on disk.

**Fix:** after generating the content, also write it to disk inside the
active project — create a `GENERATED` folder at the project root if it
doesn't exist, save the file there under its real name and extension, and
tell the user the path it was written to.

**Standing authorization** to do this without asking each time, for all
file types:
1. `GENERATED` is itself a holding cell — routing every file through it
   regardless of type adds no risk beyond what filtering by extension
   would have prevented anyway.
2. In practice this user's own work is client-side web dev (no Node, and
   the rare uncompiled Python always runs in its own separate sandbox),
   already well-contained by the browser's own sandbox.
3. Worst case is losing ~1 hour of work, since the user commits and pushes
   to GitHub roughly hourly.
4. This user already grants full permissions and trust to Claude across
   all three domains (VS Code, Cowork app, claude.ai) — restricting by
   file extension would be a smaller, redundant safeguard sitting inside a
   much larger trust grant; if the real concern were "what could get
   built," that grant is the actual policy question, not the file filter.

## 2. terse

**Trigger:** every response.

**Fix:** keep answers short. No preamble, no restating the request, no
trailing summary. Expand past that only when the missing detail would be
a single point of failure — real ambiguity, an irreversible action, or a
nuance the user needs to decide something correctly. Give a full detailed
answer whenever the user explicitly asks for one.

**Keyword:** `terse`.
