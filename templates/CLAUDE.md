# CLAUDE.md: {{PROJECT_NAME}}

<!--
lanes template. The coordination session copies this file to the project root and fills every {{…}}.
Sections marked (method) are the lanes protocol: keep them unless you change the method on purpose.
Sections marked (project) are yours: stack, domain rules, commands.
Delete this comment when done.
-->

{{ONE_PARAGRAPH: what the project is, who uses it, what matters most (e.g. "correct before fast").}}

## Working agreements (project)

- **Language:** {{LANGUAGE}} for every doc, brief, plan, commit message, PR and message to the owner. Code identifiers in English.
- **Owner:** {{OWNER_NAME}} approves plans, merges PRs and makes the calls that are not in `docs/`.
- **Commits and PRs:** {{ATTRIBUTION_RULE, e.g. "no AI attribution: no Co-Authored-By, no 'Generated with' lines"}}.
- **Architecture stance:** {{e.g. "decouple only what is likely to change (models, vendors); no clean architecture layers"}}.
- {{Other standing preferences.}}

## Sources of truth (method)

| What | Where |
|---|---|
| Working rules (this file) | `CLAUDE.md` |
| Decisions (D1, D2, …) | `docs/decisions.md` |
| Shared memory: lane state, carry-overs, gotchas, owner to-dos | `docs/memory.md` |
| Roadmap and status of every brief | `docs/briefs/INDEX.md` |
| What your session must deliver: scope, boundaries, acceptance | `docs/briefs/<ID>-<slug>.md` (the **brief**) |
| How you implement it: files, tests, tasks | `docs/plans/<ID>-<slug>.md` (the **plan**, you write it) |
| {{Project-specific sources: schema, contracts, design system…}} | {{path}} |

- The **brief** is the *what*. The coordination session writes it; it does not change during your session.
- The **plan** is the *how*. You write it from the brief, and the owner approves it before any code.
- If something contradicts these files, these files win. If they contradict each other, stop and ask.
- **Read only what your brief lists under "Read first".** Do not walk all of `docs/`.

## Session protocol (method)

Start prompt: *"Start the brief `docs/briefs/<ID>-<slug>.md` following `CLAUDE.md`. Your decision goes as D<n>."*

0. **Isolate.** Never work on `main` or in the main checkout.
   - If you are in the main checkout: `git fetch origin` and enter a worktree named after the brief id (lowercase).
   - If you are already in a worktree: do not create another one.
   - Rename the branch to the one the brief gives, and run `{{SETUP_CMD}}`.
1. **Read** this file, `docs/memory.md`, your brief and **only** what the brief lists under "Read first". If your brief depends on another, read that brief's "What's left", not its code.
2. **Write the plan** with the skill `lanes:planning`: `docs/plans/<ID>-<slug>.md`, following `docs/plans/_template.md`. No code before the owner's OK.
   - Tests are listed before code. Every deviation from the brief is marked as such.
   - Questions for the owner go at the top, each with **your recommended option first and why**.
   - The plan ends with **"Context for implementation"**: written so that the plan alone is enough to implement after a compaction.
   - **Stop and wait for the OK.** If the owner asks for changes, fix the plan and wait again.
3. **Compact at the boundary.** After the OK (and the adjustments are in the plan), compact with: *"Keep the approved plan, the adjustments and the context for implementation; drop exploratory reads."* If the context is already above ~75 %, prefer `/clear` and restart from the plan.
4. **Implement test-first** with the skill `lanes:test-first`: red → code → green → refactor. Tick each task (`- [x]`) as you finish it; add unplanned tasks marked `(new)`. The plan always shows where you are.
5. **Run the checks:** `{{CHECK_CMD}}`. Nothing moves on until it is green.
6. **Review with agents** (from the lanes plugin; launch the ones that apply in parallel): `lanes:code-reviewer` always; `lanes:database-reviewer` if you touched SQL, migrations, schema or non-trivial queries; `lanes:security-reviewer` if you touched auth, public endpoints, webhooks, secrets, uploads, outbound calls or personal data. {{Project-specific reviewers, if any (e.g. a front-end reviewer).}} Fix everything critical and high; the rest goes to "What's left".
7. **Close the brief, in the same PR:**
   - fill the brief's **"What's left"**: what the module exposes, what deviated and why, what is pending (and for which future brief);
   - copy the items meant for other briefs into `docs/memory.md` under "Carry-overs";
   - add your decision block to `docs/decisions.md` (the number you were given);
   - mark the brief `done` in `docs/briefs/INDEX.md` with the PR link.
8. **Open the PR** against `main` and end with the **final report** (below) and the PR URL on its own line.
9. **After the merge**, only when the owner says it merged: confirm with `gh pr view --json state` that it is `MERGED`, then clean up (worktree, per-worktree databases or caches). **Never delete a worktree with an open or unpushed PR.**

**If you need a decision that is not in `docs/`, stop and ask. Do not invent.** The answer goes to `docs/decisions.md` in the same PR.

### Final report (method)

Short, in this order:

1. **Done:** what the PR delivers, in plain words (behaviour, not files).
2. **Verification:** checks run and their result (numbers), reviews run and what they found.
3. **Not done / honest notes:** anything skipped, tested late, or only mocked.
4. **Owner to-dos:** what only the owner can do before this works for real (accounts, keys, payments, approvals).
5. **One decision for you** (if any): the options, with your recommendation first.
6. The PR URL, alone on the last line.

## Done means (method)

1. The plan's tests exist, were written first, and cover the brief's acceptance criteria.
2. `{{CHECK_CMD}}` is green.
3. Review agents passed with no critical or high findings open.
4. "What's left", `docs/memory.md`, `docs/decisions.md` and `INDEX.md` are updated in the PR.
5. The owner reviewed the diff.

## Project rules (project)

{{Stack, architecture, where the domain rules live (e.g. "the database is the guardian: do not repeat in code what constraints enforce"), code style, test conventions, local environment, git conventions (branch naming `<module>/<id>-<slug>`, Conventional Commits, squash merge), what not to do.}}
