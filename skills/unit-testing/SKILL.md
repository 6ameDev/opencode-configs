---
name: unit-testing
description: Write fast, deterministic, behavior-focused unit and component tests across backend, web, and mobile codebases. Use when creating, refactoring, or reviewing unit tests, test suites, test doubles, mocks, stubs, parameterized test tables, or ephemeral database test setups.
---
# Unit Testing

A stack-agnostic guide for writing fast, deterministic, behavior-focused unit and component tests that survive refactoring and avoid brittle test doubles.

## Core Principles

1. **Test Observable Behavior, Not Implementation**
   - Anchor tests to public contracts, return values, state transitions, and visible side effects so internal refactors do not break tests.
   - Target one cohesive behavior per test case, using one or multiple assertions as needed to verify that outcome.

2. **Speed and Determinism First**
   - Keep pure logic tests executing in milliseconds.
   - Inject clocks, random seeds, and environment boundaries instead of relying on wall-clock time, network latency, global state, or execution order.

3. **Prefer Parameterized / Table-Driven Tests**
   - Express input-to-outcome matrices using the language's idiomatic table-driven or parameterized test pattern rather than duplicating test functions.
   - Cover named happy paths, boundary thresholds, null/empty inputs, and failure modes in one structure.

4. **Be Intentional with Test Doubles and Boundaries**
   - **Stubs** supply controlled inputs or canned responses so code under test reaches specific paths.
   - **Mocks / Spies** verify outward interactions only when the interaction itself *is* the observable side effect (e.g., publishing an event, calling an external gateway).
   - **External Boundaries:** Isolate third-party APIs, network services, and hardware/OS interfaces you do not own behind test doubles.
   - **Owned Persistence:** Avoid mocking your own database queries or ORM layers when lightweight ephemeral test instances (containerized DBs, in-memory engines, isolated temp storage) can validate real queries, constraints, and transactions rapidly.

## Workflow

1. **Check Project Tooling, Not Legacy Habits**
   - Inspect the repo's test runner, directory layout, and existing setup so tests run cleanly with project tooling, but do not copy legacy anti-patterns (like heavy over-mocking or brittle implementation tests) if existing tests are sparse or poorly structured.
2. **Identify the Behavioral Seam**
   - Select the unit of behavior (pure logic, UI state/rendering, state transition, or persistence boundary) and the lightest isolation mechanism that preserves real confidence.
3. **Map the Scenario Matrix**
   - Outline happy paths, boundary cases, invalid inputs, and error recovery paths, grouping variations into parameterized tables where appropriate.
4. **Keep Setup Explicit and Minimal**
   - Populate only the fields relevant to the scenario under test; extract boilerplate into focused builders so the link between input and assertion stays obvious.
5. **Verify Execution**
   - Run the targeted test suite to confirm deterministic passes, meaningful failure signals, and zero shared mutable state across runs.

## Anti-Patterns to Avoid

- **Mirroring Production Logic:** Re-implementing the algorithm in test assertions instead of asserting concrete expected outcomes.
- **Over-Mocking Owned Code:** Mocking internal classes or repositories just for isolation, leaving real SQL queries, constraints, or contracts untested.
- **Asserting Internal Call Sequences:** Verifying exact internal helper call orders instead of resulting state or output.
- **Flaky Waits and Ambient State:** Using arbitrary sleep timers, shared singletons, or unisolated environment state.
