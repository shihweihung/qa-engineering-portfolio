# Flaky Test Management

## Problem

A flaky test is a test that fails intermittently without a change in the code under test. It creates noise that erodes trust in the test suite. Engineers learn to re-run failures instead of investigating them. Genuine failures get dismissed as "probably flaky." The suite becomes unreliable as a quality signal.

Flakiness is not a minor inconvenience. A test suite with 5% flakiness rate means that a 200-test suite will have 10 random failures on any given run. That is enough noise to make the pipeline meaningless.

## Solution

Flaky test management requires three things: detection, quarantine, and elimination.

**Detection: make flakiness visible.**

A test that fails once in ten runs is flaky. A test that fails once in a hundred runs is also flaky. Without tracking failure rates, both look like rare legitimate failures.

Track each test's pass/fail history in CI. Flag tests with a failure rate above a threshold (e.g., more than 2 failures in 20 runs with no code change) as flaky candidates for review.

**Quarantine: isolate flaky tests immediately.**

A flaky test in the main suite contaminates results. Move confirmed flaky tests to a quarantine suite that runs separately, does not block CI, and is reviewed weekly.

```bash
# Mark a test as quarantined
@pytest.mark.quarantine
def test_intermittently_failing_scenario():
    ...

# CI pipeline: run main suite only
pytest -m "not quarantine"

# Weekly review: run quarantine suite separately
pytest -m quarantine
```

**Elimination: fix the root cause, not the symptom.**

Common flakiness root causes:
- Timing dependencies (fixed by auto-waiting or explicit waits)
- Shared state between tests (fixed by improved isolation)
- External service dependencies (fixed by mocking or retrying)
- Race conditions in async code (fixed by proper synchronization)

Retry decorators suppress flakiness without fixing it. Use them only as a last resort for known external instability outside the team's control.

## Real-world example

A team had 18 flaky tests in a 150-test E2E suite. The failure rate was high enough that CI results were ignored. After quarantining all 18, the main suite went green consistently for two weeks — which immediately made the suite trustworthy again. The team then fixed the quarantined tests one per sprint over the next six weeks.

## Key takeaways

- Flakiness erodes trust in the entire test suite, not just the individual test
- Track failure rates in CI — flakiness is invisible without historical data
- Quarantine confirmed flaky tests immediately so the main suite remains reliable
- Fix root causes (timing, isolation, dependencies), not symptoms (retries)
- Set a team policy: flaky tests go to quarantine within one business day, get fixed within one sprint
