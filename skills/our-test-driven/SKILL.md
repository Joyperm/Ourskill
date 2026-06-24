---
name: our-test-driven
description: Drive new code with tests first using the red-green-refactor discipline — write a failing test, write the minimum code to pass, then refactor. Use when building a new feature, function, or behavior and you want tests to shape the design (not tests written after the fact). Distinct from /our-write-tests (tests for code that already exists) and /our-debug (fixing an existing bug).
user-invocable: true
---
# Test-Driven Development (red → green → refactor)

Let failing tests drive the code. You don't write production code until a test
demands it. This shapes the design and guarantees coverage as a byproduct.

> **Not the same as the siblings:**
> - `/our-write-tests` = code already exists, write tests *around* it (test-after).
> - `/our-debug` = a bug exists, reproduce and fix it.
> - **This skill** = the code does *not* exist yet; a failing test pulls it into being (test-first).

## The cycle — one tiny loop at a time

1. **RED — write one failing test.** Pick the smallest next behavior. Write a test
   that asserts it. Run it and **watch it fail** (for the right reason — assertion,
   not a typo/import error). A test that passes immediately tested nothing.
2. **GREEN — make it pass with the minimum.** Write the least code that turns the
   test green — even if it's "too simple" or hardcoded. No extra features, no
   speculative abstraction. Run the test; confirm green.
3. **REFACTOR — clean up while green.** Now improve names, remove duplication,
   extract functions — with tests as your safety net. Re-run after each change;
   they must stay green. Don't add behavior here.
4. **Repeat** for the next behavior until the feature is complete.

## Rules that keep it honest

- **No production code without a failing test first.** If you're tempted to write
  code, write the test that requires it instead.
- **One failing test at a time.** Don't write five tests then code — that's not TDD.
- **Minimum to pass.** Resist building beyond what the current test demands;
  the next test will force the next piece.
- **See red before green.** Always observe the failure first, so you trust the test.
- **Refactor only when green.** Never refactor and change behavior in the same step.

## Getting started

1. Detect the test framework already in the project (Jest/Vitest/Pytest/JUnit/Go
   test/etc.) and follow its conventions. If none exists, set up the idiomatic one
   for the stack first.
2. Restate the feature as a short list of **observable behaviors**, smallest first.
3. Run the red-green-refactor loop on behavior #1, then move down the list.
4. Keep the test suite fast — slow tests kill the rhythm.

## When TDD is the wrong tool

- Throwaway spikes / exploration where the design is totally unknown — explore
  first, then TDD the real implementation.
- Pure UI/visual tweaks with no logic to assert.
- Fixing an existing bug → use `/our-debug` (though writing a failing test that
  reproduces the bug *before* fixing is a great TDD-flavored habit).
