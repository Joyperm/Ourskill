---
name: our-skill-doctor
description: Health-check the installed Ourskill library and (when run inside the Ourskill repo) verify the catalog stays consistent with the actual skill folders. Use to diagnose a broken or stale install, confirm an update applied cleanly, or — on the dev machine — catch catalog/version drift before a release. Trigger on /our-skill-doctor, "check my skills", "are my skills healthy", "did the update work", "verify the catalog".
user-invocable: true
---
# our-skill-doctor — verify the skill library is healthy

Two checks in one. **Install health** runs anywhere. **Catalog consistency** runs
only when invoked inside the Ourskill repo (dev machine).

## A. Install health (always)

Scan the user-level skill dirs — Claude Code `~/.claude/skills/` and Cursor
`~/.cursor/skills/` — and report:

1. **Frontmatter integrity** — every `our-*/SKILL.md` has a non-empty `name:` and
   `description:`. Flag any missing or malformed frontmatter.
2. **Folder ↔ name match** — the folder name equals the frontmatter `name:`. A
   mismatch is the classic gotcha (the `/command` comes from `name:`, not the
   folder) and can cause silent duplicate-command collisions — flag every one.
3. **No duplicate `name:`** — the same `name:` declared by two folders means one
   shadows the other. List all collisions.
4. **Tier inventory** — count basic `our-*` vs protected `our-adv-*`; list the
   `our-adv-*` machine-local skills explicitly so the user sees what is *not*
   managed by the central library.
5. **Both tools in sync** — the same skill set should exist in both dirs (ignoring
   `our-adv-*`, which may legitimately differ per tool). Report anything present in
   one but not the other.
6. **Version** — read the installed `VERSION` file in each dir (if present) and
   report it.

Output a short PASS/FAIL per check with the specific offending paths. End with one
line: healthy / needs attention + the single most important issue.

## B. Catalog consistency (only inside the Ourskill repo)

Detect the repo by the presence of `skills/`, `SKILLS.md`, and `VERSION` in the
working directory. If not present, skip this section. If present, also verify:

1. **Catalog ↔ folders** — every `skills/our-*` folder has a row in `SKILLS.md`,
   and every `SKILLS.md` row maps to an existing folder. List mismatches both ways.
   `our-adv-*` must NOT appear in the catalog (machine-local tier).
2. **Count agreement** — the count in the `SKILLS.md` "Skill List (N)" heading
   equals the actual number of `skills/our-*` folders.
3. **Version label agreement** — the version in `VERSION` is the single source of
   truth. Flag any stray hardcoded version number elsewhere (README/SKILLS
   headers) that disagrees with it. (The `Changelog.md` version history is expected
   and not a drift.)
4. **Frontmatter integrity** across `skills/` — same checks as A.1–A.3 but against
   the repo source.
5. **No dangling references** — `our-*` cross-references in skill bodies point to
   skills that still exist under the current names (catch stale names after a
   rename).

Report the same PASS/FAIL style. This is the check that catches stale catalog
counts and version drift *before* they ship.

## Notes

- Read-only: this skill diagnoses and reports; it does not modify or reinstall.
  To fix a broken install, run `/our-skill-update` (clean reinstall). To fix
  catalog drift, edit `SKILLS.md` / the offending file.
- On a consumer machine the repo is deleted after install, so section B simply
  does not run there — that is expected, not a failure.
