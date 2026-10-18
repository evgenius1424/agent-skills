---
name: verify
description: "Verification contract: choose checks before changing code, run them while working, and report only what actually ran. Use when planning acceptance criteria, before claiming work is done, or when a consequential invariant has no test."
---

# Verify

A claim of "done" is only as strong as the evidence behind it. An automated check (tests, type checks, lint, build) gives a deterministic pass/fail; an automated review gives an agent's judgement.

## Before changing anything

- State the **acceptance criteria** as observable behavior.
- Name the invariants the change could break.
- Find the repo's real check commands. In order: `CONTRIBUTING.md`, `CLAUDE.md`/`AGENTS.md`, the README dev section, CI config, then package or build scripts. CI is the source of truth when they disagree.
- Note which criteria the existing tests do not cover.

A **consequential invariant** with no test (see `why`) gets a focused test written before or alongside the change. That is how its WHY becomes executable. A gap that isn't consequential gets a test if it fits the scope. Otherwise report it as a gap.

## While changing

Work in small coherent units. Run the narrowest relevant check after each unit, before you stack more changes on top. Investigate a red check before dependent work. Compare it with the baseline: fix regressions introduced by the task; document unrelated pre-existing failures and continue independent work. Never count a failing or unavailable check as passing evidence.

## Evidence by task class

| Task | Minimum evidence |
|---|---|
| Trivial local edit | One focused test, type check or lint that exercises it |
| Behavior change | A test that fails without the change and passes with it, at the level the behavior lives (unit, integration or contract) |
| Security, authorization, transactions, concurrency, migration, public API | The above plus negative cases and an explicit compatibility check of old callers, data and clients |
| Refactor | Proof that behavior is preserved: existing tests green before and after, plus characterization tests where coverage is thin. Compiling is not enough. |
| Audit or investigation | Every claim reproducible: a file:line, a command and its output, or a commit |
| Docs or skills | Links resolve, triggers don't overlap, and one representative walkthrough |

## Before reporting

- Run the checks that cover the final integrated state. Reuse results only if the checked code and relevant environment have not changed; a worker's isolated green run does not prove integration.
- Read the task-owned diff against the outcome, preserving pre-existing user changes. Remove task-added changes outside scope or list them as proposals. Remove task-added debug code, dead code and comments that restate the code.
- Use the repo's `CONTRIBUTING.md` and other instruction docs as the review standard, alongside the acceptance criteria.

## Report

Put each item under exactly one verification label. Ran lists automated checks only.

```markdown
**Verification**
- Ran: `<command>` → <passed | failed: summary>
- Demonstrated: <behavior shown, and how: test name, output, screenshot>
- Justified: <architectural claims backed by a WHY block>
- Gaps: <criteria or invariants not covered, and why>
- Blocked: <checks that could not run, and what stopped them>
```

A command that did not run belongs under Blocked, never under Ran. A trivial change reports one line: `Ran: <command> → passed`.
