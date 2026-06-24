---
name: our-skill-expert
description: Create a machine-local "stack expert" skill for a specific tech stack (e.g. Next.js, Django, Rails, Spring). Pulls a matching skill from a known source repo when one exists, otherwise generates a self-contained one from scratch, then installs it locally as an `our-adv-<stack>` skill that the central library never overwrites. Use when the user wants deep, stack-specific guidance on this machine without polluting the shared library — "make me a Next.js expert skill", "I need a Django expert here", "add a stack expert for my work machine".
user-invocable: true
---

# our-stack-expert — build a machine-local stack expert

Different machines need different depth. A work machine might want a strong
**stack expert** (framework conventions, gotchas, best practices) that a general
library shouldn't carry everywhere. This skill builds one **on this machine only**.

## Output contract (read this first)

- The result is installed as **`our-adv-<stack>`** (frontmatter `name: our-adv-<stack>`).
- `our-adv-*` is the **machine-local "advanced" tier**: it is **never pushed** to
  the central repo, **never added** to the shared catalog, and is **protected** —
  `/our-skill-update` and `/our-skill-uninstall` skip anything named `our-adv-*`, so
  syncing the central library never deletes or overwrites it.
- ⚠️ Because it lives only on this machine, it is **not recoverable** from the
  central repo. If it matters, the user should keep their own backup.

## Steps

### 1. Clarify the target

Ask only what you can't infer:
- **Stack / framework** + major version (e.g. "Next.js 15 App Router", "Django 5").
- **Focus** — what they want the expert strong at (e.g. routing, data layer,
  testing, performance, deployment). Default: broad best-practices + common gotchas.
- **Tool** to install for — Claude Code, Cursor, or both (default both).

Derive the slug: lowercase, hyphenated, no version noise unless it matters
→ `our-adv-nextjs`, `our-adv-django`, `our-adv-spring-boot`.

### 2. Try to PULL an existing expert (preferred)

Look for a ready-made skill for this stack before writing one:
- If the user names a source repo, use it.
- Otherwise check known framework-skill collections, e.g.
  `github.com/jeffallan/claude-skills` (framework-specific experts) or another the
  user trusts. (Pulling needs network + `git`; if offline, skip to step 3.)

If a good match exists: clone to a temp dir, take the one skill, then **adapt it**
before use:
- Rename to `name: our-adv-<slug>` (folder + frontmatter).
- **Genericize** — remove references to any specific external project; keep only
  framework conventions (optional "if present" notes are fine).
- **Make it self-contained (zero-dependency)** — inline or strip any
  `references/*.md`, `resources/*`, or links to files you didn't bring; flag any
  external CLI/service it assumes.
- Delete the temp clone.

### 3. Otherwise GENERATE from scratch

If no good match (or offline), write a self-contained expert from your own
knowledge of the stack. A good stack-expert skill covers:
- **Conventions** — idiomatic project structure, naming, file layout for this stack.
- **Best practices** — the patterns the framework's own docs/community endorse.
- **Gotchas** — the top mistakes and version-specific traps people hit.
- **Decision guidance** — when to use X vs Y within the stack.
- **Concrete snippets** — short, idiomatic examples, not walls of code.

Keep it tight and opinionated — an expert gives a clear default, not a survey.

### 4. Assemble the skill

```markdown
---
name: our-adv-<slug>
description: <keyword-rich — the stack + what it makes you good at + when to use>
---
# <Stack> Expert

<the guidance>
```

- Self-contained, no dangling links, no hidden external deps.
- **Secrets safety:** if the stack guidance touches `.env`, API keys, or
  credentials, include a short in-skill note — never print or commit real values;
  keep them in `.env` / a secrets manager.

### 5. Install LOCALLY ONLY

- Copy the `our-adv-<slug>/` folder into the chosen install dir(s):
  - Claude Code → `~/.claude/skills/`
  - Cursor → `~/.cursor/skills/`
- **Do NOT** add it to the repo's `skills/`, **do NOT** add a row to `SKILLS.md`,
  and **do NOT** commit or push it. It is machine-local by design.

### 6. Confirm

Tell the user the skill is installed as `/our-adv-<slug>`, that it is **protected**
from `/our-skill-update` (won't be wiped on sync), that it lives only on this
machine, and to reload Cursor / restart Claude Code to load it.

## Notes

- One stack per skill — don't bundle unrelated frameworks into one `our-adv-*`.
- To refresh an expert later, re-run this skill for the same stack; it overwrites
  the local `our-adv-<slug>` (still never touching the central library).
- `/our-skill-autoread` will include `our-adv-*` skills and prefer them when the
  task is on that stack.
