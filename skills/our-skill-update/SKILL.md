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
   - Perform the update using a temporary directory to avoid leaving duplicate git repositories:
     1. Create a temporary folder on the local machine.
     2. Clone the remote repository into it (e.g., `git clone --depth 1 https://github.com/Joyperm/Ourskill.git temp_ourskill`).
     3. Identify the user installation paths: Claude Code (`~/.claude/skills/`) and Cursor (`~/.cursor/skills/`).
     4. Delete all existing folders in those target paths whose `SKILL.md` frontmatter `name:` starts with `our-` **except** any whose `name:` starts with `our-adv-`.
        - ⚠️ **Never touch `our-adv-*` skills.** They are the machine-local "advanced" tier — created on this specific machine (e.g. stack experts), never pushed to the central repo, and **not recoverable** from it. The sweep here only manages the central/basic library; `our-adv-*` belongs to this machine and must survive every update.
     5. Copy the new `our-*` folders from the cloned `skills/` directory into both installation paths.
     6. Copy/write the remote `VERSION` file to the installation directories to update the local version.
     7. **Clean up**: Delete the temporary folder completely.

5. **Prompt Reload**
   - Notify the user of the successful update and ask them to reload Cursor or restart Claude Code.
