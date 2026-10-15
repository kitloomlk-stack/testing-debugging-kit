---
description: "Implement a described behaviour test-first, one red-green-refactor step at a time."
---

# tdd-cycle

When invoked with a description of a behaviour to build:

1. Restate the behaviour as a short list of concrete examples (inputs and expected outputs). Ask one clarifying question if something essential is ambiguous.
2. Find the project's test command and the nearest existing tests, and follow their style. Run the suite once to record the baseline.
3. Pick the simplest example. Write one failing test for it. Run it and show that it fails for the expected reason.
4. Write the least code that passes. Run the test.
5. Refactor if there is duplication or unclear naming, keeping the tests green.
6. Repeat from step 3 for the next example, adding edge cases (empty, boundary, invalid input) as you go.
7. Finish by running the full relevant suite and the linter or type checker the project uses.

Report the examples covered, the tests added, the commands you ran and their real results, and anything left untested.
