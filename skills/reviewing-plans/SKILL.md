---
name: reviewing-plans
description: Review a lane session's plan (or its final PR report) and hand the owner a paste-ready "OK to the plan with these adjustments" block. Use when the owner pastes a lane's message saying the plan is written and waiting for the OK, or when a lane reports its PR is open.
---

# Reviewing plans

The lane session wrote `docs/plans/<ID>-<slug>.md` in its worktree and is waiting for the owner's OK. Your job: catch what is false or missing **without re-planning**, answer the plan's questions with a recommendation, and give the owner one block to paste back.

## 1. Locate and size

- The plan lives in the lane's worktree, not on `main`: usually `.claude/worktrees/<id>/docs/plans/<ID>-<slug>.md`. Its brief is next to it; if the brief changed on `main` after the lane started, audit against the `main` version (`git show origin/main:docs/briefs/<file>`).
- Size it: `wc -l`. A plan under ~400 lines with one theme gets **one** auditor. A large mixed plan (many independent fixes, like a hardening brief) gets **two**, split by focus (e.g. "data and concurrency" / "security, real-time and API contract").

## 2. Audit (do not re-plan)

Launch the `auditor` agent with: the plan path, the brief path, the focus (if split), and the list of questions the plan asks the owner. Run two auditors in parallel, in the background, and wait for both before answering.

While they run, form your own view on the owner questions from what you already know (decisions, earlier briefs, what other lanes are doing). Do not duplicate the auditors' file reading.

When the reports arrive:

- **Spot-check the surprising findings** (one grep or one file view each) before passing them on. Auditors are usually right, sometimes confidently wrong.
- **Merge** the two reports; drop duplicates; keep only what changes the plan.
- **Decide each owner question** with a recommendation and its reason in one line. If you disagree with the plan's recommendation, say why.
- Watch for **cross-lane effects** the lane cannot see: two lanes touching the same files or migrations, an item another lane already covers, a brief that changed on `main`.

## 3. What the owner gets

First, in plain words and short: what the auditors found that matters (the one or two serious things), and your recommendation on any choice that is genuinely the owner's (a deviation from the brief, a business trade-off). Say clearly when a recommendation departs from the brief, so the owner can decide.

Then the block, in a fenced `text` code block, addressed to the lane session:

```text
OK to the plan with these adjustments (all go to D<n>):

Decisions:
- A: yes. / change: <what, and why in one line>.
- B: …

Adjustments:
1. <What to change> — <evidence in one line: path:line, or Dn>. <The concrete instruction>.
2. …

Leave as is: <decisions confirmed without changes, if worth naming>.
To "What's left": <items that should not be fixed now, and for whom (the front-end, a later brief, deploy)>.
```

Rules for the block:
- **Self-contained:** the lane must be able to act on it without this conversation. Include file:line and decision numbers.
- **Instructions, not discussions.** "Use X" rather than "consider X".
- **Ordered by the plan's own numbering** for the decisions, then adjustments by importance.
- If the owner may want to drop one adjustment (a recommended deviation from the brief), say so outside the block: "if you prefer to keep the brief, paste it without point N".

## 4. Final report and PR

When the lane reports its PR is open:

- Check CI (`gh pr view <n> --json statusCheckRollup,mergeable`), and that commits and body follow the project's attribution rule.
- Check the docs in the diff: brief "What's left" filled, INDEX row `done`, decision block added, carry-overs copied to `docs/memory.md`.
- **A red CI is not automatically the lane's fault.** Look at which test failed and whether it touched that area; check whether the same test failed on `main` before (`gh run list --branch main`). A flaky test from another module: rerun the failed job and route the fix to the lane where it fits, with the diagnosis.
- Turn the lane's "owner to-dos" into a short ordered list for the owner, and add them to `docs/memory.md`.
- Give the owner the **next start prompt** for that lane (close step → `/clear` → prompt with the reserved decision number).
