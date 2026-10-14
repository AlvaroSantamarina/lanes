---
name: system-design
description: Phase 0 of lanes — turn an idea or an existing pile of notes into the decisions, the roadmap (core + waves) and the repo scaffolding that parallel lane sessions can build from. Use when starting a new project or a large new part of one, before any brief is written.
---

# System design (phase 0)

Goal: a repo where a lane session can start a brief and **never ask something already decided**. Everything below ends up as files in the repo; nothing important stays only in this conversation.

## 1. Understand the business

- Read what exists (notes, notebooks, old code, the client's messages). Treat old notes as **sources, not truth**: decisions weeks old get re-validated with the owner before building on them.
- Questions for the business side (the client, the owner's partner) go as a **numbered plain list**, one question per line, without jargon, in the format they prefer. Batch them; do not drip them.
- Every answer becomes a row in `docs/decisions.md` §2 (business rules). Every unanswered question goes to §3 with a **provisional assumption**, so nothing blocks.

## 2. Decide, and write it down as you go

Use `${CLAUDE_PLUGIN_ROOT}/templates/decisions.md`. Each decision: number, date, who decided, the decision first, short details, discarded alternatives with why.

Cover at least:

- **What is swappable and what is not.** Decouple only where change is likely (models, vendors, channels): one function type and one schema per piece, chosen by configuration, each with a mock. Everything else (database, framework, queue) is used directly. No layers "just in case".
- **Where the rules live.** Pick one guardian per kind of rule (for example: the database enforces domain invariants with constraints and triggers; the app translates its errors). Write it as a rule the lanes must follow.
- **Architecture:** processes, what each one does and may touch, and how they talk.
- **Data model** (if any): design it before the code, decision by decision, and test the schema on its own (a scratch database, a flows script). The schema files become the source of truth.
- **The contract** with consumers (API spec generated from schemas, events): who owns it and how it is distributed.
- **The local environment:** mocks by default for every external service; real services opt-in per worktree; integrations that allow one callback URL run one worktree at a time.
- **The method itself** (these become decisions too): how work is split, branch and worktree naming, squash merges, what "done" means, which review agents run when, the maximum number of parallel lanes.

When the owner is silent on a proposal, follow their standing rule (some owners use "silence means agreement"; record that rule itself as a decision).

## 3. Carve the work

- **Core (sequential):** the foundation every other brief stands on: skeleton, data, identity and API, the main input and output paths. Five or so briefs, one after another. Define a **core milestone** that works end to end with mocks.
- **Waves (parallel):** briefs that touch disjoint modules. Wave 1 is what makes the product useful; wave 2 is what makes it complete (privacy, statistics, tooling). Pure, isolated work (pure functions, a local lab) can start early: say so explicitly.
- **Collision points solved in advance:** per-module registries (routes, jobs, settings) with one line per module in a central file; timestamped migration names; generated artifacts (API spec) built in CI, not committed; append-only docs.
- Aim for briefs a session can finish in one sitting: one page of brief, one PR. Expect ~20 for a mid-size product.

## 4. Scaffold the repo

1. `CLAUDE.md` from the template, filled with the owner (language, attribution rule, architecture stance, stack, check command, setup command, reviewers).
2. `docs/decisions.md` (what you wrote), `docs/memory.md` (seeded: lanes empty, reserved numbers, owner to-dos from §3), `docs/briefs/INDEX.md` (core and waves), `docs/plans/_template.md`.
3. Data docs or design docs the briefs will cite.
4. The core briefs (skill `writing-briefs`). Wave briefs can wait until the core is near done: they will be better with the core's "What's left".

## 5. Exit criteria

- Every open question has an assumption; nothing blocks the core.
- The first core brief can be started with the standard prompt and its "Read first" list alone.
- **Test of sufficiency:** when the first lane runs, note every question it asks that was already decided somewhere. Each one is a hole in the docs: fix the doc, not just the answer.

Then switch to the `coordination` skill.
