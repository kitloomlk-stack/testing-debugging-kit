# flaky-test

Diagnose and stabilise an intermittently failing test.

# flaky-test

When invoked with the name or path of an intermittently failing test:

1. Run the test repeatedly (for example 20 to 50 times, using the runner's repeat option or a simple loop) alone, then together with its file and the full suite. Record the pass rate and the failure messages for each case.
2. Compare failing and passing runs. Look for the usual causes: shared or leaked state between tests, test order, real time or randomness, unawaited promises, fixed sleeps, network or filesystem dependence, port or file collisions, and parallel workers touching the same data.
3. Form a hypothesis and test it by changing one variable (run in isolation, fix the clock, serialise the workers).
4. Fix the cause: isolate the state, inject the clock or seed, await the real condition, or replace the sleep with a wait on an observable event. Do not add retries, longer timeouts or `skip` to hide the problem.
5. Re-run the repeated runs and confirm the failure rate is zero over a meaningful number of runs.

Report the cause, the fix, the before and after pass rates, and any related tests that share the same weakness.
