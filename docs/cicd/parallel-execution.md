# Parallel Test Execution

## Problem

A test suite that runs sequentially for 30 minutes blocks the delivery pipeline for 30 minutes on every run. As the suite grows, this cost compounds. Parallel execution reduces wall-clock time without reducing coverage — but introduces test isolation requirements that sequential execution hides.

## Solution

`pytest-xdist` distributes tests across multiple workers. Each worker runs a subset of tests in its own process, and results are collected at the end.

```bash
# Run tests across 4 workers
pytest -n 4

# Use all available CPUs
pytest -n auto
```

**Ensure test isolation before enabling parallelism.**

Tests that share state across processes will fail non-deterministically under parallel execution. Common violations:

- Tests that write to the same database rows without transaction isolation
- Tests that use hardcoded file paths that multiple workers try to access simultaneously
- Tests that depend on execution order from a previous test's side effects

**Use scoped fixtures to share expensive setup within a worker.**

Session-scoped fixtures initialize once per worker process, not once per test run. For setup that is safe to share within a worker, this is the correct scope.

**Distribute tests by file, not by test.**

The default xdist distribution can create contention when tests in the same file share module-level state. `--dist=loadfile` assigns all tests in a file to the same worker, preventing cross-worker state conflicts.

```bash
pytest -n 4 --dist=loadfile
```

## Real-world example

A team enabled 4-worker parallelism and saw 40% of their tests fail intermittently. Investigation revealed tests that created users with fixed emails — two workers trying to create `test@example.com` simultaneously caused database conflicts.

Adding a unique suffix to generated test data (using `uuid4()`) eliminated the conflicts. Parallel execution then reduced the suite from 28 minutes to 8 minutes with no test failures.

## Key takeaways

- Parallel execution requires test isolation — shared state that works sequentially breaks under parallelism
- Fix isolation issues before enabling parallelism; debugging parallel failures is significantly harder
- `--dist=loadfile` prevents cross-worker conflicts for tests with module-level shared state
- Generate unique test data per test, not hardcoded identifiers that conflict under concurrency
- Start with 2 workers, verify results match serial runs, then scale up
