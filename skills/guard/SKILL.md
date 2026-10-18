---
name: guard
description: "Architecture review of a bounded diff: flags unjustified new structure, unsafe removals, and patterns future agents would copy. Use when reviewing a branch, PR or working-tree changes for architecture, or as the reviewer pass on consequential work."
---

# Guard

Review only the decisions this diff introduces, changes or removes. Legacy code outside the diff is out of scope unless the diff copies a pattern from it.

Run in fresh context when possible, as the Reviewer role ([delegate](../evgenius1424-mode/references/delegate.md)). Otherwise do a separate inline pass that rereads the diff cold.

## Pass

1. Get the diff against its base and read the stated outcome (PR body, ticket or request).
2. List every consequential decision in the diff, as `why` defines it. Check each one: does a WHY block exist, does its evidence hold up when you open the cited files, and is the verdict consistent with its scores?
3. Flag:
   - **Unjustified addition**: an interface, layer, config or generic mechanism with strength ≤2 or timing LATER.
   - **Unsafe removal**: structure deleted with no evidence that its guarantee is kept elsewhere.
   - **Scatter**: behavior placed outside its owning deep module without a one-line reason.
   - **Copied pattern**: something likely to be copied that teaches a wrong pattern.
   - **Convention break**: a deviation without a WHY.
4. Where `code-review` is installed, it covers correctness and the spec. Otherwise the Reviewer also checks the diff against acceptance criteria, error paths, callers and relevant compatibility constraints. Guard is the architecture lens; a full review always includes correctness, with or without optional skills.

## Findings

One per issue, most severe first:

```markdown
- [<unjustified|unsafe-removal|scatter|copied-pattern|convention>] <file:line>: <what> — evidence: <…> — suggest: <smallest fix or the missing evidence>
```

If nothing is wrong, say so in one line. Report only findings with evidence.

**Done when** every consequential decision in the diff has been checked against its WHY block, and each finding cites file:line evidence.
