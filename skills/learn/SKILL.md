---
name: learn
description: "Turn a mistake or a wrongly-guessed WHY into a durable repo improvement by classifying its root cause and fixing the repo, not the prompt. Use after work that hit avoidable confusion, a correction from the user, a misleading example, or vocabulary drift."
---

# Learn

The repo is the prompt. When an agent reasons wrongly about a WHY, assume first that the repo misled it or left something out, and fix that.

When the human's WHY differs, state both interpretations and locate the evidence that produced the mismatch. Distinguish a correction of intent from a changed requirement or a factual disagreement. Current human intent governs the desired outcome; verify factual claims against the code and checks. Resolve any remaining product conflict with the human, then update the authoritative decision and any misleading examples. Acknowledging the correction in chat is not completion.

## Classify the root cause

| Bucket | Signal | Fix in the repo |
|---|---|---|
| 1. Missing information | The WHY or a term existed only in someone's head | A test, a better name or type, a one-line comment at the site, or a `GLOSSARY.md` term |
| 2. Misleading example | The agent copied a pattern that was wrong for this case | Correct or remove the example |
| 3. Missing boundary | Ownership was unclear, so behavior got spread around | Restructure into the owning deep module |
| 4. Genuinely ambiguous | The evidence supports both readings | Ask the user, and record the answer at the site (or an ADR per `why`) |
| 5. Reasoning error | The repo was adequate and the agent erred anyway | Nothing on the first occurrence. If it repeats, sharpen the skill text that should have prevented it. |

Buckets 1–4 fix the environment. Bucket 5 fixes the skill.

## Apply or propose

- **In scope and reversible**: apply it now and verify it like any other change.
- **Out of scope**: list it under "Repo improvements → proposed" with its bucket, the evidence, and the smallest change. Leave the code as it is.

Choose the smallest durable fix for the cause. Behavior and guarantees belong in types or focused tests; domain ambiguity belongs in names or `GLOSSARY.md`; rejected alternatives and historical intent belong in a comment, maintained spec or ADR under `why`. Verify that a future reader can recover the corrected WHY without this conversation. Read-only requests produce proposals, not edits.

## GLOSSARY.md

There is one `GLOSSARY.md` at the repo root. Create it when the first term is needed. Add a term when ambiguity caused, or plausibly could cause, a wrong WHY, or when a deep module is named after a concept the glossary doesn't have yet. Format:

```markdown
**Term**: one-line definition in domain language. _Avoid_: synonym, synonym.
```

Keep it to domain language: the words the request and its users use, for terms the code alone leaves unclear. Implementation details and framework terms stay in the code.

## Done when

Every confusion you hit during the work is either fixed in the repo, listed as proposed with its bucket, or classified as bucket 5 with no action.
