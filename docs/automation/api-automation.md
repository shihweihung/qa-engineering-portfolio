# API Testing

This is where my practical automation experience actually lives.

---

## Postman

Postman has been my primary tool for API testing throughout my career. I use it for:

- **Exploratory testing** — understanding how an API behaves before writing formal test cases
- **Manual verification** — validating specific endpoints during feature development and issue troubleshooting
- **Reproducing bugs** — isolating API behavior from UI behavior when investigating production issues
- **Sharing test scenarios** — exporting collections that other team members can use

I'm comfortable constructing requests, setting up authentication, using environment variables across different environments (dev/staging/production), and reading and interpreting response bodies.

---

## Basic API Verification in Practice

In my current role, API verification with Postman has been part of the feature validation workflow — checking that new endpoints return the expected structure and values, verifying error responses for invalid inputs, and confirming that changes in one service are reflected correctly in dependent services.

This isn't automated in the sense of running in CI — it's manual verification using Postman as the tool. The value is in the systematic coverage: checking not just the happy path, but the common error conditions and edge cases that developers may not have tested explicitly.

---

## What I Understand But Haven't Shipped

From participating in automation discussions and my current learning, I understand how Python + requests + pytest API automation suites work conceptually — centralized clients, fixture-based setup, schema validation with jsonschema. I haven't owned the delivery of a production API automation suite, but I understand what one needs to look like and why.
