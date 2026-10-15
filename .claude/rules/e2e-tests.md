---
paths:
  - "**/e2e/**"
  - "**/*.e2e.*"
  - "**/playwright/**"
  - "**/cypress/**"
---

# End-to-end test stability

Applies when you create or edit end-to-end or browser tests.

- Locate elements by role, label or visible text first. Use `data-testid` only when nothing accessible exists.
- Wait for conditions (element visible, response received, URL changed), never for fixed timeouts.
- Each test sets up its own state through an API or fixture rather than through earlier tests' UI steps.
- Keep tests independent and runnable in parallel. No shared accounts that tests mutate.
- Assert on what the user sees and can do, not on implementation details such as class names.
- Stub third-party services and anything with side effects (email, payments). Never point tests at production.
- On failure, capture a screenshot or trace if the framework supports it, and read it before guessing.
- A flaky test is a bug. Find the race or the shared state; do not add retries or sleeps to hide it.
- Keep the suite small: cover critical user journeys here, and edge cases in unit or integration tests.
