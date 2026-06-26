# Incident Retrospectives

## Problem

Production incidents produce pressure to find someone to blame and move on. Teams that operate this way repeat the same incidents because the conditions that allowed the incident remain unchanged. Blame also suppresses honest reporting — engineers learn not to surface problems if the consequence is becoming the responsible party.

A retrospective that assigns blame is a retrospective that does not improve anything.

## Solution

Blameless retrospectives assume that engineers acted reasonably given the information they had at the time, and focus instead on the conditions and systems that made the incident possible.

**Timeline reconstruction.**

Start by reconstructing a factual timeline: when was the change deployed, when was the first signal of a problem, when was it detected, when was it diagnosed, and when was it resolved. The timeline reveals detection gaps and response time without assigning blame.

**Contributing factors, not root cause.**

Most incidents have multiple contributing factors rather than a single root cause. A production outage is rarely just "someone made a mistake." It is typically a combination of: a code change, insufficient test coverage on the affected path, a monitoring gap that delayed detection, and a deployment process that did not catch the issue before production.

**Identify systemic improvements in each category.**

For each contributing factor, ask what systemic change would prevent or catch this class of problem. Common improvement categories:

- Test coverage: was there a test that should have caught this?
- Monitoring: was there a signal that should have alerted the team earlier?
- Deployment: was there a check that should have caught this before production?
- Documentation: would better documentation have prevented the incorrect assumption?

**Track improvements to completion.**

A retrospective that produces a list of improvements but no follow-through is the same as no retrospective. Assign each improvement to an owner with a target date and review progress in the next retrospective.

## Real-world example

An API change broke backwards compatibility for clients on an older app version. The retrospective revealed four contributing factors: no version compatibility tests, no monitoring on the affected endpoint's error rate, a deployment that skipped canary release, and an API contract that was not documented. Each produced a concrete improvement that the team implemented over the next two sprints.

## Key takeaways

- Blameless retrospectives produce more useful information than blame-focused ones
- Timeline reconstruction is the foundation — establish facts before drawing conclusions
- Most incidents have multiple contributing factors; address each rather than finding a single root cause
- Improvements should address systemic gaps: coverage, monitoring, deployment, documentation
- Track improvements to completion — an unimplemented improvement is not an improvement
