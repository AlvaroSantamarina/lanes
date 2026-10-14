# Plan <ID> · <Title>

**Brief:** [<ID>](../briefs/<ID>-<slug>.md) · **Branch:** `<module>/<id>-<slug>` · **Decision:** D<n> · **Status:** waiting for the owner's OK

<!--
lanes plan template. The lane session writes it from the brief, with the real code in view.
Keep it as short as the work allows. The owner reads the "Questions" and "Deviations" sections first.
-->

## Questions for the owner

<!-- Only what you cannot decide from the brief, the decisions or the code. Each with your recommendation first. -->

1. **<Topic>.** <The question in one sentence.>
   - **(Recommended) <Option A>:** <what happens, why it is the better default>.
   - <Option B>: <what happens, the trade-off>.

## Deviations from the brief

<!-- Anything you do differently from the brief, or beyond it (an extra migration, a contract change). Marked, with the reason. -->

- **Deviation 1:** <what> — <why>.

## What I verified before planning

<!-- Facts about the code/data/vendors that the plan relies on, each with file:line or source. The auditor checks these. -->

- <Fact> (`path/to/file.ts:42`).

## Approach

<!-- The design in a few paragraphs or bullets: what changes where, and why this way. -->

## Files

| File | Change |
|---|---|
| `path/to/file` | create / modify: <what> |

## Tests (written before the code)

| Id | Test | Covers |
|---|---|---|
| T1 | <behaviour under test> | acceptance criterion 1 |

## Tasks

<!-- In the order you will do them. One commit per task when the work allows. Tick as you go. Unplanned tasks: add them marked (new). -->

- [ ] 1. <task> (tests T1, T2)
- [ ] 2. <task>
- [ ] N. Checks, review agents, "What's left", memory, decisions, INDEX, PR.

## Risks and open edges

- <What could go wrong, and what you do about it or leave for "What's left".>

## Context for implementation

<!--
Written so that, after a compaction or /clear, this plan alone is enough to implement.
No exploration should be needed to resume.
-->

- **Map:** <where each piece lives; entry points; the registries you add a line to>.
- **Facts you will need:** <signatures, constraint names, error codes, env vars, with file:line>.
- **Traps found while planning:** <things that look obvious and are not>.
- **Adjustments from the OK:** <paste the owner's adjustments here once approved>.
