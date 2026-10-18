# Tickets

Turns the agreed spec into one file per ticket at `.scratch/<slug>/tickets/NN-<slug>.md`, numbered from `01` with blockers first. Record the spec path in each ticket. Use one ticket when the spec fits one verifiable slice; ticket decomposition is the agent's work.

1. **Slice vertically.** Each ticket delivers one observable behavior through every layer it needs, can be verified on its own, and fits in one fresh context window. Assign each spec criterion one accountable ticket. Where it spans several slices, make its integrated check an explicit final ticket blocked by those slices.
2. **Prefactor when needed.** Add a `refactor` ticket only when evidence shows it makes the authorized outcome safer or simpler overall. State the preserved behavior and WHY; a speculative cleanup waits.
3. **Keep wide changes green.** A mechanical change that touches many call sites (a rename, a retyped shared symbol) becomes expand → migrate in batches → contract, one ticket each, so every ticket lands with passing checks.
4. **Draw only real blocking edges.** A ticket is blocked only when it can't start without another one. Fewer edges give a wider frontier.

```markdown
# NN: <title>

**Status:** ready
**Spec:** <path>
**Blocked by:** none | NN, NN
**Playbook:** feature | bug | refactor
**Owning module:** <module>

## Delivers
<the behavior this ticket makes work, from the user's side>

## Acceptance criteria
- [ ] <spec criterion number and text> → <check>

## Decisions
<pointers to the spec's WHY blocks this ticket implements; new ones found while working go here>

## Evidence
<filled when done: the Verification section from `verify`>
```

**Status** is `ready`, `in-progress`, `done`, or `blocked: <question or reason>`.

**Done when** every spec criterion has one accountable ticket, integration checks are assigned and every ticket's blockers have lower numbers. Continue with [implement](implement.md) when implementation is authorized; a request for tickets alone ends here.
