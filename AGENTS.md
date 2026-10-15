# Testing & Debugging Kit

This setup makes the agent work like a careful engineer when code is wrong or unproven. New
behaviour starts with a failing test. Failures are explained with evidence before they are
fixed. Tests are written to catch real regressions, not to inflate a coverage number. Claims
such as "fixed" or "passing" are only made after the relevant command has been run and its
output read.

## Working agreement

- Run the project's own test command before changing anything, so you know the baseline. Find it
  in the manifest (`package.json` scripts, `pyproject.toml`, `Makefile`, `go.mod`) or the README;
  do not guess a command and report its result as if it were the project's.
- If tests were already failing before you started, say so, and do not count those failures as
  yours or silently "fix" them as a side effect.
- Keep changes small. One behaviour per test, one cause per fix, one concern per commit.
- Do not delete, skip, `xit`, `.skip` or loosen an assertion to make a test pass. If a test is
  wrong, say why and change it in a separate, explained step.
- Ask before running anything slow, destructive, or against a shared environment (a staging
  database, a paid API, a deployed URL). Prefer local fixtures and fakes.
- Do not push, deploy, or install global tooling without being asked.

## Test-driven development

1. Write one failing test that describes the next small behaviour. Run it. Confirm it fails for
   the reason you expect (an assertion, not a typo or an import error).
2. Write the least code that makes it pass. Run it again.
3. Refactor with the tests green. Run the full relevant suite, not just the new test.
4. Repeat. Commit when a coherent slice is green.

For a bug report, the first step is a test that reproduces the bug. It must fail before the fix
and pass after. If you cannot write such a test, you do not yet understand the bug.

## What a good test looks like

- Name it for the behaviour: `rejects_expired_token`, not `test1` or `testAuth`.
- Arrange, act, assert, in that order, with one reason to fail.
- Assert on outcomes the caller can observe (return values, persisted state, emitted events,
  rendered text), not on private helpers or call counts, unless the call itself is the contract.
- Test boundaries: empty, one, many, maximum, invalid type, duplicate, concurrent, time zone,
  locale, encoding.
- Mock only what you must: the network, the clock, randomness, the filesystem when slow. Never
  mock the unit under test. A test whose mocks return the answer it asserts proves nothing.
- No shared mutable state between tests. Each test creates and cleans up its own data and can run
  alone or in any order.
- Deterministic by construction: inject time and randomness, never use `sleep` to wait for
  something that can be awaited.
- Snapshot tests only for small, reviewed output. Never accept a snapshot update without reading
  the diff.

## Debugging protocol

Do not edit code to "see if that helps". Work in this order and write down what you learn.

1. **Reproduce.** Get a failing command, test or input. Record the exact error, stack trace and
   environment. If it is intermittent, find what varies (ordering, timing, data, machine).
2. **Isolate.** Shrink the input and the code path until the failure is minimal. Use
   `git bisect` or a manual binary search over changes when something "worked yesterday".
3. **Hypothesise.** List two or three candidate causes. For each, state what you would observe
   if it were true and how to check it cheaply.
4. **Gather evidence.** Add targeted logging or a debugger breakpoint, read the real values,
   and rule hypotheses out. Remove temporary instrumentation afterwards.
5. **Fix the cause.** Change the code that is wrong, not the code that notices. If the fix
   needs more than one hypothesis to be true, you have not found the cause.
6. **Prove it.** The reproducing test now passes, the surrounding suite still passes, and you
   have said what you ran.
7. **Ask why it was possible.** If the same class of bug could occur elsewhere, say so and
   propose a guard (a type, a lint rule, a test), but do not widen the change unasked.

Stop and report instead of guessing when three consecutive fixes have not worked; the model of
the problem is probably wrong.

## Browser testing

- Verify UI changes in a real browser, not by reading code. Check the console for errors and
  warnings, the network panel for failed or unexpected requests, and the layout at a mobile
  width and a desktop width.
- Prefer role- and label-based locators (`getByRole`, `getByLabel`, `getByText`) over CSS or XPath.
  Add a `data-testid` only when no accessible locator exists.
- Wait on conditions (an element visible, a response received), never on fixed delays.
- Keep end-to-end tests few and valuable: sign-in, the main purchase or publish path, anything
  where a regression is expensive. Push detail down to unit and integration tests.

## Before you finish

- The reproducing or new test fails without your change and passes with it.
- The wider suite and the type checker or linter the project uses have been run, and you have
  reported their actual results.
- No leftover `console.log`, `debugger`, `.only`, `.skip` or commented-out code.
- The summary says what was wrong, why, what changed, and what you did not verify.

## Skills in this kit

- `tdd` — build a feature or fix a bug test-first with red-green-refactor.
- `diagnosing-bugs` — a hard bug or performance regression with an unknown cause.
- `debugging-and-error-recovery` — a failing test, broken build or unexpected error.
- `parallel-debugging` — several plausible causes; test competing hypotheses against evidence.
- `five-whys` — a recurring problem where you need the root cause, not a patch.
- `e2e-testing-patterns` — writing or stabilising Playwright or Cypress tests.
- `browser-testing-with-devtools` — inspecting the DOM, console, network and performance in a real browser.
- `kiro-verify-completion` — before claiming work is done, back the claim with fresh evidence.

## Commands

- `/tdd-cycle` — implement a described behaviour test-first.
- `/debug` — trace a failure to its root cause and fix it with a regression test.
- `/flaky-test` — diagnose and stabilise an intermittently failing test.

## Sub-agents

- `bug-investigator` — reproduces a failure and traces it to a root cause; reports, does not edit.
- `test-reviewer` — reviews tests for gaps, brittleness and weak assertions; reports, does not edit.

## Scoped rules

Agents that support scoped rules load these automatically. If yours does not, read the matching file before editing files it covers:

- `.agents/rules/test-files.md` — for `**/*.test.*`, `**/*.spec.*`, `**/__tests__/**`, `**/tests/**`, `**/test_*.py`, `**/*_test.go`: Conventions for writing and editing test files.
- `.agents/rules/e2e-tests.md` — for `**/e2e/**`, `**/*.e2e.*`, `**/playwright/**`, `**/cypress/**`: Stability rules for end-to-end and browser tests.
- `.agents/rules/debugging-discipline.md` — always: Always-on rule: find the root cause with evidence before changing code.
