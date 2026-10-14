# Shared memory

<!--
lanes shared memory. Lives at docs/memory.md, next to CLAUDE.md, and is read by EVERY session at start:
the coordination session, the lane sessions and the auditors.
It is the common memory that survives compactions and new sessions: if it is not here (or in decisions,
briefs, plans), nobody else knows it.

Rules:
- Short, dated entries. Delete what is no longer true instead of piling corrections.
- Facts and pointers, not narratives. Decisions go to docs/decisions.md, not here.
- The coordination session curates it. Lane sessions add to it in their own PR (carry-overs, gotchas).
- Changes reach `main` by PR like everything else; batch them with the coordination's doc PRs.
-->

**Last updated:** <YYYY-MM-DD> by <session>

## Lanes now

| Lane | Brief | Decision | Notes |
|---|---|---|---|
| 1 | <ID> | D<n> | <plan approved / implementing / PR #n open> |

**Next up:** <lane → brief (D<n>) after its current one merges>.

## Reserved decision numbers

<!-- Assign before starting a lane, and repeat it in the start prompt. Two sessions taking the same number is the most common collision. -->

- `main` has up to D<n>. Reserved: <ID> → D<n>, <ID> → D<n>. Skipped/empty: <D<n> and why>.

## Carry-overs (for future briefs)

<!-- Items that a closed brief left for a later one. The coordination session folds them into the brief when it writes it, then deletes them here. -->

**For <ID> (<title>), from <ID>:** <what and why, with a pointer to the "What's left" that has the detail>.

## Gotchas

<!-- Things every session should know and nobody would guess: flaky tests and their cause, environment traps, tool quirks, vendor surprises. -->

- <YYYY-MM-DD> <gotcha> — <what to do about it>.

## Owner to-dos

<!-- What only the owner (or the business) can do: payments, accounts, approvals, questions to third parties. -->

- [ ] <to-do> — blocks <ID or feature>.

## Process notes

<!-- Lessons about the method itself in this project: what to do differently next time. -->

- <YYYY-MM-DD> <lesson>.
