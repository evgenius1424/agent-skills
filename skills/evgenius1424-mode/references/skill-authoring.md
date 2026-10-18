# Skill authoring

For editing skills, `CLAUDE.md`, `AGENTS.md`, or any document an agent loads. Use `writing-for-agents` when it's installed. These rules hold either way:

- **Code beats prose.** Before adding an instruction, check whether a test, type, name or module boundary could carry it (`learn`, buckets 1–3).
- **One source of truth.** Each rule lives in exactly one skill, and the others link to it. The policy lives in `why`, the evidence contract in `verify`, and the routing here.
- **Descriptions are context pointers.** Front-load the leading word, write one trigger per distinct branch, and make sure no two skills claim the same branch.
- **Progressive disclosure.** Inline what every path needs. Push branch-specific material into `references/`.
- **State the positive.** Say the behavior you want rather than listing what's forbidden.
- **Prune.** Delete any sentence that doesn't change behavior compared with the model's default.

**Done when** every relative link resolves, routing has no ambiguous owners or recursive invocation loops, and one representative scenario walks through correctly. Cross-references may point back to shared policy; load it once and return to the active step. Report the walkthrough as a walkthrough, not as an executed eval.
