---
name: writing-briefs
description: Write a lanes brief — the one-page WHAT a lane session will plan and implement. Use when the coordination session needs a new brief, or a batch of briefs for the next wave. Covers the template, the rules that keep briefs short and true, and the pre-push audit.
---

# Writing briefs

A brief tells a lane session **what** to deliver: scope, boundaries, acceptance. The session writes the **how** (the plan) with the code in view. A good brief lets the session plan without asking anything already decided, and without reading anything it does not need.

Template: `${CLAUDE_PLUGIN_ROOT}/templates/brief.md` (copy it to `docs/briefs/<ID>-<slug>.md`).

## Before writing

1. **Read the state:** `docs/memory.md` (carry-overs for this brief, gotchas, reserved numbers) and `docs/briefs/INDEX.md`.
2. **Gather what earlier briefs left for this one:** the "Carry-overs" in memory and the "What's left" of the briefs it depends on. Each carry-over becomes a line in "In scope", "Out of scope" or "Known edge cases". Then remove it from memory.
3. **Verify every claim about the current system before you write it.** If the brief says "the function exists", "the database already enforces it", "there is no route for X", grep it first. A false claim in a brief costs a whole planning round. This is also how gaps are found (e.g. "there is no client API at all": that was a missing brief, not a detail).
4. **Ask the owner only what changes the brief.** Use one question per decision, options with your recommendation first. Business questions that only the business can answer go to decisions §3 with a provisional assumption instead of blocking.

## Rules for the content

- **What, not how.** Name behaviours, rules and constraints. Leave files, functions and order of work to the plan. Exception: name the *place* when the project's rules dictate it ("in the database, not in code", "in the app, per decision D89").
- **Cite decisions by number, and check each number says what you claim.** Wrong citations are the most common brief bug.
- **"Read first (only this)" is short and narrow:** specific decisions, specific files or sections. The session reads nothing else.
- **Out of scope is explicit**, and each item says where it goes (another brief, the owner, later).
- **Acceptance criteria are observable and testable**, each one with how it is tested. The last one is always "the checks are green".
- **Known edge cases** are the cases you already know are tricky (races, partial failures, purged/deleted data, out-of-order events). The session finds more; you write down the ones you know.
- **Decisions the session must propose** are named as such: "the plan proposes X and the owner decides". Do not decide them in the brief by accident.
- **Dependencies are real:** "depends on" means it cannot start before that merge. If a dependency only affects one section, say so ("A1 only for the meetings section").
- One page. If it does not fit, it is two briefs.

## Batch and roadmap

- Update `docs/briefs/INDEX.md` (rows, dependencies) and `docs/memory.md` (lanes, next up, reserved decision numbers) in the same PR.
- Reserve the decision number of each brief now. Collisions happen when two lanes pick "the next free one".
- If writing the brief changed another brief (a dependency moved, an item belongs elsewhere), edit that brief in the same PR and say so.

## Audit before pushing

Run the `auditor` agent (from this plugin) on the new briefs **before** pushing. Two auditors in parallel work well for a batch:

- one against **the code and the data** (are the claims true? is something missing that the code makes obvious?);
- one against **the decisions and the method** (contradictions, wrong citations, format, lane collisions).

Apply what is right, verify what is surprising (spot-check the cited lines yourself), then push.

## The PR

- One branch per PR, fresh from `origin/main`, from the coordination worktree.
- Body: what enters, then **Closed** (what the owner decided) and **Pending** (what the owner or the plans will decide). The owner reads the body, not the diff.
- After merge, confirm that **every commit landed** (`git branch -r --contains <sha>` or check the file on `origin/main`). Commits pushed after the merge started are silently left out; open a follow-up PR for them.
