# Refactor

Use for requested simplification or the smallest restructuring needed to complete an authorized feature, bug fix or spec. Explain why that restructuring is necessary and preserve unrelated behavior. Broader cleanup is a proposal. An answer-only or audit-only request remains read-only.

1. **Baseline.** Run the repo's checks **before touching any code** and record the output verbatim. Write characterization tests wherever a behavior you will touch is uncovered (`verify`). Every check that is green here must still be green at the end.
2. **Inventory the target.** Write a WHY block for each structure in scope. Act only on REMOVE, or on a simplification that keeps every guarantee. INVESTIGATE items stay as they are.
3. **Preserve contracts.** Public APIs, serialized formats, storage, error semantics and timing stay identical unless the user approved a change. Keep cleanup and behavior changes in separate batches.
4. **Batch.** One coherent change per batch, verified before the next. Commit per batch when commits are authorized.
5. **Deepen.** Prefer moving behavior into its owning deep module over adding a coordinating layer. Fix any canonical example the refactor makes misleading.

**Done when** the baseline checks and the characterization tests are green, every removed structure cites the evidence that removing it is safe, and the diff stays inside the stated scope.
