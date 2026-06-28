# API Testing

## What I've Done

API testing has been a consistent part of my QA work across multiple products. I've tested REST APIs at the integration level — validating responses, checking authentication flows, verifying error handling, and building automated test suites that run in CI.

---

## Responsibilities

**Manual API exploration with Postman**

When a new API feature lands, my first step is exploratory: understand the contract, map the edge cases, find the places where the behavior doesn't match what was specified. Postman is my primary tool for this phase. I build collections that document the API behavior and share them with the team.

**Automated API validation**

I've built Python-based API test suites using pytest and the requests library. The suites cover happy paths, common error conditions, authentication boundaries, and schema validation. They run in CI and provide fast feedback on API regressions before they surface in UI testing.

**Cross-service validation**

In products with multiple services talking to each other, I pay attention to the integration boundaries — how one service's response feeds into another's request, where data gets transformed, and where silent failures can propagate downstream without obvious symptoms.

**Error handling and edge cases**

I test what happens when things go wrong: malformed payloads, expired tokens, rate limiting, missing required fields, and boundary values. Many API bugs hide in error paths that developers don't test because they're focused on making the happy path work.

---

## Challenges

**Undocumented behavior**

APIs frequently behave differently from their documentation. I've learned to treat the documentation as a starting point, not a source of truth, and to verify the actual behavior before building tests around it.

**Stateful API flows**

Some API scenarios require a specific sequence of calls — create a resource, then use its ID in the next call, then verify the state. Managing that state in automated tests without creating coupling between test cases takes care.

**Authentication complexity**

OAuth flows, token refresh, session management — authentication failures are common and often subtle. I make sure auth edge cases are covered explicitly rather than assuming they work because the happy path does.

---

## Lessons Learned

API tests give the best signal-to-maintenance ratio of any test layer. They run fast, they're isolated from UI changes, and when they fail, the failure is usually clear. I try to push as much coverage to the API layer as possible, reserving UI automation for scenarios that can only be verified through the interface.
