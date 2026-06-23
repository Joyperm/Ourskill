---
name: our-skill-autoread
description: Skill router for the our-* library. Matches the user's current task against the available /our-* skills and recommends the best-fitting one, so the user never has to remember the whole catalog. Trigger on /our-skill-autoread, when the user asks "which our skill should I use", "is there a skill for this", "what fits this task", and proactively at the start of a non-trivial task to check whether an our-* skill applies before diving in.
---
# our-skill-autoread — which /our- skill fits this task?

The `our-*` library is large and easy to forget. This skill matches the user's
current task against the available skills and recommends the best fit, so the user
never has to remember the whole catalog.

## Finding the available skills (NO hardcoded / personal paths)

Build the current `our-*` catalog from whichever source is available — never rely
on an absolute path to anyone's repo (e.g. a `.../Desktop/Ourskill/SKILLS.md`
path is wrong: consumer machines delete the cloned repo and only keep the
*installed* skills):

1. **Already-loaded skills (preferred):** if the running tool already exposes the
   installed skills and their descriptions (e.g. Claude Code lists available
   skills in context), use those directly.
2. **Scan the user-level skills directory** for the current tool and read each
   `our-*/SKILL.md` frontmatter (`name:` + `description:` only — that's enough):
   - Claude Code → `~/.claude/skills/`
   - Cursor → `~/.cursor/skills/`

Skip `our-skill-autoread` itself and any non-`our-*` skill. Include `our-adv-*`
skills — they are this machine's local "advanced" tier (often stack-specific
experts) and are frequently the most precise match for a task on that stack, so
prefer them when their `description:` fits more tightly than a basic skill's.

## What to do

1. Restate the user's current task / topic in one short line.
2. Match it against each available skill's `description:` (what it does + when to
   use it).
3. Recommend:
   - **Best fit** — the single most relevant `/our-<skill>` + one line on why.
   - **Runners-up** — up to 2 more, only if genuinely relevant.
   - **None** — if nothing fits well, say so plainly. Do not force a match.
4. Ask whether to run the recommended skill, or hand back for the user to decide.

## Style

- Be concise: a short recommendation, not a dump of the whole catalog.
- Do not auto-invoke the recommended skill unless the user agrees.
- Honest matching beats coverage — a wrong recommendation is worse than "none fit."
