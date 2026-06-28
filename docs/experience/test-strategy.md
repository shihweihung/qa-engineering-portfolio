# Test Strategy

## What I've Done

Writing a test strategy means answering the question: given limited time and resources, where does testing effort go? That answer changes with every product, every release, and every significant architecture change.

I've owned test strategy for mobile applications with cross-platform requirements, complex content delivery logic, and integration with third-party payment systems. Each area requires a different approach.

---

## Responsibilities

**Risk-based test planning**

I start every test planning conversation from risk, not feature count. The questions I ask: what happens when this fails? How likely is it to fail? How would we know if it did?

A user authentication flow that was recently refactored and touches every downstream service gets deep coverage. A minor UI tweak to a secondary settings screen gets a sanity check. The allocation is intentional and documented so the team understands what's covered and what's not.

**Coverage decisions and tradeoffs**

I document what's in scope and, importantly, what's explicitly out of scope and why. Untested code isn't always a problem — a well-isolated utility with no user-facing impact may legitimately have no dedicated test coverage. But that decision should be explicit, not accidental.

When coverage gets cut due to time pressure, I make the tradeoff visible: "we're not covering X; the risk is Y; we're accepting that because Z." That gives product and engineering the information to either agree or make a different call.

**Test strategy documents**

For significant features or architecture changes, I write a test strategy document: what the feature does, what the risk areas are, what's being tested and how, what's being deferred and why, and what the acceptance criteria are. It's a single page, not a 20-page specification. The point is alignment, not documentation for its own sake.

**Adapting strategy to the development phase**

Testing an early-stage feature is different from testing a release candidate. In early development, I focus on fundamental correctness and fast feedback to the developer. In release validation, I focus on regression coverage, integration scenarios, and known risk areas. The approach changes; the rigor shouldn't.

---

## Challenges

**Testing across platforms with limited time**

Cross-platform products multiply the testing surface. I've had to make explicit decisions about which scenarios get tested on both platforms, which get tested on one (the higher-risk one), and which are covered by shared automation. Those decisions need to be defensible when something does slip through.

**Communicating risk without causing alarm**

Not every risk is a blocker. Part of writing good test strategy is communicating what the team is accepting, without making every release feel like a gamble. That means being specific: not "there's risk" but "this specific scenario is untested, and here's what would happen if it failed."

---

## Lessons Learned

The most useful thing a test strategy does is make risk explicit. Teams that make explicit risk decisions feel more confident, even when they're shipping with known gaps, than teams that have implicit coverage and aren't sure what they're missing.
