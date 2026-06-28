# API Automation

API automation is the test layer with the best return on investment: it's fast, it's stable, and when it fails, the failure is usually informative.

---

## How I Use It

**Centralized API client**

I build API tests around a client class that handles authentication, base URLs, and request construction centrally. Tests use the client's methods rather than constructing requests directly. This means authentication changes and base URL changes require a one-file update, not changes across every test.

**Validation beyond status codes**

Checking `status_code == 200` is necessary but not sufficient. I validate response schemas — required fields are present, types are correct, values are within expected ranges — and I validate business logic: a newly created user should have the default role, a successful purchase should update the account state.

I've used `jsonschema` for automated schema validation, which catches breaking API changes early rather than letting them propagate to UI failures.

**Error path coverage**

Developers test the happy path. I spend deliberate effort on error paths: malformed payloads, missing required fields, expired tokens, rate limits, and concurrent requests. Many API bugs hide in error handling code that is rarely exercised.

**CI integration**

API tests run in CI on every significant PR. They're fast enough that they don't meaningfully increase CI time, and they catch regressions on API behavior before they surface as UI test failures or user reports.

---

## Tools

- **Postman** — Exploratory testing, manual validation, collection sharing with the team
- **Python + requests + pytest** — Automated API test suites
- **jsonschema** — Response schema validation
- **GitHub Actions** — CI integration

---

## What I've Built

- Automated API test suites covering authentication, content APIs, and purchase flows
- Schema validation for key API responses
- Postman collections documenting API behavior shared with the broader team
