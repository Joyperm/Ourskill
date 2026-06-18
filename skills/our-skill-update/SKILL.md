---
name: our-skill-update
description: Check the remote repository for updates to the Ourskill library and synchronize/install updated skills to Claude Code and Cursor.
---
# our-skill-update

Use this skill when the user asks to update their Ourskill library, check for newer versions of skills, or synchronize their local skills with the remote repository.

## Steps

1. **Locate the Remote Repository URL**
   - Inspect the current directory's Git configuration (`git remote get-url origin`).
   - If not found or if running outside the repository, use the central repository URL: `https://github.com/Joyperm/Ourskill.git`.

2. **Fetch the Remote Version**
   - Check the remote repository's `VERSION` file (or `Changelog.md`).
   - If using git, run `git fetch` and compare the local branch to `origin/master` (or the default branch).
   - If running as a standalone folder outside Git, fetch the `VERSION` file directly from the raw Git URL: `https://raw.githubusercontent.com/Joyperm/Ourskill/master/VERSION`.

3. **Compare Versions**
   - Read the local version from the `VERSION` file in the installation directory.
   - If the remote version is the same as the local version, tell the user: "Ourskill is already up-to-date (Version X.Y.Z)."
   - If a newer version is available, proceed to the installation step.

4. **Update/Synchronize Skills**
   - Since the repository is in the gathering phase (v0.0.x), perform a clean install (**Phase A** from the main documentation):
     1. Retrieve the latest skill codebase from the remote repository (e.g., via `git pull` or temporary download).
     2. Identify the installation paths for Claude Code (`~/.claude/skills/`) and Cursor (`~/.cursor/skills/`).
     3. Scan all folders in these paths. Read the frontmatter `name:` in each `SKILL.md`. If it starts with `our-`, delete that folder.
     4. Copy the newly fetched `our-*` folders into both installation paths.
     5. Update the local `VERSION` file to match the remote version.

5. **Prompt Reload**
   - Notify the user of the successful update and ask them to reload Cursor or restart Claude Code.
