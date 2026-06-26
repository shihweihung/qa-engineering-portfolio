# CI/CD Integration

Making tests a meaningful part of the delivery pipeline.

Tests that only run locally do not protect the team. Tests that run in CI but take 40 minutes block delivery. The goal is fast, reliable feedback on every commit — which requires deliberate pipeline design, not just adding test commands to a YAML file.

## Articles

- **[Test Pipeline Design](pipeline-design.md)** — Structuring CI stages to give fast signal without sacrificing coverage
- **[Parallel Execution](parallel-execution.md)** — Reducing test suite runtime without breaking test isolation
- **[Flaky Test Management](flaky-tests.md)** — Diagnosing, quarantining, and eliminating non-deterministic tests
- **[Quality Gates](quality-gates.md)** — Defining and enforcing the conditions that must pass before a build can proceed
