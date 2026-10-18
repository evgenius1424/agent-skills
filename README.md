# evgenius1424 skills

The codebase is a prompt. These skills make an agent keep improving it. Behavior goes into deep modules, uncertainty gets reduced, an abstraction waits until it's necessary, and any decision that can be postponed is postponed. When an agent gets a WHY wrong, the repo is fixed, not the prompt.

## Skills

| Skill | Role |
|---|---|
| `evgenius1424-mode` | Entry point. Routes by intent, sets exploration and delegation rules, and holds the playbooks (spec → tickets → implement, feature, bug, investigate, refactor, ship, skill-authoring). |
| `why` | Decision policy: WHY block, scores, verdicts, deep-module vocabulary, ADRs. |
| `verify` | Verification contract and report format. |
| `audit` | Read-only repo audit with ranked findings. |
| `guard` | Architecture review of a diff. |
| `learn` | Root-cause a mistake into a repo improvement; owns `GLOSSARY.md`. |

## Install

Claude Code plugin:

```sh
/plugin marketplace add evgenius1424/agent-skills
/plugin install evgenius1424@evgenius1424
```

Plain skills (any Agent Skills runtime):

```sh
npx skills add evgenius1424/agent-skills
```

To make it the default, add one line to `~/.claude/CLAUDE.md`:

```markdown
For software engineering work, use the `evgenius1424-mode` skill.
```

## Workflow

Ask: "Grill this idea and write a spec." The agent investigates facts, asks about unresolved product choices and writes a reviewable spec under `docs/specs/` or your repo's existing convention.

Then ask: "Implement this spec completely, using subagents where useful." The agent owns ticket decomposition, dependency ordering, implementation, integration and verification. It repairs implementation details without ticket approvals and asks only when the agreed outcome or authority needs to change. An already agreed spec can go straight to implementation. Commits and delivery follow your authorization.

Specs retain intent; temporary tickets track progress. WHY corrections update the smallest durable source, such as a test, domain term, comment or ADR. Minimal change means the smallest coherent solution, including necessary improvements to the affected module. Unrelated cleanup remains a proposal.

## Evals

`evals/` holds one case per operating scenario. Run them with `claude plugin eval .` See [evals/README.md](evals/README.md).

The [development workflow review](docs/reviews/2026-10-18-skills.md) records the coverage, corrected contradictions and validation gaps.

## Influences & optional dependencies

The skills reference these when they're installed and fall back to a few lines of their own when they're not. Nothing here is required.

- [Matt Pocock's skills](https://github.com/mattpocock/skills): `diagnosing-bugs`, `codebase-design`, `improve-codebase-architecture`, `code-review`, `pr`, `prototype`, `writing-for-agents`. The deep-module vocabulary and the GLOSSARY/ADR conventions come from here.
- Poteto's pstack: `deslop`, `no-comments`. The ideas of verified units, deliberate subagents and fixing the root cause come from here.
- Humanlayer's `show-me`: small visual explanations.
