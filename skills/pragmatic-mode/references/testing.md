# Testing

Tests must earn their maintenance cost by proving that a real user or business
operation works. Do not default to test-driven development.

## Which kind of check

- **Visual QA**: for checks during development, and required for final
  delivery. Drive the real app with browser use, or computer use when browser
  use is unavailable. Attach the captures to the chat.
- **E2E tests**: the only tests added as a permanent part of the test and
  deployment procedure. Keep the suite small and high-impact: the full
  automated suite must finish in three minutes. Each E2E run ends in a
  verifiable, repeatable artifact.
- **Integration tests**: only for a system that has no frontend to QA.
- **Unit tests**: never to validate code you wrote in this session. Use them
  only when:
  - unit tests already cover the code you changed. Keep them passing and adapt
    them to the new behavior;
  - the task is explicitly to write unit tests;
  - the developer explicitly asks for unit tests on existing code you did not
    write in this session;
  - the developer explicitly asks for tests up front as part of the design. Then
    write down every way the unit could fail first, then the tests, then the
    code.

## Writing a test

- Drive the operation through its public entry point to its conclusion. Assert
  the visible result or the final persisted outcome: a purchase test checks the
  completed transaction, not the order-creation response.
- Mock only external systems, at their real boundary. Never mock the behavior
  under test.
- Extend an existing scenario or fixture before adding a test. Add one only for
  a materially different outcome or path, never one per layer touched.
- Use the smallest fixture that makes the behavior observable and assert only
  what proves success. No matrices or data providers unless each case is a
  distinct outcome.
- Take inputs and error cases from the callers' real contracts and business
  rules (payment failure, wrong ownership, duplicate processing), not from
  hypothetical clients. Add no production guards just to satisfy a test.
- For a data-type change, update existing fixtures. Write a migration test only
  for a real transformation, backfill, or data-loss risk.
- Run the narrowest relevant checks. Broaden only when failures justify it.

## Before finishing

For each added test, name the completed outcome it proves that existing
coverage did not. Remove the rest.
