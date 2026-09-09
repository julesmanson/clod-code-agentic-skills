# `autonomon`

**2 autonomous skills** (`v0.5.0-beta`) — [← back to Clod Code Agentic Skills](../README.md)

Personal, always-on workflow fixes for this repo's author, originally
intended for personal use and now open to anyone who finds them useful. You
do not need to type a keyword to activate either behavior; the rules operate
automatically. The keywords are names for the behaviors and reminders in
case one is missed. See [`SKILL.md`](./SKILL.md) for the complete definition.

## 1. `generate file`

When you ask for a file that might otherwise appear only in a sandboxed
preview, expect it to be written to a `GENERATED` folder at the project root.
If the folder does not exist, it is created. The file keeps its real name
and extension, and you are given the path where it was written.

This applies to any file type and does not require a separate confirmation.
The `GENERATED` folder is a holding cell, so generated work stays separate
from the rest of the project while remaining accessible in the workspace.
The original rationale and personal-use threat model are documented in
[`SKILL.md`](./SKILL.md).

## 2. `terse`

Expect short answers by default: no unnecessary preamble, repetition, or
trailing summary. More detail is appropriate when leaving it out could cause
a real failure, when a decision is irreversible, or when you ask for a full
explanation.

---
[← back to Clod Code Agentic Skills](../README.md)
