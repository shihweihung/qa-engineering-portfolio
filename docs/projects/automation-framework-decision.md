# Automation Framework Decision

## Situation

Our QA team was distributed across two regions. Each region had independently developed automation practices: the local team used a Python/pytest-based framework built around the product's UI; the overseas team used a BDD framework with Gherkin feature files and an existing CI integration.

The client had set a clear expectation: all manual test cases — approximately 1000 in total — should eventually be covered by automation, with the goal of shortening the release cycle significantly. The current automation coverage after years of work was around 100 cases.

Both teams were asked to evaluate which framework should be adopted going forward.

---

## Challenge

The technical decision was entangled with organizational dynamics in ways that made straightforward evaluation difficult.

Each team had an incentive to advocate for their own framework — it represented existing work and engineering identity. The local team's automation lead was particularly resistant to adopting an external framework, citing concerns about team ownership and job security (those concerns were stated explicitly, which at least made them visible). The overseas team pointed to their BDD framework's existing CI integration and claimed it was production-ready.

The decision maker was caught between the two teams and was avoiding a direct call.

On the technical side, the real questions were:

- Which framework could realistically reach 1000 automated cases with a team of mixed technical backgrounds?
- Which could run across iOS, Android, and e-ink hardware?
- What would maintenance look like as the app continued to change?

---

## My Role

I was a member of the local team but tried to evaluate both options honestly. I wasn't the decision maker, but I had a clear view of both frameworks and was asked to contribute analysis.

I was also navigating the political situation — I cared about getting to the right answer technically more than I cared about which team "won."

---

## Solution

I focused the analysis on the client's stated goal: 1000 cases, shorter release cycle.

**BDD's structural advantage for scale.** Gherkin feature files map directly to human-readable test cases. QA engineers who aren't strong programmers can contribute to a BDD suite in a way they can't contribute to a Python framework that requires comfortable coding skills. For a team trying to scale to 1000 cases, that lower barrier to contribution matters.

**The maintenance question.** As the app was being rewritten, any automation written against the current UI was going to require significant rework. A framework that made it easier to rewrite scenarios (BDD's feature files are relatively straightforward to update) had an advantage over one where automation was tightly coupled to implementation details.

**The cross-platform requirement.** Both frameworks claimed cross-platform support. I pushed for concrete evidence on what "cross-platform" actually meant in practice — not in theory, but running against real devices. The overseas team's CI integration didn't cover e-ink hardware. That was a real gap.

**The organizational reality.** The local team's concern about ownership and redundancy was legitimate even if it was being used as a shield. I flagged that any framework decision needed to address how work was going to be divided, not just which framework was technically better.

---

## Outcome

The decision-making process was slow — organizational dynamics slowed it significantly. What I contributed was clarity on the technical criteria and a framework for evaluation that separated the technical question from the ownership question.

The lesson I took from this: technical decisions in distributed organizations rarely succeed unless the organizational concerns are addressed alongside the technical ones. A technically correct answer that lands in a team that doesn't believe in it will be undermined.

---

## Lessons Learned

Framework decisions that look like technical choices are often also organizational choices. The team that builds and maintains the framework needs to believe in it. A framework chosen without that buy-in will be maintained grudgingly and eventually abandoned.

When I look at a "which framework" question now, I ask: who will own this in two years? What do they need to succeed? The technical answer and the organizational answer should both point the same direction.
