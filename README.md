# Ourskill — Personal Skill Library (Claude Code + Cursor)

A central repository to store "our skills" in one place, then distribute them to both **Claude Code** and **Cursor** at the **user level (system-wide, all projects)** — not tied to any team repo.

All skills are called via the prefix **`/our-`**, for example: `/our-hello`.

> **No installation script** — managed entirely through AI agents (Claude Code / Cursor).
> The agent reads the "Instructions for AI agent" section below and handles copying, deleting, and updating paths automatically.

👉 For full details and sources of each skill, see **[SKILLS.md](SKILLS.md)**.

---

## Current Skills — v0.0.2 (36 Skills)

> 👉 For full descriptions and sources of each skill, see **[SKILLS.md](SKILLS.md)**.

**setup — Project Setup**
`/our-add-auth` · `/our-add-docker` · `/our-setup-ci` · `/our-db-design` · `/our-ui-stack` · `/our-secrets`

**fullstack — Development**
`/our-write-tests` · `/our-commit-msg` · `/our-create-pr` · `/our-audit-security` · `/our-update-npm` · `/our-css-to-tailwind` · `/our-api-design` · `/our-error-handling` · `/our-audit-perf` · `/our-e2e-tests` · `/our-sql-optimize`

**engineering — Debugging / Code Review / Comprehension**
`/our-debug` · `/our-postmortem` · `/our-review` · `/our-onboard-codebase` · `/our-test-driven` · `/our-audit-arch`

**self-dev / productivity — Self-improvement / Productivity**
`/our-prompting` · `/our-skill-from-pattern` · `/our-save-context` · `/our-adr` · `/our-mgmt-rewrite` · `/our-stay-on-track`

**planning / motivation / utility**
`/our-grill-me` · `/our-cheer` · `/our-hello` · `/our-skill-update` · `/our-skill-uninstall` · `/our-skill-autoread` · `/our-stack-expert`

---

## Other Skill Sources (For future additions)

Sources surveyed but not yet pulled:

- [spencerpauly/awesome-cursor-skills](https://github.com/spencerpauly/awesome-cursor-skills) — ~70 developer/devops skills (many rely on Cursor's built-in browser, which cannot be used in Claude Code).
- [anthropics/skills](https://github.com/anthropics/skills) — official; document processing (pdf/docx/pptx/xlsx) + creative.
- [jeffallan/claude-skills](https://github.com/jeffallan/claude-skills) — 66 full-stack framework-specific skills (React / NestJS / DevOps Expert).
- [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) · [wshobson/agents](https://github.com/wshobson/agents) — large collection from actual teams.
- [karanb192/awesome-claude-skills](https://github.com/karanb192/awesome-claude-skills) · [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) — curated list (TDD / debug / git / productivity).
- [mattpocock/skills](https://github.com/mattpocock/skills) — very popular "engineering discipline" skills that make the agent **less reckless** rather than smarter. Notable: `/grill-me` (interview before building — we already adapted this as `/our-grill-me`), a shared-language `CONTEXT.md` convention, `/tdd` (red-green-refactor), and `/improve-codebase-architecture` (scan project → report on architecture drift). Good candidate to review for ideas to consolidate into our existing skills.

> ⚠️ When selecting from these sources, be careful with skills that rely on Cursor-specific browsers or hooks, as they will not work in Claude Code.

---

## Installation Paths (User-level)

| Tool | Path |
|------|------|
| Claude Code | `~/.claude/skills/our-<name>/SKILL.md` |
| Cursor | `~/.cursor/skills/our-<name>/SKILL.md` |

- Windows: `~` = `%USERPROFILE%` = `C:\Users\<you>`
- macOS / Linux: `~` = home directory
- Both tools read the same `SKILL.md` format → 1 skill folder can be used by both.

> ⚠️ **Do not touch `~/.cursor/skills-cursor`** — Reserved by Cursor for internal use and managed automatically. The correct path for user-defined skills is `~/.cursor/skills/`.

---

## Naming Conventions (prefix /our-)

Skills are invoked based on the `name:` value in the frontmatter. Therefore, all skills must satisfy:

- Folder name = `our-<slug>`
- In `SKILL.md` → `name: our-<slug>`

→ Invoked as `/our-<slug>` in both Claude and Cursor.

> ⚠️ **Important:** The command `/our-<slug>` is determined by the **`name:`** field in the frontmatter, **not the folder name**. We keep them matching for consistency, but when performing "cleanups of old skills," always check the frontmatter `name:` field. Some machines might have misaligned folder names or nested subfolders, but they would still register as `/our-` commands. Deleting based solely on folder names might miss them and lead to skill name conflicts.

---

## Skill Tiers — Basic vs Advanced (machine-local)

Each machine can hold two kinds of `/our-` skills:

| Tier | Prefix | Owned by | Pushed to central repo? | `/our-skill-update` & `/our-skill-uninstall` |
|------|--------|----------|-------------------------|----------------------------------------------|
| **Basic** | `our-<name>` | the central library | yes — synced to every machine | **managed**: replaced/removed on sync |
| **Advanced** | `our-adv-<name>` | **this machine only** | **no** — never leaves the machine | **protected**: never touched |

**Advanced skills (`our-adv-*`)** are for needs that differ per machine — e.g. a
work machine that wants a stack-specific expert (`our-adv-nextjs`,
`our-adv-django`). They are created locally on that machine, **never pushed**, and
the sweep in `/our-skill-update` and `/our-skill-uninstall` deliberately **skips
anything whose `name:` starts with `our-adv-`**. So upgrading the central library
never deletes or overwrites a machine's own advanced skills.

> ⚠️ Because `our-adv-*` skills live only on the machine that created them, they
> are **not recoverable** from the central repo. Keep your own backup if they
> matter. The protection means an update won't wipe them — it doesn't mean they're
> stored anywhere else.

---

## 📋 Instructions for AI Agent

> This section is written for the **AI agent to read and follow**. The user only needs to command, e.g., "install all skills on this machine" or "update our-foo", and the agent will execute the steps below.

| Scenario | Step to Use | What to Do |
|----------|-------------|------------|
| New machine / First installation (or cluttered with old `/our-` skills) | **A** (One-time) | Recursively find and delete all old `our-*` skills, then clean install the entire set. |
| Regular update / Sync with remote | **`/our-skill-update`** | Run `/our-skill-update` to automatically fetch changes from the remote repository and update local skills. |
| Specific manual update (modified/new/deleted skills) | **B** (Incremental) | Modify **only** the changed skills, leaving other skills untouched. |

> 💡 The recursive cleanup based on `name:` (Phase A, Step 2) is **only used during onboarding/first-time install** to clean up old legacy files. Once onboarding is complete, all skills will reside in standard `our-<name>` folders, so subsequent updates can use **Phase B** directly to overwrite folders, without needing recursive lookup.

### A. First-Time Installation / Onboarding a New Machine — *One-time per machine* (Clean Slate)

Perform these steps for **both** target directories: `~/.claude/skills/` and `~/.cursor/skills/`

1. Create the target directory if it does not exist.
2. **Find "our skills" using `name:` in the frontmatter (not the folder name)** by scanning all `SKILL.md` files recursively (including subfolders). If the `name:` starts with `our-` **but NOT `our-adv-`**, delete the directory containing that file. Afterwards, prune empty folders in the target directory.
   - ⚠️ Check by `name:` only — folders with different names or nested inside subfolders must still be caught.
   - Do not touch skills whose `name:` does not start with `our-`, **never touch `our-adv-*` (machine-local advanced tier, see "Skill Tiers" above)**, and do not touch `~/.cursor/skills-cursor`.
3. Copy all `skills/our-*` folders from this repository to both target directories.
4. Prompt the user to reload Cursor / restart Claude Code.

### B. Specific Update (Incremental — Regular usage after onboarding)

> For machines that have already completed Phase A, all skills reside in standard `our-<name>` folders. No recursive search is needed. Perform operations **only** on the skills listed in the **Update log of [SKILLS.md](SKILLS.md)** (or specified by the user):

- **New Skill** `our-X` → copy `skills/our-X` to both target directories.
- **Modified Skill** `our-X` → delete `~/.claude/skills/our-X` + `~/.cursor/skills/our-X` and copy the new folder over.
- **Deleted Skill** `our-X` → delete `our-X` folder from both target directories.
- Other skills not in the update cycle **must not be touched**.

Then prompt the user to reload their tools.

### Reference: Cleanup Logic Based on `name:` — *Used in Phase A Only* (Example Bash Script)

> This is not a script that must be executed directly — it is an example for the agent to adapt based on the operating system of the target machine. (Phase B does not require this; it simply overwrites/deletes the `our-<name>` directory directly).

```bash
# Delete all skills in $target (recursive) where frontmatter name starts with our-
# EXCEPT the machine-local our-adv-* tier, then prune empty directories
clean_ours() {
  local target="$1"; [ -d "$target" ] || return 0
  find "$target" -type f -iname 'SKILL.md' | while IFS= read -r f; do
    name=$(grep -m1 '^name:' "$f" | sed -E 's/^name:[[:space:]]*//; s/[[:space:]"'"'"']*$//')
    case "$name" in
      our-adv-*) ;;                              # protected: machine-local advanced tier
      our-*) rm -rf "$(dirname "$f")";;
    esac
  done
  find "$target" -mindepth 1 -type d -empty -delete
}
# Apply to both: clean_ours ~/.claude/skills ; clean_ours ~/.cursor/skills
```

---

## Adding New Skills from Other Git Repositories

1. Clone the source repository to a temporary location and choose the skill folder you want.
2. Copy it into `skills/` and **rename the folder to `our-<name>`**.
3. Edit `SKILL.md` → set `name: our-<name>` (keep the rest of the body content unchanged).
4. Add a new row to the catalog in **[SKILLS.md](SKILLS.md)** + record it in the Update log.
5. (To use immediately) Perform Phase **B** to sync that skill onto the machine.

---

## Important Caveats

- Reload Cursor / restart Claude Code after every sync to load new/updated skills.
- Onboarding a machine that has legacy `/our-` skills → using Phase **A** will clean them up automatically.
- Do not touch `~/.cursor/skills-cursor`.

---

## Installing on Other Machines / Offline Setup

To set up Ourskill on a new machine safely without accidental push risks:

1. Clone the repository:
   ```bash
   git clone https://github.com/Joyperm/Ourskill.git
   ```
2. **Remove the git remote** from the cloned folder to turn it into a purely local-only repository (preventing accidental pushes back to the central repository):
   ```bash
   git remote remove origin
   ```
3. Instruct your local agent (Claude Code or Cursor) to install the skills by running **Phase A** (clean slate) from this directory. Once installed, the cloned folder can be deleted.
