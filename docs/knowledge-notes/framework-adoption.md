# Framework Adoption

## The Lesson

When two teams are evaluating the same tooling decision, the technical comparison is rarely the hard part. The hard part is that each side has already formed an opinion, and the evaluation process needs to produce alignment, not just a recommendation.

I worked through a multi-month framework selection process between a local team and an overseas team debating whether to adopt BDD (Gherkin/Behave) or pure Python pytest for a new automation effort. Both sides had valid technical arguments. The disagreement wasn't really about the tools.

---

## What I Observed

The BDD argument was primarily about collaboration: test cases readable by non-engineers, shared ownership of test definitions, product managers who could read the test scenarios. Legitimate benefits — on teams where those benefits are actually realized.

The pytest argument was primarily about engineering control: no translation layer, parametrize and fixture composition, less ceremony for complex test logic. Also legitimate — especially for teams where the "non-engineer readability" of BDD scenarios is theoretical rather than practiced.

What I noticed: each team's preference correlated almost perfectly with their team's composition and working style, not with a neutral technical assessment.

---

## What I Learned

**Framework choices are organizational choices.** The right tool depends on who will use it, how the team works, and what problems they're actually trying to solve — not on which framework is objectively better.

**A shared goal clarifies the decision.** In our case, agreeing that the goal was 1000 automated test cases over 12 months — with clear ownership expectations — made the tradeoffs concrete. BDD's ceremony has a real cost when you're trying to build volume. That shifted the discussion.

**Technical disagreements between teams are often proxy disagreements about ownership.** The team that "wins" the framework choice has to maintain it. Recognizing that dynamic early helps navigate the conversation more honestly.

The final decision was pytest. The more important outcome was that both teams understood why.
