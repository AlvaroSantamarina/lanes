---
name: planning
description: Write a lane's plan from its brief — the HOW, with the real code in view — and stop for the owner's OK before any code. Use at step 2 of the session protocol in CLAUDE.md, right after reading the brief and its "Read first" list.
argument-hint: "[docs/briefs/<ID>-<slug>.md]"
---

# Planning (lane session)

Output: `docs/plans/<ID>-<slug>.md`, following `docs/plans/_template.md` (from `${CLAUDE_PLUGIN_ROOT}/templates/plan.md`). Then **stop and wait**. No code, no scaffolding, no "quick spike" before the OK.

## 1. Restate the brief in your head, not in the plan

Read the brief, `docs/memory.md` and **only** the brief's "Read first" list. If the brief depends on others, read their "What's left", not their code. If you are tempted to read more of `docs/`, you need a question, not a read.

## 2. Ground the plan in the code

For every piece of the brief, find where it lands and what it must mirror:

- **The pattern to copy:** the closest existing module that does something similar (route, job, migration, test). Name it with `path:line`. New code looks like the code around it.
- **Load-bearing facts:** anything the plan relies on ("this trigger already exists", "this error maps by constraint name", "this cron option works with our pool"). **Verify each one** — open the file at the line, run the query, read the library source if needed — and list it under "What I verified before planning". An auditor will check exactly these; a false one costs a round.
- **The registries** you will add one line to (routes, jobs, settings, error maps), instead of editing shared code.

Read as much as you need to be right, and no more: targeted searches, not whole-directory walks.

## 3. Decide, or ask

- Decide everything the brief, the decisions and the code let you decide. Do not ask the owner what is already in `docs/`.
- When the brief says "the plan proposes X and the owner decides", or you hit a real business or product choice: put it under **"Questions for the owner"**, with the options and **your recommendation first**, with the reason. One question per decision.
- Anything you do differently from the brief, or beyond it (an extra migration, a contract change, touching another module): **"Deviations from the brief"**, each with its reason. Contract changes that affect another team (the front-end) also go to "What's left" for them.

## 4. Tests before tasks

List the tests first (id, behaviour, which acceptance criterion it covers), including the hard ones: concurrency, out-of-order events, purged or deleted data, time boundaries (midnight in the business's timezone, DST). Then the tasks, in order, one commit each when possible, each naming its tests.

## 5. Write "Context for implementation" last

Write it for a reader who has lost everything except this plan (after `/compact` or `/clear`): the map of where things go, the facts with `path:line`, the traps you found, and — once approved — the owner's adjustments pasted in. If resuming would require re-exploring, this section is not done.

## 6. Hand it over

Tell the owner, briefly: where the plan is, the questions (with your recommendations), the deviations, the risks. Then stop.

When the OK arrives with adjustments: apply them to the plan (decisions, tests, tasks, context), mark the status as approved, then compact as the protocol says before writing the first test.
