---
name: debug
description: "Investigate a failure to its root cause, then fix it with a regression test."
disable-model-invocation: true
---

# debug

When invoked with a bug report, error message or failing test:

1. Reproduce it. Run the failing command or test and capture the exact output. If you cannot reproduce it, say so and list what extra information you need.
2. Minimise: reduce the input and code path until the failure is as small as possible. If it used to work, bisect the history to find the change that introduced it.
3. List two or three candidate causes and how each could be confirmed or ruled out.
4. Gather evidence with targeted logging, a debugger, or reading the real values. Rule hypotheses out one at a time.
5. Write a test that reproduces the bug and fails for the right reason.
6. Make the smallest change that fixes the cause, not the symptom.
7. Run the new test, then the surrounding suite. Remove any temporary logging.

Report: the root cause in one or two sentences, the evidence for it, the fix, the commands run with their results, and whether the same mistake could occur elsewhere. If three attempts fail, stop and report instead of continuing to guess.
