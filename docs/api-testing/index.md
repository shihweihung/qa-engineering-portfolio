# API Testing

A summary of my experience testing REST APIs — manually and through automation.

---

## How I Approach API Testing

API testing is the layer of the test pyramid with the best return on investment. APIs are faster to test than UI, easier to control than production, and when they fail, the failures are usually informative.

My approach to any API testing engagement:

1. **Understand the contract** — What does this endpoint promise to return? Under what conditions? What are the documented error cases?
2. **Test the error paths deliberately** — Developers write code to the happy path. The error handling paths are where bugs hide.
3. **Validate more than status codes** — HTTP 200 doesn't mean correct. Validate response schemas, field values, and business logic.
4. **Automate the stable, manual the exploratory** — Regression suites automate the known behavior. Manual exploration investigates the unclear behavior.

---

## Tools I Use

**Postman** — My starting point for manual API exploration. I use it to understand a new API, experiment with requests, document collections, and share test scenarios with the team. Postman collections have been useful for onboarding new team members.

**Python + requests + pytest** — Automated API test suites. I've built suites around a centralized API client class that handles authentication and base URL configuration. Tests use the client's methods rather than constructing raw requests.

**jsonschema** — Response schema validation. Defining the expected shape of API responses and validating automatically catches breaking changes before they surface elsewhere.

---

## What I've Built

- Authentication flow testing: login, token refresh, token expiry, logout, concurrent session handling
- Content API testing: retrieval, pagination, filtering, search
- Purchase flow API testing: validation, error conditions, idempotency
- Cross-service validation: verifying that an action on one API produces the expected state in another
- Schema validation for key response types

---

## What I Focus On

**Error path coverage** — Missing required fields, malformed payloads, invalid authentication tokens, expired sessions, rate limits. These conditions are usually undertested.

**State verification** — Testing that an API call produces the correct downstream state, not just the correct response. A "successful purchase" that doesn't update account state is a bug, even if it returns 200.

**Cross-service consistency** — When multiple services are involved, verify that state is consistent across them. These are often the hardest bugs to catch in isolated unit or integration testing.

**CI integration** — API test suites run in CI on every significant pull request. They're fast enough to include without meaningfully increasing build time, and they catch regressions before they surface as UI failures or user reports.
