# Custom Test Reporters

## Problem

pytest's default output tells engineers whether tests passed or failed. It does not tell stakeholders how many user-facing scenarios were verified, which risk areas were covered, or what the trend looks like over time.

Test output that only engineers can read creates a gap: QA cannot demonstrate coverage to product or leadership, and product cannot use test results to inform release decisions.

## Solution

pytest plugins allow custom output at the level of detail that different audiences need. The key is separating what the CI log needs from what a stakeholder report needs.

**Use `pytest-html` for self-contained HTML reports.**

`pytest-html` generates a single HTML file with pass/fail results, screenshots (for UI tests), and run metadata. It requires no server and can be attached to CI artifacts directly.

```bash
pytest --html=reports/report.html --self-contained-html
```

**Write a custom plugin for business-readable output.**

A plugin that emits a summary of covered scenarios — expressed in product language rather than test IDs — is more useful than a raw pass/fail count for non-engineering stakeholders.

```python
# conftest.py
def pytest_terminal_summary(terminalreporter, exitstatus, config):
    passed = len(terminalreporter.stats.get("passed", []))
    failed = len(terminalreporter.stats.get("failed", []))
    print(f"\n=== QA Summary ===")
    print(f"Scenarios verified: {passed}")
    print(f"Scenarios failing:  {failed}")
```

**Tag tests with business categories and filter in reports.**

Using custom markers, tests can be grouped by feature area, risk tier, or release milestone. Reports filtered by marker give stakeholders targeted coverage information.

```python
@pytest.mark.critical
@pytest.mark.payment_flow
def test_checkout_completes_successfully():
    ...
```

## Real-world example

A QA team was asked to demonstrate test coverage before a major release. They had 300 tests and a passing CI build, but could not quickly answer "how many critical payment flows are verified?" without manually counting.

Adding `critical` and `payment_flow` markers, and a custom report template that filtered by those markers, reduced the answer to a single command and a readable output that the release review meeting could act on.

## Key takeaways

- Default pytest output is for engineers; stakeholder reports need a different format
- `pytest-html` provides a self-contained report suitable for CI artifacts and sharing
- Custom terminal summary plugins provide release-time snapshots without additional tooling
- Markers enable targeted reporting by feature area, risk tier, or release scope
- Invest in reporting early — it becomes significantly harder to retrofit markers across a large suite
