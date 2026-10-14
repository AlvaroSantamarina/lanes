# <ID> · <Title>

**Module:** <module> · **Branch:** `<module>/<id>-<slug>` · **Depends on:** <ids> · **Unblocks:** <ids or —> · **Status:** pending

<!--
lanes brief template. The coordination session writes it: the WHAT, not the HOW.
One page. Every claim about existing code or data is verified before it is written here.
-->

## Why
<What this brief delivers and for whom, in two to four sentences. The problem it closes, in the user's words where possible.>

## In scope
1. **<Piece>** (<decision refs>):
   - <behaviour, rule or constraint the session must respect>;
   - <…>.
2. **<Piece>:** <…>

## Out of scope
- **<Thing>:** <why, and which brief or owner it belongs to>.

## Read first (only this)
- `CLAUDE.md`
- `docs/decisions.md`: <D numbers, each with a word on why>
- <other source files or sections, as narrow as possible>
- The "What's left" of <previous briefs this one builds on>, and `docs/memory.md` "Carry-overs" for <ID>.

## Touches
- **Writes:** <tables, files, external systems>.
- **Migration / schema change:** <expected or "none expected">.

## Exposes
- <functions, endpoints, events, jobs other modules or the client will use>.

## Acceptance criteria
- [ ] <observable behaviour, with how it is tested> (test).
- [ ] <…>
- [ ] `{{CHECK_CMD}}` is green.

## Known edge cases
- **<Case>:** <what must happen>.

## Review
- `code-reviewer`
- <other reviewers, each with the focus that justifies it>.

## Plan
`docs/plans/<ID>-<slug>.md`: the session writes it, the owner approves it before code, and the session ticks tasks as it goes.

## What's left
<!-- Filled by the session when closing: what it exposes, what deviated and why, what is pending and for which brief. -->
