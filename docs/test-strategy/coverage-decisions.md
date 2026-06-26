# Test Coverage Decisions

## Problem

Coverage is easy to measure and hard to interpret. A codebase with 90% line coverage can still ship a critical bug. A suite with 40% coverage can give a team high confidence if the 40% covers the right things.

The problem is that most coverage conversations focus on the number rather than the decision behind the number. "We need 80% coverage" is not a strategy. It is a target that teams hit by writing tests for easy code rather than risky code.

## Solution

Coverage decisions should be explicit, documented, and tied to risk.

**Define what coverage means for your team.** Line coverage, branch coverage, and scenario coverage answer different questions. For most product teams, scenario coverage — the set of user-facing behaviors that are verified by automated tests — is more meaningful than code-level metrics.

**Document what is explicitly out of scope and why.** Untested code is not always a problem. Third-party SDKs, generated code, and well-isolated utilities with no user-facing impact may legitimately have no direct test coverage. The risk is leaving this implicit — unstated assumptions become invisible gaps.

**Use coverage as a diagnostic, not a gate.** Coverage that drops suddenly after a change is a signal worth investigating. Coverage that has been stable at 60% for six months may simply reflect a deliberate decision about scope. Reacting to the number without the context produces the wrong fixes.

**Align coverage expectations with the risk tier.** Critical paths get covered deeply. Low-risk code gets covered incidentally or not at all. This is the risk-based testing principle applied to coverage policy.

## Real-world example

A payments team had a rule requiring 85% code coverage on all new code before merge. The rule was producing tests that verified implementation details rather than behavior — tests that passed regardless of whether the feature worked correctly for users.

The QA lead replaced the code coverage gate with a scenario checklist: every new feature required documented coverage for the happy path, the primary error state, and any edge case surfaced during requirements review. There was no percentage threshold.

Coverage actually increased over the following quarter — not because the number was tracked, but because the conversation shifted to "what does this code need to handle" rather than "how do I hit 85%."

## Key takeaways

- Coverage numbers are easy to hit for the wrong reasons — the decision behind the number matters more
- Document what is explicitly out of scope, not just what is covered
- Use coverage as a diagnostic signal, not a release gate
- Scenario coverage is more meaningful than line coverage for most product teams
- Align coverage expectations with the risk tier of each product area
