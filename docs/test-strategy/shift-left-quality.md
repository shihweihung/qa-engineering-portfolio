# Shift-Left Quality

## Problem

In a traditional workflow, QA receives a build after development is complete and reports bugs that development must then fix before release. This creates a predictable bottleneck: defects found late are more expensive to fix, schedule pressure increases, and the QA phase becomes the place where bad news is delivered rather than prevented.

"Shift left" is the practice of moving quality activities earlier — but the phrase is overused without specifics. Simply adding a QA person to planning meetings does not shift quality left. The activities need to change.

## Solution

Shifting left means changing where quality decisions are made, not just when QA gets involved.

Three concrete shifts produce the most impact:

**Requirements review before development starts.** QA involvement in user story refinement surfaces testability gaps, undefined edge cases, and missing acceptance criteria before a single line of code is written. A story that cannot be tested without manual verification is a story that should not be accepted into the sprint.

**Developer-authored tests as part of definition of done.** Unit and integration tests written by the engineer who built the feature catch the obvious failures immediately, before QA ever sees the build. This does not replace QA — it raises the floor so QA can focus on what automated unit tests cannot reach.

**Automation at the right layer.** E2E tests are slow and brittle. Shifting coverage to lower layers — unit, service, contract — gives faster feedback with less maintenance overhead. QA's role is to own the test strategy across layers, not to own all the test authorship.

## Real-world example

A team was experiencing a consistent pattern: QA found critical bugs in the final week of each sprint, causing either delayed releases or rushed hotfixes. The bugs were not exotic — they were straightforward edge cases that no one had thought through during planning.

The QA lead introduced a structured requirements review in sprint planning. Each story went through three questions: what is the happy path, what are the main failure modes, and what does the acceptance test look like. Stories that could not answer all three were sent back for refinement.

Within two sprints, the team was catching ambiguities that previously became bugs, and QA was spending less time on regression and more time on exploratory testing of genuinely new behavior.

## Key takeaways

- Shifting left means changing where quality decisions are made, not just adding QA to meetings earlier
- Requirements review before development is the highest-leverage shift-left activity
- Developer-authored tests raise the floor so QA can focus on higher-value coverage
- Automation at lower layers (unit, service) gives faster feedback than additional E2E coverage
- The measure of a successful shift-left is how early defects are found, not when QA gets involved
