# Root Cause Analysis

## Problem

A bug that gets fixed without understanding why it happened will happen again. The symptom is addressed; the underlying condition is not. Teams that fix bugs without root cause analysis accumulate technical debt in their quality process — the same classes of defects recur, and the team treats each instance as new rather than recognizing the pattern.

## Solution

Root cause analysis goes beyond "what broke" to "why did it break" and "why wasn't it caught earlier."

**The five-why technique applied to software defects.**

Start with the observable failure and ask "why" repeatedly until you reach an actionable cause:

1. Why did the user see an error? — The API returned a 500 status.
2. Why did the API return a 500? — A null pointer exception in the response handler.
3. Why was there a null pointer exception? — A field that was previously always present became optional in a schema update.
4. Why was the optional field not handled? — The contract between the API and its consumer was not documented or tested.
5. Why was there no contract test? — The team had no practice of contract testing for this service.

The fifth why points to a systemic gap — no contract testing practice — not just a missing null check. The fix is not just adding a null check; it is establishing contract testing for service boundaries.

**Distinguish immediate cause from systemic cause.**

The immediate cause is what broke. The systemic cause is why the team was in a position where this could break. Both need to be addressed, but the systemic cause is more valuable to understand.

**Produce a finding and a prevention action.**

Root cause analysis that produces only a description of what happened is not complete. Each analysis should end with at least one concrete prevention action: a new test type, a process change, a documentation update, or a code pattern change.

## Real-world example

A production incident caused order confirmations to be sent without order details for a subset of users. The immediate cause was a race condition in an async email dispatch. The root cause analysis traced it to a missing integration test for the async path, which had been deprioritized because the synchronous path was well-covered.

The prevention action was not just fixing the race condition — it was adding async path coverage as a standard requirement for any feature using event-driven architecture.

## Key takeaways

- Fixing a symptom without understanding the root cause produces recurring bugs
- The five-why technique traces from symptom to systemic gap
- Distinguish immediate cause (what broke) from systemic cause (why the team was vulnerable)
- Root cause analysis is complete only when it produces a concrete prevention action
- Document findings and actions — patterns become visible only when tracked over time
