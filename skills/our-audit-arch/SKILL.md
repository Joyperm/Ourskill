---
name: our-audit-arch
description: Scan a whole codebase for architecture drift — coupling, layering violations, circular dependencies, god files, duplicated logic, leaky abstractions, inconsistent patterns — and produce a prioritized report of refactors that preserve the intended design. Use when a project is turning into a "ball of mud", before starting a big feature, or as a periodic structural health check. Distinct from /our-review (reviews a diff/PR) and /our-onboard-codebase (only maps the structure).
user-invocable: true
---
# Architecture Audit — find the drift, protect the design

Codebases decay one reasonable shortcut at a time until they become a "ball of
mud". This skill scans the **whole project's structure** (not a single diff) and
reports where the design is drifting, with concrete refactors to pull it back.

> **Not the same as the siblings:**
> - `/our-review` reviews a specific change/diff/PR.
> - `/our-onboard-codebase` *maps* the structure to learn it.
> - `/our-audit-perf` and `/our-audit-security` audit a different lens.
> - **This skill** audits **structural/architectural health** and prescribes refactors.

## Steps

1. **Establish the intended design.** Infer (or ask for) the architecture the
   project is *supposed* to follow — layers, module boundaries, where business
   logic lives, allowed dependency directions. You can't measure drift without the
   intended shape. Check for an `ARCHITECTURE.md`, ADRs (`/our-adr`), or a README.

2. **Map the real structure.** Build the actual module/dependency graph: which
   files/modules import which. Note entry points, layers, and boundaries as they
   *actually* are.

3. **Scan for drift signals:**
   - **Layering violations** — lower layers importing higher ones; UI reaching into
     the database; business logic leaking into controllers/components.
   - **Circular dependencies** — modules that import each other directly or in a cycle.
   - **High coupling / low cohesion** — a module that touches everything; unrelated
     things bundled in one file.
   - **God files / god functions** — oversized files, very long functions, classes
     doing many unrelated jobs.
   - **Duplicated logic** — the same rule/algorithm implemented in several places.
   - **Leaky abstractions** — implementation details (SQL, HTTP, framework types)
     bleeding across boundaries that should hide them.
   - **Inconsistent patterns** — the same problem solved three different ways across
     the codebase (error handling, data access, validation).
   - **Dead / orphaned code** — modules nothing imports.

4. **Rank by impact × effort.** For each finding, note severity (how much it slows
   change or invites bugs) and rough effort to fix. Prioritize high-impact /
   low-effort first.

5. **Generate the report.** For each finding: location (file/module), what the drift
   is, why it hurts, and a **specific refactor** that moves back toward the intended
   design. Group into "fix now / fix soon / watch". End with 3–5 highest-leverage
   moves.

## Principles

- **Describe drift relative to the intended design**, not your personal taste — if
  there's no stated design, surface that gap first (recommend an ADR / ARCHITECTURE.md).
- **Recommend incremental, safe refactors** — boundary by boundary, with tests as a
  net (pair with `/our-test-driven` or `/our-write-tests`).
- **Don't prescribe a rewrite.** The goal is to preserve and restore design, not
  replace it.

## Notes

- This is a read-and-report pass; it does not change code unless the user then asks.
- For large repos, sample the worst-offender areas first rather than boiling the ocean.
- Record any architecture decisions that come out of the audit as ADRs (`/our-adr`).
