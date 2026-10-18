---
name: evgenius1424-mode
description: "evgenius1424's engineering mode: routes software work (planning and grilling into spec, tickets and implementation; feature, bug, investigation, refactor, audit, review, PR, agent docs) through evidence-backed decisions and executable verification. Use for /evgenius1424-mode, or when CLAUDE.md names it as the default mode."
---

# evgenius1424 mode

The codebase is a prompt. Every structure, name, example and test you leave behind teaches the next agent where to look and what to copy. So keep improving it: put behavior in **deep modules** (one module per responsibility), reduce uncertainty, add an abstraction only when it is necessary, and postpone every decision that can be postponed.

If an agent gets a WHY wrong, the fault lies with the repo or with missing information. Fix that cause with [`learn`](../learn/SKILL.md) instead of working around it.

Improve the repo where this task exposes a concrete misunderstanding or design problem. Minimal means the smallest coherent change that meets the outcome and leaves a clear owner, not the fewest changed lines. Deepen the affected module when evidence warrants it; propose unrelated improvements separately.

## 1. Frame the request

Read the request, the repo's instruction docs (`CLAUDE.md`/`AGENTS.md`, `CONTRIBUTING.md`, the README dev section) and the root `GLOSSARY.md` if one exists. Settle three things:

- **Outcome**: what observably changes when this is done.
- **Scope**: which module owns it.
- **Authorization**: implement, or only answer/design/audit? An audit or a design question stays read-only until the user authorizes implementation.

**Trivial** work skips the rest of this file: one module, no new observable behavior, no consequential decision (see [`why`](../why/SKILL.md)), one check verifies it. Typical examples: renaming a symbol, fixing a typo, updating a constant. Adding new behavior is not trivial even when the change is small. Make the change, run the narrowest executable check that exercises it (find the repo's check commands as `verify` does), and report in one line: what changed + `Ran: <command> → <result>`. A search or a reread is not a check. If any of those conditions stops being true partway through, escalate to the matching playbook and keep what you already found.

## 2. Route

Read only the branch you need. Combine branches when the request really needs both. Each branch ends on its own **Done when**.

| Request | Go to |
|---|---|
| Plan, grill, fuzzy, underspecified, or "help me think" | [spec](references/spec.md) → [tickets](references/tickets.md) → [implement](references/implement.md) |
| Implement an existing spec, wherever it lives | [implement](references/implement.md) |
| Add or change behavior | [feature](references/feature.md) |
| Broken, failing, slow, regressed | [bug](references/bug.md) |
| Explain, find a historical WHY, compare designs | [investigate](references/investigate.md) |
| Simplify or restructure existing code (authorized) | [refactor](references/refactor.md) |
| Assess a repo's architecture or AX (agent experience) | [`audit`](../audit/SKILL.md) |
| Review a diff's architectural decisions | [`guard`](../guard/SKILL.md) |
| Commit, PR, ship | [ship](references/ship.md) |
| Edit skills, `CLAUDE.md`, `AGENTS.md` | [skill-authoring](references/skill-authoring.md) |

**Re-route** with findings carried forward and the original authorization preserved. An investigation that finds a defect reports it; implement it when changes are authorized. A structural bug may need a scoped refactor. An uncovered consequential invariant goes to [`verify`](../verify/SKILL.md) for a test. The next playbook starts from the known owner, evidence and constraints.

## 3. Leave the owning module deliberately

Start at the requested behavior and its likely owner. Use symbol and reference search, the owner's tests, and the nearest canonical example. Before opening anything else (another module, git history, a repo-wide search), name the question it answers. Stop once the evidence is enough to make and verify the next decision.

When you leave the owning module, add one line to the report: "opened `billing/` because the refund contract lives there". `audit` is the exception: it sweeps systematically.

## 4. Decide with evidence

Any **consequential** decision, as [`why`](../why/SKILL.md) defines it, goes through `why`, which produces a WHY block and a verdict. A change that touches code outside the owning module needs a one-line reason. It needs a full WHY block only when an interface or boundary changes.

Consequential or multi-module work also gets a Reviewer and a Verifier pass, inline when subagents are unavailable. [delegate](references/delegate.md) defines those roles, the Scout for wide reads, and the delegation brief.

Existing convention wins by default. Breaking it is consequential. If the convention's own WHY is unknown, the verdict is INVESTIGATE before you deviate.

## 5. Verify by contract

For every non-trivial route, load [`verify`](../verify/SKILL.md) before the first edit: it sets the acceptance criteria, finds the repo's check commands, decides which uncovered invariants need a test, and defines the verification labels. Run checks while you work in small units, and report only checks that actually ran.

## 6. Ask only what is yours to ask

Ask the user about product or preference calls, irreversible or outward-facing actions, and WHYs that stay ambiguous after investigation. Find facts out yourself by reading or running something. Routine reversible work proceeds without checkpoints. Commit only when the user asks or authorized it for the session.

## 7. Report

For non-trivial work, run [`learn`](../learn/SKILL.md) over any confusion you hit before you report. One shape for every route. A trivial change gets one line plus the check that ran.

```markdown
**Outcome:** what changed or what was found.
**Decisions:** WHY blocks with verdicts, for consequential decisions only.
**Verification:** the verification labels Ran / Demonstrated / Justified / Gaps / Blocked, as `verify` defines them.
**Repo improvements:** applied / proposed, each with its root-cause bucket (`learn`).
**Open uncertainty:** what is still unknown and what evidence would settle it.
```
