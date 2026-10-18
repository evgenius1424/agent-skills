# Delegate

Subagents are an execution technique: the main agent owns intent, scope, decisions, integration and the "done" claim.

| Subagent role | Use when |
|---|---|
| **Scout** | Answering one named question ("who owns X?", "what calls Y?") would mean reading many files you won't need afterwards |
| **Implementer** | An independent ticket can be built and checked in an isolated worktree while the main agent or another worker progresses |
| **Reviewer** | Consequential or multi-module work needs an automated review of its WHY blocks in fresh context. `guard` runs as this role. |
| **Verifier** | Consequential or multi-module work needs acceptance criteria checked against the diff, the repo's own check commands, and what actually ran |

A delegation brief is a **handoff artifact**: judge it by what a session with zero context could do with it. It states: the narrow question or deliverable, the relevant files and constraints, the read/write boundary, and the expected return, which is findings with evidence and open uncertainty, not a transcript. Concurrent edits need isolated worktrees; without them, write from one agent only. Trivial or sequential work stays with the main agent.

A Reviewer's or Verifier's judgement is an automated review, not an automated check ([`verify`](../../verify/SKILL.md)). If subagents are unavailable or not worth the cost, run the same role inline as a separate pass. Reread the diff as that role, with its brief.

An Implementer returns its change or commit, checks actually run, decision evidence and unresolved issues. It does not mark shared tickets done or change product scope. Integration and verification in the combined tree remain the main agent's responsibility. Use fresh reviewers when available; do not treat a worker's self-review as independent evidence.
