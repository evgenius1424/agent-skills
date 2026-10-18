# Bug

1. **Reproduce.** Get a reproduction loop that fails reliably, ideally a test, before you form any theory. Use `diagnosing-bugs` when it's installed. Otherwise bisect hypotheses one at a time, and change one variable per run.
2. **Evidence the cause.** Name the line or condition and show the run that proves it. A plausible story is not a cause.
3. **Fix at the cause.** Make the smallest change that turns the reproduction green. The test stays as a regression guard.
4. **Check neighbors.** Search for the same pattern elsewhere. Fix it where the scope allows, otherwise propose it under `learn`.
5. **Structural cause?** If the bug exists because a boundary is wrong or missing, ship the fix first, then re-route to `refactor`, or propose the refactor if it isn't authorized. Carry the reproduction and the evidence along.

If the user asked for a diagnosis only, stop after step 2 and report.

**Done when** the reproduction is green, `verify` passes, and the cause is cited with evidence.
