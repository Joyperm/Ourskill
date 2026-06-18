---
name: our-skill-uninstall
description: Uninstall all personal skills starting with prefix /our- from Claude Code and Cursor.
---
# our-skill-uninstall

Use this skill when the user explicitly requests to uninstall all personal skills, clean up their environment, or delete the Ourskill library from their system.

## Steps

1. **Locate Installation Paths**
   - Identify the user-level installation paths for both tools:
     - Claude Code: `~/.claude/skills/`
     - Cursor: `~/.cursor/skills/`

2. **Clean Up Skills**
   - Perform the cleanup logic for both directories:
     1. Search for all `SKILL.md` files recursively within both directories.
     2. Read the frontmatter `name:` field of each file.
     3. If the `name:` starts with `our-`, delete the parent folder containing that `SKILL.md` file.
     4. Do NOT touch any skill folder where the `name:` does not start with `our-`.
     5. Do NOT touch the `~/.cursor/skills-cursor/` directory.

3. **Prune Empty Directories**
   - Traverse the target directories and delete any subdirectories that are empty after the cleanup.

4. **Confirm to User**
   - Notify the user that all `our-*` skills have been successfully uninstalled from Claude Code and Cursor.
   - Remind the user to reload Cursor and restart Claude Code to apply the changes.
