# Mentoring

## What I've Found Works

The goal of mentoring a QA engineer isn't to teach them to follow a process correctly. It's to develop their ability to make good quality judgments independently.

That means focusing on the thinking behind decisions, not just the decisions themselves. When a junior QA engineer asks whether a bug is a blocker, the useful response isn't to answer the question — it's to walk through the considerations that lead to an answer: What's the user impact? How reproducible is it? Is there a workaround? What's the release risk? Over time, they internalize the framework.

---

## In Practice

**Code and test review as a teaching surface.** When I review test code or test plans, I explain the reasoning behind feedback rather than just marking something wrong. "Why does parametrizing this test help?" and "Why is this assertion not sufficient?" produce more learning than a corrected version.

**Pairing on hard problems.** When a QA engineer is stuck on something difficult — reproducing a hard bug, designing a test for a complex system, navigating a politically difficult conversation with a developer — working through it together is more valuable than advising from a distance.

**Calibrating autonomy to readiness.** I've found that junior engineers develop faster when they're given real responsibility before they feel fully ready, with support nearby. The risk of giving someone a problem they might not solve perfectly is usually outweighed by the development value. Protecting someone from hard problems keeps them junior.

---

## Cross-Regional Mentoring Complexity

I've mentored engineers across regional and time zone boundaries, which adds communication overhead. What I've learned: the documentation of reasoning matters more in distributed settings than in co-located ones. If the thinking is only in my head, it doesn't transfer. Written test plans, documented coverage decisions, and explicit rationale for engineering choices are more important when the mentoring relationship can't be continuous.

---

## What I'm Still Learning

Mentoring at scale — influencing quality thinking across a team without being present in every decision — is harder than individual mentoring. I've tried to address this through documentation and through creating shared frameworks the team uses, but I don't think I've fully solved the problem of how to build team-wide quality judgment rather than individual quality judgment.
