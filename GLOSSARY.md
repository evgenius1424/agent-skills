# Glossary

Terms used across these skills. The authoritative definitions live in the skill named in brackets.

## Borrowed terms

Used in their source meaning; the gloss is how these skills apply it.

- **Module / deep module**: anything with an interface and an implementation; a deep one hides a lot of behavior behind a small interface. Each responsibility has one owning module. [`codebase-design`] _Avoid_: drawer, area, part.
- **Seam**: a place where behavior can be altered without editing there: the location of an interface, with adapters behind it. [`codebase-design`]
- **Handoff**: moving context to a session that starts with zero context and has no return path. [dictionary](https://www.aihero.dev/ai-coding-dictionary/handoff)
- **Handoff artifact**: the document that carries a handoff, such as a delegation brief or a spec. [dictionary](https://www.aihero.dev/ai-coding-dictionary/handoff-artifact)
- **Subagent**: an agent spawned for one task in its own session, returning a single report. [dictionary](https://www.aihero.dev/ai-coding-dictionary/subagent)
- **Automated check**: a deterministic pass/fail run: tests, type checks, lint, build. [dictionary](https://www.aihero.dev/ai-coding-dictionary/automated-check)
- **Automated review**: an agent's judgement of another agent's work. [dictionary](https://www.aihero.dev/ai-coding-dictionary/automated-review)
- **AX** (agent experience): how well the environment lets an agent do good work: checks, architecture, free context. [dictionary](https://www.aihero.dev/ai-coding-dictionary/ax) _Avoid_: agent readiness.
- **Environment**: what the agent acts on and what persists between sessions; here, mostly the repo. [dictionary](https://www.aihero.dev/ai-coding-dictionary/environment)
- **Design concept**: what user and agent jointly understand is being built, developed by grilling. [dictionary](https://www.aihero.dev/ai-coding-dictionary/design-concept)
- **Grilling**: interviewing the user about unresolved product decisions, in rounds of independent questions with recommended answers. Dependent questions wait for earlier answers. [evgenius1424-mode]
- **Context pointer**: a mention that lets an agent load a document only when the task needs it; skill descriptions are context pointers. [dictionary](https://www.aihero.dev/ai-coding-dictionary/context-pointer)
- **Progressive disclosure**: loading only the context needed now, with context pointers to the rest. [dictionary](https://www.aihero.dev/ai-coding-dictionary/progressive-disclosure)

## Framework terms

**Consequential decision**: a decision that must go through a WHY block; the list lives in `why` [why]. _Avoid_: architectural, significant.
**Trivial change**: one module, no consequential decision, one check verifies it [evgenius1424-mode].
**WHY block**: the evidence record for a consequential decision, ending in a verdict [why]. _Avoid_: ADR (an ADR is where a WHY block may be stored).
**Verdict**: ADOPT, DEFER, REJECT, KEEP, REMOVE or INVESTIGATE [why].
**DEFER trigger**: the named event that reopens a deferred decision [why].
**Evidence label**: intent, behavior or hypothesis [why].
**Verification label**: Ran, Demonstrated, Justified, Gaps or Blocked in a verification report [verify]. _Avoid_: evidence class.
**Consequential invariant**: a guarantee a consequential decision protects; it needs a test [verify].
**Root-cause bucket**: one of the five classes `learn` sorts a mistake into [learn].
**Scout / Implementer / Reviewer / Verifier**: the delegation roles for exploration, independent implementation, review and verification. They run inline when delegation is unavailable or unnecessary [evgenius1424-mode].
**Spec**: the durable statement of agreed outcome, acceptance criteria and decisions, normally at `docs/specs/<slug>.md`; it links to WHYs at their decision sites after implementation [evgenius1424-mode].
**Ticket**: one vertical slice of a spec, with its blocking edges and status, at `.scratch/<slug>/tickets/` [evgenius1424-mode].
**Frontier**: the decisions (grilling) or tickets (implementation) whose prerequisites are all settled [evgenius1424-mode].
**Re-route**: moving from one playbook to another within a session, carrying the findings forward [evgenius1424-mode]. _Avoid_: handoff.
