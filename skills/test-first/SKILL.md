---
name: test-first
description: Implement an approved lanes plan test-first — red, green, refactor, one task at a time, ticking the plan as you go and keeping honest evidence. Use at the implementation step of the session protocol in CLAUDE.md, after the plan's OK and the compaction.
argument-hint: "[docs/plans/<ID>-<slug>.md]"
---

# Test-first implementation (lane session)

Input: the approved plan. It is the source of truth for what to build and in what order; its "Context for implementation" tells you where things are. Re-read the plan, not the codebase.

## The loop, per task

1. **Red.** Write the task's tests from the plan. Run them and **see them fail for the right reason** (the behaviour is missing, not an import error or a typo). Keep the failing line for the evidence.
2. **Green.** Write the least code that makes them pass, mirroring the pattern the plan names.
3. **Refactor** with the tests green. No new behaviour in this step.
4. **Tick** the task in the plan (`- [x]`). A task that appeared on the way is added and marked `(new)`. Commit (one per task when possible; Conventional Commits; the project's attribution rule).

Run only the relevant tests while looping; run the full check (`CLAUDE.md`) before review and before the PR.

## Rules

- **Behaviour, not implementation.** Test what a caller, a user or the database can observe. Mock only the external services the project already mocks.
- **The hard tests are not optional:** concurrency (two transactions, a barrier, not a sleep), out-of-order and repeated events, time boundaries with an injected clock, failure in the middle. If the plan lists them, they are written before the code like the rest.
- **Flaky is a bug.** A test that depends on timing, ordering between parallel tests or the real clock gets fixed with a barrier or an injected clock, not with retries or longer sleeps. If you find a flaky test from another module, note it in `docs/memory.md` "Gotchas" with its cause.
- **When the plan is wrong**, do not improvise silently: fix the plan (mark the change), and if it changes a decision or the scope, stop and ask the owner.
- **When the code says the brief is wrong** (a rule the database already enforces, a function that does not exist), same: stop and ask, then record the answer.

## Honest notes

Keep a short list as you go, for the final report and the plan:

- tests that were written after the code (and why);
- what was only tested with mocks;
- cases you decided not to test, and why.

The owner trusts the report because it says what was not done.

## Before review

- Full check green.
- Every task ticked, or explained in "What's left".
- The plan reflects what was actually built.

Then continue with the review agents and the closing steps in `CLAUDE.md`.
