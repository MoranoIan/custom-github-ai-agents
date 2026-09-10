---
name: test-planning
description: 'Turn a change request, PR description, or bug report into a concrete test strategy — unit, integration, edge cases, and regression risk. Use when planning tests for a new feature, bug fix, or refactor, or when asked "what should I test for this change".'
---

# Test Planning

Use this skill when someone describes a change (a feature, bug fix, or refactor) and needs a concrete plan for what to test — not just "write some tests."

## Process

1. **Identify what actually changed.** Read the diff or description and separate:
   - New behavior (needs new tests)
   - Modified behavior (existing tests may need updating)
   - Unchanged code that sits on the same path (needs regression coverage, not new tests)

2. **Classify the change** as one of:
   - New feature
   - Bug fix
   - Refactor (behavior should be unchanged)
   - Config/infra change

   The classification changes the test strategy: a bug fix needs a test that reproduces the original bug and fails without the fix; a refactor needs tests that pin down *current* behavior before the change, not new behavior.

3. **Build the test plan across these layers, only where relevant:**
   - **Unit** — the smallest testable unit touched by the change. List specific inputs, including boundary values (empty, zero, max, null/None, malformed).
   - **Integration** — how this unit interacts with the rest of the system (database, API, other services). Only include this layer if the change crosses a boundary.
   - **Edge cases** — inputs or states that are easy to miss: concurrent access, partial failure, retries, timeouts, empty collections, duplicate entries.
   - **Regression risk** — existing functionality that could break because it shares code, state, or a dependency with the change. Name the specific existing tests or areas to re-run, don't just say "run the full suite."

4. **Flag what can't be easily tested** (e.g., timing-dependent behavior, third-party service responses) and suggest a mitigation: a mock, a fixture, or a manual verification step.

## Output format

Give the plan as a short structured list per layer, not prose paragraphs. For each test case, state: the input/scenario, the expected outcome, and why it matters (what it would catch). Skip layers that don't apply — don't pad the plan to look thorough.

## Boundaries

- This skill plans tests; it doesn't replace judgment about how much coverage a given change actually warrants. A one-line config change doesn't need the same treatment as a new payment flow — scale the plan to the risk.
- Don't invent test cases for code you haven't seen. If the change description is too vague to plan against, ask for the diff or more detail rather than guessing.