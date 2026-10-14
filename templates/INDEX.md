# Roadmap

<!--
lanes roadmap template. Lives at docs/briefs/INDEX.md. It answers one question: what is the state of every brief.
Everything else (lane notes, carry-overs, gotchas, owner to-dos) lives in docs/memory.md.
A brief becomes `done` inside its own PR, so `main` always tells the truth.
-->

States: `pending` · `done` (with PR link) · *no brief yet*.

**Ordering rules:**
- **The core runs in sequence**, one brief after another: it is what every later brief stands on.
- **Waves run in parallel lanes** once the core is `done`. Up to {{MAX_LANES}} sessions at a time.
- Exceptions (pure functions, isolated tooling) are named here explicitly.

## Core (sequential)

| Brief | Branch | Depends on | Status |
|---|---|---|---|
| [C1 <Title>](C1-<slug>.md) | `core/c1-<slug>` | — | pending |

**Core milestone:** <what works end to end when the core is done, e.g. "users can operate the inbox by hand, without the bot, with mocks">.

## Wave 1 (parallel, after the core)

| Brief | Branch | Depends on | Status |
|---|---|---|---|
| [A1 <Title>](A1-<slug>.md) | `<module>/a1-<slug>` | C3 | pending |

## Wave 2

| Brief | Branch | Depends on | Status |
|---|---|---|---|
| <ID> <Title> | `<module>/<id>-<slug>` | <ids> | *no brief yet* |
