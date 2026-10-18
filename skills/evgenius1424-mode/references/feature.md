# Feature

1. **Find the owning module.** Locate the deep module that owns the behavior, along with its tests and the nearest canonical example. With no clear owner, compare boundaries using `why`.
2. **Set the bar.** Write the acceptance criteria and pick the checks (`verify`). If a consequential invariant has no test, that test is part of the work.
3. **Decide.** Each consequential decision gets a WHY block. The default is concrete code inside the owning module: an interface waits for a second implementation or a contract `why` names, and config waits for a second variant.
4. **Build in units.** Write a failing test first, make it pass, and run the repo's check command after each unit. Running the check is required; skipping it for a behavior change is not permitted.
5. **Review.** For consequential or multi-module work, run `guard` and the verifier role ([delegate](delegate.md)).
6. **Close.** Run `verify`'s pre-report steps and `learn`, then report using the full verification template — not the trivial one-liner.

**Second implementation arriving?** That's actual variation, and it reopens a deferred interface. Check whether a caller actually needs interchangeability. Extract only the shared contract that current callers need, with a WHY; two unrelated implementations can remain concrete.

**Cross-module change?** Name the question that each extra module answers. Change each module through its interface. A change to a contract between modules is consequential.

**Done when** every acceptance criterion sits under Ran or Demonstrated (`verify`), every consequential decision has a WHY block with a verdict, and the diff stays inside the owning module or each extra module has its one-line reason.
