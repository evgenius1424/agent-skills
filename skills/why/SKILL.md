---
name: why
description: "Decision policy for consequential structure: interfaces, layers, boundaries, dependencies, generic mechanisms, config knobs, public contracts, and changes touching security, transactions, concurrency, migrations or compatibility. Use when adding, copying, keeping, or removing such structure; yields a WHY block and a verdict."
---

# WHY

Every consequential decision carries a WHY. A strong WHY rests on evidence. A decision that costs the same tomorrow waits until tomorrow.

## Consequential or not

A decision is **consequential** when it adds, removes or reshapes an interface, layer, module boundary, dependency, generic mechanism, config knob or public contract, or touches security, transactions, concurrency, migrations or compatibility. Decide everything else inline and move on.

## Gather evidence

Rank sources by how much they can settle, strongest first:

1. Current requirements and correctness constraints.
2. Observed behavior, tests and external contracts.
3. Recorded decisions: ADRs, commit messages, linked issues.
4. Maintained canonical examples and repo instructions.
5. Existing patterns.
6. General practice.

Label each claim as **intent** (backed by history: an ADR, commit, issue or the author), **behavior** (observed in code, tests or runs), or **hypothesis**. Structure shows behavior; intent comes from history. Repetition shows a pattern; necessity needs its own evidence. An unknown WHY leaves necessity open, so removal still needs its own evidence.

## The WHY block

Answer every line. "Unknown" is a valid answer and usually leads to INVESTIGATE.

```markdown
**Decision:** <what structure, where>
- Problem now: <what fails or is missing today>
- Evidence: <file:line, test, run output, ADR>, labeled intent / behavior / hypothesis
- Preserves: <capability, invariant or guarantee this structure protects>
- Simpler alternative: <concrete option, and why it falls short or doesn't>
- If removed or deferred: <what breaks, for whom>
- Why now: <why this can't wait>, or the trigger for DEFER
- Would change my mind: <evidence that flips the verdict>
- Scores: strength <0-5> · timing <NOW|LATER|NEVER> · deferral cost <L|M|H> · change risk <L|M|H>
**Verdict:** <ADOPT|DEFER|REJECT|KEEP|REMOVE|INVESTIGATE>
```

## Scores

The four scores are independent. A strong WHY can still be LATER. A weak WHY with high change risk calls for INVESTIGATE before any removal.

- **Strength**: 5 required (correctness, security, data integrity, explicit requirement) · 4 demonstrated (a problem observed now) · 3 constrained (verified external contract or platform need) · 2 preferential (readability or consistency, nothing demonstrated) · 1 speculative (a future need) · 0 ceremonial (habit, unsupported convention).
- **Timing**: NOW, needed to finish the current requirement safely · LATER, plausible value and safe to postpone · NEVER, no current justification (new evidence can reopen it).
- **Deferral cost**: L, a local refactor later · M, real coordination later · H, a migration, an irreversible commitment, or compatibility fallout.
- **Change risk**: weigh callers, public contracts, storage/serialization, transactions, concurrency, authorization, lifecycle, operations and how strong verification is.

## Verdicts

| Verdict | Meaning |
|---|---|
| ADOPT | Build it now. Strength ≥3 and timing NOW. High deferral cost contributes evidence for NOW; it does not excuse a speculative WHY. |
| DEFER | Use the simplest thing now and name the trigger that reopens the decision ("second implementation", "second caller", "interface got shallow"). |
| REJECT | The proposed structure lacks a current WHY. |
| KEEP | Existing structure with a confirmed WHY. |
| REMOVE | The WHY is shown to be absent and removal safety is established through callers, contracts and tests. |
| INVESTIGATE | The WHY is unknown or the evidence contradicts itself. Gather history and tests before changing anything, and ask the user only if it stays ambiguous. |

## Defaults that follow

- Write concrete code first. An interface needs a current reason beyond DI, mocking or a naming convention. One implementation can still justify one when it enforces a real security, transaction, ownership, lifecycle or failure-isolation contract. Two implementations still need a reason for them to be interchangeable.
- Generalize only on actual variation or knowledge that is shown to be shared. Factories, registries, plugins, pipelines, config and shared utilities each need a current benefit. Judge shared meaning, not textual similarity.
- A layer earns its place by doing independent work. Simplification leaves less to understand; reflection, global state and opaque dispatch only hide the complexity.
- New behavior goes in the deep module that owns it. With no clear owner, compare extending the closest module with creating a cohesive owner. Choose the smallest design that hides the responsibility from callers; a new boundary needs current evidence. DEFER speculative separation with a named trigger.
- Leave behind an example worth copying. Ask: if the next agent copies this structure, will it make a justified, local change?

## Deep-module vocabulary

When `codebase-design` is installed, use its vocabulary. Otherwise:

- **Module**: anything with an interface and a body: a function, class, package or service.
- **Interface**: everything a caller must know to use it (types, invariants, errors, ordering), not just an `interface` keyword.
- **Deep module**: a lot of behavior behind a small interface. **Shallow**: the interface is about as complex as the body.
- **Seam**: a place where behavior can be swapped without editing callers. It needs a current reason to exist.
- **Deletion test**: if this module disappeared, where would each of its responsibilities and guarantees go? If the answer is "nowhere, the callers already do it", the module is shallow.

## Where a WHY lives

Each WHY lives at its decision site, where the next agent will find it, rather than in a central log. In order of preference:

1. **Structure or name**: a type, a module boundary, a name that says what it protects.
2. **Test**: one that fails when the invariant breaks.
3. **One-line comment** at the decision site, saying why rather than what.
4. **ADR**: only when the decision is consequential, cross-cutting and hard to reverse, or when it's a KEEP on a WHY that was previously unknown. Write it to `docs/adr/NNNN-slug.md`, or to the module's own `docs/adr/` when only that module is affected. Create the directory only when needed. The body is the WHY block plus its verdict.

Structure and tests express the guarantee, but may not explain why it matters or why an alternative was rejected. Preserve that missing rationale in a nearby comment or decision document and link to its evidence. Keep one authoritative account; specs and reports can link to it. On a later WHY question, distinguish the recorded intent from what the current code demonstrates and what remains a hypothesis.
