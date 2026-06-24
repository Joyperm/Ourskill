# Ourskill — Skill Directory (v0.0.3)

Choose the desired skill from this table and invoke it using the command in the **Command** column.
For full details on each skill, read `skills/<name>/SKILL.md`.

For installation/update instructions, see [README.md](README.md) ("Instructions for AI Agent" section).

---

## Skill List (36)

| Command | What it does | Category | Source |
|---------|--------------|----------|--------|
| `/our-hello` | Check that the `our-*` skill pipeline is installed and working correctly | utility | local |
| `/our-skill-update` | Check remote version and update installed skills | utility | local |
| `/our-skill-uninstall` | Uninstall all personal skills from local machine | utility | local |
| `/our-skill-autoread` | Skill router — match the current task to the right /our-* skill so you don't have to remember them all | utility | local |
| `/our-skill-expert` | Build a machine-local `our-adv-<stack>` expert skill (pull from a source repo if one exists, else generate) — installed locally only, never synced/overwritten | utility | local |
| `/our-code-debug` | 4-step debugging discipline: reproduce → trace → falsify → cross-reference | code | 9arm-skills |
| `/our-code-review` | Review a plan/PR/code from an outsider's perspective — question intent + trace code paths | code | 9arm-skills |
| `/our-code-postmortem` | Write a Root Cause Analysis (RCA) / post-mortem after fixing a bug | code | 9arm-skills |
| `/our-code-tdd` | TDD discipline — red-green-refactor: write a failing test first, minimum code to pass, then refactor (test-first, unlike /our-dev-tests) | code | local |
| `/our-code-audit-arch` | Scan the whole codebase for architecture drift (coupling, layering, circular deps, god files, duplication) → prioritized refactor report | code | local |
| `/our-code-onboard` | Run a parallel exploration subagent to map architecture/data/APIs/auth/deployment → produce onboarding doc | code | spencerpauly |
| `/our-dev-tests` | Analyze code → write unit/integration tests + mocks + edge cases | dev | spencerpauly |
| `/our-dev-e2e` | Set up Playwright end-to-end testing — config, smoke test, CI integration | dev | spencerpauly |
| `/our-dev-commit` | Write conventional commit messages (type/scope/body) | dev | spencerpauly |
| `/our-dev-pr` | Create a PR with title/description/linked issues/reviewers | dev | spencerpauly |
| `/our-dev-api` | REST/GraphQL design principles — resources, versioning, pagination, error formats | dev | wshobson |
| `/our-dev-errors` | Error-handling patterns — exceptions vs Result types, propagation, graceful degradation | dev | wshobson |
| `/our-dev-sql` | SQL query optimization — EXPLAIN analysis, indexing strategies, fixing slow queries | dev | wshobson |
| `/our-dev-tailwind` | Convert CSS rules into Tailwind utility classes | dev | spencerpauly |
| `/our-dev-npm` | Safely update npm packages (separate minor/major updates + handle migrations) | dev | spencerpauly |
| `/our-dev-perf` | Audit & optimize performance — bundle size, rendering, data fetching, Core Web Vitals | dev | spencerpauly |
| `/our-dev-security` | Systematically audit security: OWASP Top 10, secret leaks, risky patterns | dev | spencerpauly |
| `/our-setup-auth` | Add authentication (NextAuth/Auth.js) — OAuth, sessions, protected routes | setup | spencerpauly |
| `/our-setup-docker` | Dockerize: production-grade Dockerfile + docker-compose + .dockerignore | setup | spencerpauly |
| `/our-setup-ci` | Set up GitHub Actions CI: lint / test / type-check / deploy | setup | spencerpauly |
| `/our-setup-db` | Design database schemas: tables, relationships, indexes, constraints, ORMs | setup | spencerpauly |
| `/our-setup-ui` | Enforce design system (spacing/color/typography/dark mode) for consistent generated UIs | setup | spencerpauly |
| `/our-setup-secrets` | Secure secrets/credentials management for CI/CD (Vault, AWS/Azure/GCP, GitHub Actions) | setup | wshobson |
| `/our-prod-prompting` | Write prompts for LLMs: named frameworks (CO-STAR/RTF/APE…) + structure, few-shot, CoT, system prompts, output parsing | prod | spencerpauly·local |
| `/our-prod-pattern` | Identify repeated workflows → automatically convert them into a new SKILL.md | prod | spencerpauly |
| `/our-prod-context` | Save research/decisions/lessons learned into a workspace file for cross-session context | prod | spencerpauly |
| `/our-prod-adr` | Record Architecture Decision Records: context, options, rationale | prod | spencerpauly |
| `/our-prod-mgmt` | Rewrite engineering updates/reports for executives/management, tailored for the channel | prod | 9arm-skills |
| `/our-prod-focus` | Prevent looping on long tasks + manage context budget + hand off before context is full | prod | 9arm-skills |
| `/our-prod-grill` | Conduct a deep design interview, pressure-testing assumptions before building (one question at a time) | prod | local-adapted |
| `/our-prod-cheer` | Provide context-aware encouragement and perspective without being generic or using templates | prod | local |

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

**v0.0.3** — Full skill rename to `our-<category>-<action>` pattern (our-code-*, our-dev-*, our-setup-*, our-prod-*); consumer machines require Phase A on this update
**v0.0.2** — `our-adv-*` machine-local tier + `/our-skill-expert`, `/our-code-tdd`, `/our-code-audit-arch`; prompting frameworks merge; secrets-safety notes; audit fixes
**v0.0.1** — Initial gathering set

| Source key | Repository / Origin |
|------------|---------------------|
| `spencerpauly` | github.com/spencerpauly/awesome-cursor-skills |
| `wshobson` | github.com/wshobson/agents |
| `9arm-skills` | github.com/thananon/9arm-skills |
| `local-adapted` | Adapted from local `AgentJoJoy/grill-me` to be generic |
| `local` | Created locally in this repository (our-hello, our-cheer, our-skill-autoread, our-test-driven, our-audit-arch, our-stack-expert) |

> Other skill sources that have not yet been pulled are listed under "Other Skill Sources" in [README.md](README.md).

---

## Update Log

> Record skills added, modified, or removed each release — used by Phase B (incremental update) to know which folders to sync.
> Full descriptions and rationale for each change are in [Changelog.md](Changelog.md).

| Version | Action | Skill |
|---------|--------|-------|
| 0.0.3 | Renamed (31) | See Changelog `[Unreleased]` for full old→new table. Consumer machines require **Phase A** (clean slate) to remove old names. |
| 0.0.2 | Added | `/our-stack-expert`, `/our-test-driven`, `/our-audit-arch` |
| 0.0.2 | Modified | `/our-prompting` (Named Frameworks merged), `/our-skill-update`, `/our-skill-uninstall`, `/our-skill-autoread`, `/our-skill-from-pattern`, `/our-secrets`, `/our-add-auth`, `/our-setup-ci`, `/our-add-docker`, `/our-audit-security`, `/our-debug`, `/our-review`, `/our-postmortem` |
