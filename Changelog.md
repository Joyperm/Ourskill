# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

> Accumulating changes since 0.0.1 (already installed on another machine). VERSION
> stays `0.0.1` until these ship together as `0.0.2`, which `/our-skill-update`
> will detect and roll out to consumer machines.

### Added
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
