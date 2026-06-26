# Quality Gates

## Problem

Without explicit quality gates, CI pipelines enforce compilation and test execution but not quality outcomes. A build can have 30 failing tests, zero coverage on a new feature, and an open critical defect — and still deploy because nothing blocked it.

Quality gates make the delivery standard explicit and machine-enforced. They turn implicit expectations into hard checks.

## Solution

A quality gate is a condition that must be true for a build to proceed. Define gates that match the risk level of the stage.

**Common quality gates and their appropriate stage:**

| Gate | Stage | Rationale |
|---|---|---|
| All unit tests pass | Every PR | Fast, low cost, high signal |
| No new critical-severity linting violations | Every PR | Catches common mistakes before review |
| All API tests pass on deployed service | Post-merge | Validates integration |
| E2E test pass rate ≥ 95% | Release candidate | Tolerates known flakiness without skipping the gate |
| No open P0 defects | Release | Safety net before production |
| Coverage on changed files ≥ defined threshold | Every PR (optional) | Targeted coverage enforcement |

**Implement gates at the pipeline level, not the process level.**

A gate that exists as a Slack message or a checklist item is a social contract, not a gate. A gate that fails the build is a gate.

```yaml
# GitHub Actions: fail the build if tests below threshold
- name: Check test results
  run: |
    PASS_RATE=$(python scripts/compute_pass_rate.py)
    if (( $(echo "$PASS_RATE < 0.95" | bc -l) )); then
      echo "Pass rate $PASS_RATE below threshold 0.95"
      exit 1
    fi
```

**Make gate failures actionable, not just blocking.**

A gate failure message that says "tests failed" is less useful than one that says "12 tests failed in the payment flow; see linked report." Gates should tell the team what to fix, not just that something is broken.

## Real-world example

A team had a manual release checklist that included "QA sign-off" as a step. In practice, time pressure consistently shortened the review. After encoding the release criteria as pipeline gates — no open P0s verified via JIRA API, E2E pass rate above 95%, all smoke tests green — the release decision became automatic when conditions were met.

The team stopped having end-of-sprint debates about whether it was ready to ship.

## Key takeaways

- Quality gates enforce delivery standards automatically, without relying on social contracts
- Define gates before the sprint, not at the end of it
- Gates should match the risk level of the stage — not every gate belongs on every PR
- Make gate failures actionable: include enough information to diagnose the issue immediately
- A gate that can be bypassed is not a gate — pipeline enforcement is the point
