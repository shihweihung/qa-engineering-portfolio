# Regression Prevention

## Problem

A bug that is fixed and then recurs is a process failure, not just a code failure. The fix was incomplete, the test coverage was insufficient, or the fix was later accidentally reverted. Regression is one of the most visible quality failures — it signals to users that the product was not tested, and it signals to the team that previous work cannot be trusted.

## Solution

Regression prevention requires closing the feedback loop between the bug and the test suite so that the same defect cannot ship again undetected.

**Write a failing test before fixing the bug.**

The sequence is: reproduce the bug, write a test that fails due to the bug, fix the bug, verify the test now passes. This sequence guarantees that the test captures the specific condition that produced the bug — not a generalization of it.

A test written after the fix often tests the fix rather than the bug. The distinction matters: if the fix is later reverted or changed, a test that verifies the bug's behavior will catch the regression; a test that verifies the implementation of the fix may not.

**Add the test to the regression suite, not just the feature suite.**

A test added only to a feature-specific test file may not run on unrelated changes. Regression tests for critical bugs belong in a suite that runs on every change to the affected area.

**Track regression rate by feature area.**

If the same area of the product produces repeated regressions, the tests for that area are insufficient or the code is structurally fragile. Tracking regression by area makes patterns visible before they become chronic.

**Include regression coverage in the definition of done for bug fixes.**

"The bug is fixed" is not done. "The bug is fixed and a regression test is in CI" is done. Adding this to the team's definition of done institutionalizes regression prevention without requiring QA to verify each fix individually.

## Real-world example

A team had a recurring bug in a discount calculation feature — the same incorrect rounding behavior appeared three times over eight months, each time after a change to adjacent code. Investigation revealed there was no test for the specific rounding case.

After adding a parametrized test covering all the rounding edge cases, the same bug was caught automatically in CI twice in the following four months — both times before it reached users.

## Key takeaways

- Write the failing test before the fix, not after — it ensures the test captures the defect condition
- Regression tests belong in suites that run on every relevant change, not just the feature suite
- Track regression rate by feature area to identify structurally fragile code
- Regression coverage should be part of the definition of done for bug fixes
- A recurring bug in the same area is a signal about test coverage, not just about code quality
