# Test Pipeline Design

## Problem

A test suite that takes 40 minutes to run is not useful for development feedback. Engineers stop waiting for results, start merging without green CI, and the pipeline becomes a compliance checkbox rather than a quality gate.

The solution is not to run fewer tests — it is to run the right tests at the right stage, with fast feedback for common cases and thorough coverage for higher-risk changes.

## Solution

Structure the pipeline in stages that trade completeness for speed as you move earlier in the cycle.

**Stage 1 — Fast feedback (under 3 minutes):**
Unit tests and static analysis. These run on every commit and block immediately if they fail. They should be fast enough that engineers wait for them before continuing.

**Stage 2 — Integration validation (under 10 minutes):**
API tests and component integration tests. These run on every PR and confirm that services interact correctly. They do not require a full deployment.

**Stage 3 — Regression (under 30 minutes):**
E2E and UI automation against a deployed environment. These run on merges to the main branch and on release candidates. Not every PR needs this.

**Stage 4 — Extended coverage (nightly):**
Full regression, device farm runs, performance benchmarks. These do not block development but surface issues that require attention before the next release.

```yaml
# Example GitHub Actions pipeline structure
jobs:
  unit-tests:
    runs-on: ubuntu-latest
    steps:
      - run: pytest tests/unit --timeout=30

  api-tests:
    needs: unit-tests
    runs-on: ubuntu-latest
    steps:
      - run: pytest tests/api --timeout=60

  e2e-tests:
    needs: api-tests
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - run: pytest tests/e2e --timeout=120
```

## Real-world example

A team had a single CI job that ran everything — unit tests, API tests, and E2E tests — on every commit. It took 35 minutes. Engineers were merging without waiting. Adding a fast unit test stage that ran first and returned results in 2 minutes gave engineers immediate feedback on their most likely errors. E2E coverage moved to post-merge.

## Key takeaways

- Design pipeline stages around feedback speed, not test type
- Fast feedback stages (under 3 minutes) must block developers; slow stages should not
- Not every PR needs full E2E coverage — scope expensive stages to merges and releases
- Nightly runs are appropriate for tests that are too slow or expensive to run continuously
- A pipeline that engineers bypass is not a quality gate; optimize for speed before coverage
