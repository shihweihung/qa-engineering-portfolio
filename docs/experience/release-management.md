# Release Management

## What I've Done

Release management is one of the most visible parts of QA work. The team looks to QA to answer "can we ship this?" — and that answer has to be grounded in something real, not just confidence or optimism.

I've been part of release processes for mobile apps on iterative sprint cycles. I own the QA side of release readiness: test coverage, open issue review, risk communication, and final sign-off.

---

## Responsibilities

**Defining release criteria upfront**

I establish what "done" looks like before the sprint starts, not at the end of it. That means agreeing on which test scenarios must pass, what severity of open issue can be deferred, and what constitutes a blocker versus an acceptable known issue.

When the criteria are clear before the sprint, the end-of-sprint conversation is straightforward. When they're not, the release decision becomes a negotiation, and the outcome depends on who pushes hardest rather than on the actual state of quality.

**Regression scope management**

Not every release requires running everything. I maintain a risk-tiered regression scope — what must be validated for every release, what gets spot-checked on significant changes, and what's covered implicitly by automated testing. That lets us release with confidence without running full regression on every sprint.

**Risk communication**

When there are open issues at release time, I document them clearly: what the issue is, who it affects, what the workaround is (if any), and the team's reasoning for shipping with it. This isn't about hiding problems — it's about making the risk visible and giving stakeholders the information they need to make an informed decision.

**Coordination across stakeholders**

A release involves more than QA and engineering. I coordinate with product management and leadership to ensure that known issues, scope changes, and quality risks are communicated before the release, not discovered after.

---

## Challenges

**Pressure to ship with open issues**

Release deadlines create pressure, and that pressure falls on QA when there are still open questions. I've been in situations where the ask was "can we ship anyway?" for issues I wasn't comfortable deferring. Learning to hold that line without being obstructionist — clearly explaining the risk and what it would take to mitigate — is a skill that develops with experience.

**Last-minute scope changes**

A feature that lands late in the sprint compresses QA time. When that happens, I make a fast risk assessment: what's the worst-case failure scenario for this change, how visible is it, and what's the minimum coverage needed to feel reasonably confident? Explicit fast-risk-assessment is better than either skipping testing or refusing to release.

---

## Lessons Learned

Release readiness is a process, not a moment. Teams that define their release criteria upfront, maintain automated coverage of critical paths, and communicate risk clearly throughout the sprint have much calmer release days than teams that save the quality assessment for the end.

The goal isn't zero known issues at release. It's known and understood risk, with a plan for anything significant.
