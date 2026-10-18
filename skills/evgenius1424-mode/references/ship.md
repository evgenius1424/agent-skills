# Ship

Carry out the requested delivery action: commit, push, PR, merge or deployment. Each action needs authorization from the request or session; preparing a PR does not authorize merging or deployment.

1. Run `verify`'s pre-report steps. Use `deslop` or `no-comments` when they're installed.
2. Write the commit message: what changed and why, in the repo's existing style.
3. Write the PR body with `pr` when it's installed. Otherwise use:

```markdown
## Summary
<smallest view: pseudocode, call tree, or diff sketch>

## Decisions
<WHY blocks with verdicts; omit when none are consequential>

## Evidence
<the Verification section from `verify`: Ran / Demonstrated / Gaps / Blocked>

## Merge danger
Door: <one-way | two-way> · Blast radius: <one word> · <ramifications if any>
```

Use domain terms from `GLOSSARY.md`.

For an authorized PR, inspect its checks and actionable review feedback when the request includes making it ready to merge. Fix task-related failures and rerun relevant verification. For deployment or data migration, establish the target, compatibility, rollout checks and recovery plan before acting; verify the resulting service or data state afterwards. If a required action is unavailable, report the exact blocker.

**Done when** the requested delivery action is complete and verified, with its commit, PR or deployment reference and truthful evidence. A draft PR or green local build alone does not prove deployment or production behavior.
