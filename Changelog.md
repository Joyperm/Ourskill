# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.0.2] - 2026-06-23

### Added
- **Machine-local `our-adv-*` tier**: a protected namespace for advanced, machine-specific skills (e.g. stack experts) that are created on one machine, never pushed, and **never touched** by `/our-skill-update` or `/our-skill-uninstall`. The recursive sweep (Phase A, update, uninstall) now skips any `name:` starting with `our-adv-`. `/our-skill-autoread` includes them and prefers them when they match a task more tightly. Documented under "Skill Tiers" in README.
- `/our-stack-expert`: generator skill that builds a machine-local `our-adv-<stack>` expert (pull from a known source repo if one exists, else generate self-contained), installs it locally only, and never adds it to the shared catalog or pushes it.
- `/our-test-driven`: TDD discipline (red-green-refactor / test-first), kept distinct from `/our-write-tests` (test-after) and `/our-debug` (bug fixing).
- `/our-audit-arch`: whole-codebase architecture-drift audit (coupling, layering, circular deps, god files, duplication) producing a prioritized refactor report; distinct from `/our-review` (diff) and `/our-onboard-codebase` (mapping). Inspired by ideas in `mattpocock/skills`. Total 36 skills.
- `/our-prompting`: merged a **Named Frameworks** reference (16 frameworks — RTF, CO-STAR, RISE, APE, CRAFT, GRADE, etc.) with a selection matrix and how-to-pick guide, so all prompt guidance lives in one skill (single source of truth). The standalone draft was dropped.
- **Secrets safety** notes in secret/API-sensitive skills (`/our-secrets`, `/our-add-auth`, `/our-setup-ci`, `/our-add-docker`, `/our-audit-security`): warn the user and confirm `.env`/secrets handling before acting; never print or commit real values.

### Fixed
- Aligned stale command/skill references to `/our-` names (`/our-debug`, `/our-review`, `/our-postmortem`) and removed dangling cross-skill links and source-repo leftovers found in a full repo dependency audit. Genericized `/our-skill-from-pattern` to work in both Claude Code and Cursor.

## [0.0.1] - 2026-06-18

### Added
- Initial collection of 26 utility, setup, fullstack, engineering, self-dev, and productivity skills for Claude Code and Cursor.
- Added new utility meta-skills `/our-skill-update` and `/our-skill-uninstall` to automate skill management.
- Project documentation (`README.md` and `SKILLS.md`) translated to English for international usage.
- Added 7 full-stack skills (from wshobson/agents + spencerpauly/awesome-cursor-skills): `/our-api-design`, `/our-error-handling`, `/our-secrets`, `/our-sql-optimize`, `/our-audit-perf`, `/our-e2e-tests`, plus the `/our-skill-autoread` skill router — total 33 skills, still v0.0.1 (not yet used in production).

### Fixed
- Updated `skills/our-hello/SKILL.md` to remove outdated references to `scripts/install.ps1` and `bootstrap one-liner`, aligning with the AI-agent-managed installation workflow.
