---
name: our-hello
description: >-
  Sanity-check skill for the Ourskill library. Use when the user types
  /our-hello or asks to verify that the our-* skill pipeline is installed and
  working in Claude Code or Cursor.
---
# our-hello

A minimal skill that proves the `our-` skill pipeline is wired up correctly in
both Claude Code and Cursor.

When invoked, reply with a short confirmation that includes:

1. A greeting: "👋 our-hello is alive."
2. Which tool you are running in (Claude Code or Cursor), if you can tell.
3. The path this skill was loaded from, if determinable
   (e.g. `~/.claude/skills/our-hello` or `~/.cursor/skills/our-hello`).
4. A one-line reminder: edit skills in the central `Ourskill` repo, then re-run
   `scripts/install.ps1` (central machine) or the bootstrap one-liner (other
   machines).

Keep the reply to a few lines. This skill exists only to verify installation.
