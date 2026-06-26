# Release Readiness

## Problem

"Is it ready to ship?" is asked at the end of every sprint, and answered differently by QA, engineering, and product every time. Without a shared definition, release decisions are made by whoever has the most social capital in the room — not by the team's actual confidence in the build.

A QA lead who says "no" without a clear framework is just another opinion. A QA lead who defines release readiness in advance transforms the question from a judgment call into a checklist.

## Solution

Release readiness is a set of conditions that must be met, agreed upon before the sprint starts, not debated at the end.

**Define the conditions by risk tier, not by calendar.** A minor content update and a payment flow refactor should not have the same release criteria. The conditions scale with the risk of the change.

**Separate blocking from non-blocking issues.** Not every open bug is a blocker. A blocker is a defect that prevents a user from completing a critical flow, causes data loss or corruption, or violates a regulatory requirement. Everything else is a known issue with a documented severity and a plan.

**Include signal from automated tests.** Release criteria should specify what must pass, not just "all tests." A failing flaky test that has been quarantined is different from a failing test on a critical payment path. The distinction should be explicit.

**Make the release decision auditable.** A release sign-off should record what was tested, what was deferred, and who made the call. This creates accountability and makes post-release retrospectives more useful.

## Real-world example

A team was releasing on a two-week cycle but spending the last three days of each sprint in a "is it ready" conversation that produced stress rather than decisions. QA had no formal criteria; the release decision defaulted to whoever pushed hardest.

The QA lead introduced a one-page release checklist covering: all automated regression tests passing on the target build, no open P0 or P1 defects without an approved deferral, manual exploratory coverage of any new feature, and explicit sign-off from QA and one engineer. The checklist was version-controlled and updated each quarter.

Within two cycles, the end-of-sprint conversation was five minutes long. The team was spending that time on the next sprint instead.

## Key takeaways

- Define release readiness criteria before the sprint starts, not at the end of it
- Scale the criteria to the risk of the change, not the proximity of the deadline
- Separate blocking bugs from known issues — not everything open is a blocker
- Include specific automated test requirements in the criteria, not just "tests pass"
- Make release decisions auditable: document what was tested, what was deferred, and who approved
