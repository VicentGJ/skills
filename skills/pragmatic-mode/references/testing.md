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

## Test the completed operation

Test through the public entry point and follow the operation to its meaningful
conclusion. Assert the externally visible result or the final persisted
business outcome. A purchase test places the order, confirms payment, processes
fulfillment, and checks that the completed transaction records the right items
and recipient. An order-creation response alone does not prove the purchase
works.

Mock external systems at their real boundaries. Keep routing, validation,
domain behavior, and persistence real wherever practical. Never mock the
behavior being verified.

## Consolidate around outcomes

- Before adding a test, read the existing tests for the operation. Adapt an
  existing scenario or fixture when it can prove the change.
- Touching several layers does not justify a test per layer. One
  completed-operation test usually proves what a request, schema, module, and
  persistence test would each repeat.
- Add a separate test only for a materially different business outcome or
  execution path, and name that difference. "Extra coverage" or "preventing
  regressions" is not a reason on its own.

## Keep scenarios focused

- Use the smallest realistic fixture that makes the behavior observable. Add
  variation only when it changes the outcome. Two records with the same display
  name help when testing selection by identity. Unrelated accounts, quantities,
  retries, and options do not.
- Assert what proves success. Assert an intermediate step only when it is an
  external effect the final outcome cannot show, such as the message sent to an
  external service.
- Never add data providers or test matrices by default. Each case must expose a
  distinction the existing scenario does not.

## Match verification to the change

- A data-type change does not need a new suite of boundary and migration tests.
  Update fixtures and expectations, then show through the business flow that
  the value survives the operation.
- Write dedicated migration tests only for real transformations, backfills,
  reconciliation, or data-loss risk, not for straightforward column changes.
- Run the narrowest relevant checks. Broaden only when failures or integration
  risk justify it.

## Test real contracts and failure modes

- Find out who controls the callers and read their implementations or
  documented contracts before inventing input scenarios or defensive
  requirements.
- Do not add malformed-input matrices for hypothetical clients, or production
  guards that exist only to satisfy such tests.
- Test error cases that are real business rules or consequential failures:
  payment failure, wrong ownership, duplicate processing.

## Before finishing

For each added test, state the completed outcome it proves and why existing
coverage does not already prove it. Remove overlapping assertions and
scenarios. Optimize for clarity and maintenance, not test count or line count.
Shortening a test by removing its meaningful conclusion is not simplification.
