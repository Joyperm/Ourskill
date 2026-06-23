# Ourskill — Skill Directory (v0.0.1)

Choose the desired skill from this table and invoke it using the command in the **Command** column.
For full details on each skill, read `skills/<name>/SKILL.md`.

For installation/update instructions, see [README.md](README.md) ("Instructions for AI Agent" section).

> 🚧 **Gathering Phase (v0.0.x):** Currently pulling skills from multiple sources — all pinned at **v0.0.1**.
> Remote repo and detailed changelogs are not yet set up because currently "installation = clear all old ones + install new set (Phase A)". Incremental updates (Phase B) will be used when the skill set becomes stable and a remote repo is established.

---

## Skill List (34)

| Command | What it does | Category | Source |
|---------|--------------|----------|--------|
| `/our-hello` | Check that the `our-*` skill pipeline is installed and working correctly | utility | local |
| `/our-skill-update` | Check remote version and update installed skills | utility | local |
| `/our-skill-uninstall` | Uninstall all personal skills from local machine | utility | local |
| `/our-debug` | 4-step debugging discipline: reproduce → trace → falsify → cross-reference | engineering | 9arm-skills |
| `/our-postmortem` | Write a Root Cause Analysis (RCA) / post-mortem after fixing a bug | engineering | 9arm-skills |
| `/our-review` | Review a plan/PR/code from an outsider's perspective — question intent + trace code paths | engineering | 9arm-skills |
| `/our-onboard-codebase` | Run a parallel exploration subagent to map architecture/data/APIs/auth/deployment → produce onboarding doc | engineering | spencerpauly |
| `/our-mgmt-rewrite` | Rewrite engineering updates/reports for executives/management, tailored for the channel | productivity | 9arm-skills |
| `/our-stay-on-track` | Prevent looping on long tasks + manage context budget + hand off before context is full | productivity | 9arm-skills |
| `/our-grill-me` | Conduct a deep design interview, pressure-testing assumptions before building (one question at a time) | planning | local-adapted |
| `/our-add-auth` | Add authentication (NextAuth/Auth.js) — OAuth, sessions, protected routes | setup | spencerpauly |
| `/our-add-docker` | Dockerize: production-grade Dockerfile + docker-compose + .dockerignore | setup | spencerpauly |
| `/our-setup-ci` | Set up GitHub Actions CI: lint / test / type-check / deploy | setup | spencerpauly |
| `/our-db-design` | Design database schemas: tables, relationships, indexes, constraints, ORMs | setup | spencerpauly |
| `/our-ui-stack` | Enforce design system (spacing/color/typography/dark mode) for consistent generated UIs | setup | spencerpauly |
| `/our-write-tests` | Analyze code → write unit/integration tests + mocks + edge cases | fullstack | spencerpauly |
| `/our-commit-msg` | Write conventional commit messages (type/scope/body) | fullstack | spencerpauly |
| `/our-create-pr` | Create a PR with title/description/linked issues/reviewers | fullstack | spencerpauly |
| `/our-audit-security` | Systematically audit security: OWASP Top 10, secret leaks, risky patterns | fullstack | spencerpauly |
| `/our-update-npm` | Safely update npm packages (separate minor/major updates + handle migrations) | fullstack | spencerpauly |
| `/our-css-to-tailwind` | Convert CSS rules into Tailwind utility classes | fullstack | spencerpauly |
| `/our-prompting` | Write prompts for LLMs: named frameworks (CO-STAR/RTF/APE…) + structure, few-shot, CoT, system prompts, output parsing | self-dev | spencerpauly·local |
| `/our-skill-from-pattern` | Identify repeated workflows → automatically convert them into a new SKILL.md | self-dev | spencerpauly |
| `/our-save-context` | Save research/decisions/lessons learned into a workspace file for cross-session context | self-dev | spencerpauly |
| `/our-adr` | Record Architecture Decision Records: context, options, rationale | self-dev | spencerpauly |
| `/our-cheer` | Provide context-aware encouragement and perspective without being generic or using templates | motivation | local |
| `/our-api-design` | REST/GraphQL design principles — resources, versioning, pagination, error formats | fullstack | wshobson |
| `/our-error-handling` | Error-handling patterns — exceptions vs Result types, propagation, graceful degradation | fullstack | wshobson |
| `/our-secrets` | Secure secrets/credentials management for CI/CD (Vault, AWS/Azure/GCP, GitHub Actions) | setup | wshobson |
| `/our-sql-optimize` | SQL query optimization — EXPLAIN analysis, indexing strategies, fixing slow queries | fullstack | wshobson |
| `/our-audit-perf` | Audit & optimize performance — bundle size, rendering, data fetching, Core Web Vitals | fullstack | spencerpauly |
| `/our-e2e-tests` | Set up Playwright end-to-end testing — config, smoke test, CI integration | fullstack | spencerpauly |
| `/our-skill-autoread` | Skill router — match the current task to the right /our-* skill so you don't have to remember them all | utility | local |
| `/our-stack-expert` | Build a machine-local `our-adv-<stack>` expert skill (pull from a source repo if one exists, else generate) — installed locally only, never synced/overwritten | utility | local |

<!--
Add new rows to the bottom of the table using this format:
| `/our-<name>` | <short description> | <category> | <local | spencerpauly | 9arm-skills | local-adapted> |
-->

> **Note — `our-adv-*` skills are not listed here.** They are a **machine-local**
> "advanced" tier (e.g. stack experts built by `/our-stack-expert`): created on one
> machine, never pushed, and protected from `/our-skill-update` /
> `/our-skill-uninstall`. This catalog only tracks the shared/basic library. See
> "Skill Tiers" in [README.md](README.md).

---

## Versions & Sources

**v0.0.1** — Initial gathering set (see [VERSION](VERSION))

| Source key | Repository / Origin |
|------------|---------------------|
| `spencerpauly` | github.com/spencerpauly/awesome-cursor-skills |
| `wshobson` | github.com/wshobson/agents |
| `9arm-skills` | github.com/thananon/9arm-skills |
| `local-adapted` | Adapted from local `AgentJoJoy/grill-me` to be generic |
| `local` | Created locally in this repository (our-hello, our-cheer, our-skill-autoread) |

> Once the skill set starts to stabilize, we will move to v0.1.0 + set up remote + start per-release changelogs (Phase B).
> Other skill sources that have not yet been pulled are listed under "Other Skill Sources" in [README.md](README.md).
