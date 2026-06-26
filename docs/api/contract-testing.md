# Contract Testing

## Problem

End-to-end tests that verify API integrations are slow, expensive, and brittle. They require both the consumer and the producer to be running simultaneously, and they fail for reasons that have nothing to do with the integration — network flakiness, environment configuration, unrelated data state.

The underlying question — "will the consumer and producer still work together after this change?" — does not actually require both to be running at the same time.

## Solution

Contract testing verifies the agreement between a consumer and a producer independently, without deploying both.

The consumer publishes a contract: a description of the API calls it makes and the responses it expects. The producer verifies that it can fulfill the contract. If the producer changes in a way that breaks the consumer's contract, the verification fails — before deployment.

**Consumer side: define the expected interaction.**

```python
# Using Pact for Python
from pact import Consumer, Provider

pact = Consumer("frontend-app").has_pact_with(Provider("user-service"))

pact.given("a user with ID 123 exists").upon_receiving(
    "a request for user 123"
).with_request(
    method="GET",
    path="/users/123"
).will_respond_with(
    status=200,
    body={"id": 123, "email": "user@example.com", "role": "USER"}
)
```

**Producer side: verify the contract.**

The producer runs against the published contract and verifies that each defined interaction produces the expected response. No consumer deployment required.

## Real-world example

A frontend team and a backend team were independently making changes to a user profile endpoint. The frontend expected a field called `display_name`; the backend had renamed it to `full_name` during a refactor. Both teams had passing tests. The integration broke in staging.

After introducing contract testing, the backend's verification step caught the field rename immediately. The integration issue was resolved before either change was merged.

## Key takeaways

- Contract tests verify API agreements without requiring end-to-end deployment
- The consumer defines what it expects; the producer verifies it can deliver
- Breaking contract changes are caught at the development layer, not in staging
- Contract tests are fast and suitable for running on every PR
- They do not replace integration tests entirely — they eliminate a specific class of integration failure
