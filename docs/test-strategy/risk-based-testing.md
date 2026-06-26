# Risk-Based Testing in Practice

## Problem

Test coverage is theoretically unlimited. Given any non-trivial product, a team can always write more tests. But engineering time is finite, release windows are fixed, and not all failures carry equal weight.

Without a deliberate framework for deciding what to test, QA effort drifts toward familiarity rather than risk. Engineers test what they know, not what is most likely to break or most expensive to miss.

## Solution

Risk-based testing allocates effort proportional to two dimensions: probability of failure and impact of failure. A feature that is architecturally fragile and customer-facing receives deep coverage. A stable internal utility with limited blast radius receives minimal coverage.

**Step 1: Map coverage to risk, not feature count.**

For each product area, estimate:

- How likely is this to break? (Consider: recent changes, technical complexity, third-party dependencies, historical defect rate)
- What happens if it breaks? (Consider: user impact, revenue impact, recovery cost, reputational damage)

This produces a rough risk matrix. High probability × high impact = mandatory deep coverage. Low probability × low impact = sanity check only.

**Step 2: Define a coverage policy, not a test count target.**

Coverage targets like "80% code coverage" or "all test cases executed" are easy to game and easy to misread. Instead, define what each risk tier requires:

| Risk tier | Coverage expectation |
|---|---|
| Critical (high prob × high impact) | Automated regression + manual exploratory on every release |
| Elevated | Automated regression, exploratory on major changes only |
| Standard | Automated smoke, manual on significant changes |
| Low | No dedicated coverage; caught by adjacent tests or monitoring |

**Step 3: Revisit the matrix when the product changes.**

Risk is not static. A refactor moves code from stable to elevated. A new payment integration is immediately critical. The risk matrix is a living document, not a one-time artifact.

## Real-world example

A cross-platform app has three primary flows: authentication, content browsing, and in-app purchase. The team has two QA engineers and a two-week sprint.

Authentication is critical: failure locks all users out, recovery requires manual intervention, and the flow was recently refactored. It gets deep automated coverage and manual exploratory testing on every release.

Content browsing is elevated: failure is visible and frustrating, but users can reload and continue. It gets automated regression covering the happy path and key error states.

In-app purchase is critical from a revenue perspective but is handled almost entirely by a third-party SDK. The team focuses coverage on the integration layer — what the app does before and after the SDK call — rather than re-testing SDK internals.

The internal logging system gets no dedicated test coverage. It has never failed in production, has no user-facing impact if it does, and is caught incidentally by other tests.

## Key takeaways

- Test effort should follow risk, not feature count or engineering intuition
- Risk has two independent dimensions: probability of failure and impact of failure
- Define what coverage each risk tier requires, then apply it consistently
- Revisit the risk map after significant product changes, architecture changes, or new production incidents
- Explicit coverage decisions are easier to defend in planning discussions than implicit ones
