# Team Metrics That Matter

## Problem

QA teams are frequently asked to demonstrate their value through metrics. The instinct is to report what is easy to count: test cases executed, bugs found, pass rates. These numbers look like productivity but measure activity, not impact.

A team that finds 200 bugs per sprint may be finding bugs that should never have reached QA. A team that finds 5 bugs per sprint and ships zero production defects may be doing far more effective work.

## Solution

Measure outcomes, not activity. The metrics that matter are the ones that connect to the team's actual goal: reliable software reaching users.

**Escape rate: defects found in production vs. pre-production.**

This is the most important QA metric. A defect that reaches production was not caught by the QA process. Track escape rate by severity and trend over time. A declining P0 escape rate is meaningful signal; a stable test execution count is not.

**Time-to-detection: how late in the cycle are defects found?**

Defects found in unit testing cost less than defects found in QA, which cost less than defects found in production. Tracking where in the cycle defects are found measures the effectiveness of shift-left efforts.

**Automation reliability: flaky test rate and suite runtime.**

A flaky test suite erodes trust. An automation suite that takes 45 minutes to run blocks delivery. Both are QA infrastructure health metrics worth tracking.

**What not to track as primary metrics:**

- Test case count — more tests is not better if coverage is not improving
- Bugs found per sprint — this incentivizes finding low-value bugs
- Pass rate in isolation — a 100% pass rate on an inadequate test suite is meaningless

## Real-world example

A team was reporting 95% test pass rate and 300 test cases per quarter to leadership. Production had three P1 incidents in the same quarter. The metrics looked good; the outcomes did not.

After switching to escape rate and time-to-detection as primary metrics, the team identified that their automation covered only happy path flows. Investing in error path coverage reduced the escape rate from 3 P1 incidents per quarter to 0 over the following two quarters.

## Key takeaways

- Measure outcomes (escape rate, time-to-detection) rather than activity (tests executed, bugs found)
- Escape rate by severity is the most meaningful single QA metric
- Time-to-detection measures shift-left effectiveness — earlier detection is worth quantifying
- Automation reliability metrics (flaky rate, runtime) reflect QA infrastructure health
- Report metrics alongside what changed — a number without context is not actionable
