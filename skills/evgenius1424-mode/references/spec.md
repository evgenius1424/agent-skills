# Spec

For planning, grilling, or a request whose outcome, scope or acceptance criteria are unclear. The chain is grill → written spec → [tickets](tickets.md) → [implement](implement.md). Planning alone ends with the spec. If the user requested implementation too, continue after the design is settled without ticket checkpoints.

## Grill

1. **Explore first.** Find the owning module, its tests, `GLOSSARY.md` and the ADRs in the area. Facts are yours to find. Only decisions go to the user.
2. **Map a design tree.** Each open decision branches into the decisions that depend on it. The **frontier** is every decision whose prerequisites are settled.
   Cover users and outcomes, domain terms, observable success and failure, scope, existing contracts, and consequential constraints. Consider security, data changes, rollout and recovery only when the feature touches them. Separate product decisions from facts to investigate and reversible implementation details the agent can settle.
3. **Ask the whole frontier in one round.** Number each question and give your recommended answer with a one-line WHY. Wait for the answers, then recompute the frontier. A question that depends on one still open in this round waits for a later round.
4. **Give every consequential decision a verdict** (`why`). DEFER with a trigger is a good answer for anything that can wait.
5. **Challenge fuzzy terms** against `GLOSSARY.md`. When a term gets settled, record it per `learn`.
6. **Settle the design.** Write the concrete spec below and resolve material product decisions with the user before dependent implementation. If the user has confirmed the design and requested implementation, write the spec file at `docs/specs/<slug>.md` (or the repo's convention) and continue directly to [tickets](tickets.md) without stopping for confirmation — the spec file is the deliverable; the user's confirmation is about its content, not whether to write it. Otherwise present the spec for confirmation once, with any outstanding decisions explicit. Design approval alone is not permission to implement, commit or publish; preserve the scope already requested. Routine implementation choices remain the agent's work.

## Write the spec

Use the repo's spec convention or `docs/specs/<slug>.md`. Keep the spec versionable so a future session can recover intent. Honor an existing or user-specified path, including a temporary spec; preserve its durable rationale during implementation. Ticket progress lives separately in `.scratch/<slug>/tickets/`. Add that scratch directory to `.gitignore` only when created and not already ignored.

```markdown
# <Feature>

**Status:** draft | agreed | implemented | superseded
**Outcome:** what observably changes, from the user's side.
**Owning module:** <module>; each other module touched, with its one-line reason.

## Acceptance criteria
1. <observable behavior> → <check that proves it>

## Constraints and failure behavior
<relevant compatibility, errors, security, data or operational requirements; omit irrelevant categories>

## Open decisions
<unresolved product questions and blocked criteria; empty before dependent implementation>

## Decisions
<one WHY block with its verdict per consequential decision>

## Deferred
- <decision>: DEFER until <trigger>

## Test seams
<the highest existing seam each criterion is checked at; a new seam needs a WHY block>

## Out of scope
- <what this deliberately leaves alone>
```

Use `GLOSSARY.md` terms and name responsible modules. Link evidence and decision documents where needed. Keep implementation mechanics in tickets. For deployment or migration work, include rollout checks and rollback or recovery criteria.

**Done when** the written spec captures the settled design, every consequential decision has a verdict or a DEFER trigger, and acceptance criteria are verifiable. If implementation is authorized and the design is agreed, continue with [tickets](tickets.md). Otherwise deliver the spec and clearly label any unresolved decisions.
