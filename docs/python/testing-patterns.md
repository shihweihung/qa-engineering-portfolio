# Testing Patterns That Prevent False Positives

## Problem

Tests that pass when the feature is broken are worse than no tests. They create false confidence and suppress investigation. The most common causes are tests that do not actually assert the expected behavior, tests that pass because of side effects from other tests, and tests that test the mock rather than the code.

## Solution

**Follow the Arrange-Act-Assert structure.**

Every test has three parts: setup (Arrange), execution (Act), and verification (Assert). Mixing these creates tests that are hard to read and easy to write incorrectly.

```python
def test_user_receives_welcome_email_on_registration(email_client, api):
    # Arrange
    new_user_data = {"email": "user@example.com", "password": "secure123"}

    # Act
    api.register(new_user_data)

    # Assert
    assert email_client.last_sent_to == "user@example.com"
    assert "welcome" in email_client.last_subject.lower()
```

**Keep tests isolated — no shared mutable state between tests.**

Tests that depend on execution order are fragile. Any test should be runnable in isolation and produce the same result regardless of what ran before it. Use fixtures with appropriate scope and teardown to enforce this.

**Test behavior, not implementation.**

A test that verifies a private method was called is testing how the code works, not what it does for the user. If the implementation changes but the behavior stays the same, the test should still pass.

**Assert on the specific thing that can fail.**

Vague assertions like `assert result is not None` pass even when the result is wrong. Assert on the specific value or behavior that matters.

```python
# Weak: passes for any non-None result
assert response is not None

# Strong: verifies the specific expected outcome
assert response.status_code == 200
assert response.json()["user_id"] == expected_user_id
```

## Real-world example

A team had a test that was passing consistently but the feature was broken in production. Investigation revealed the test was asserting on the mock return value, not the actual output of the function under test — the function was never called. The test was testing the test setup, not the code.

After adding a call verification step and replacing the vague assertion with specific field checks, the test correctly failed for the existing bug.

## Key takeaways

- AAA structure (Arrange-Act-Assert) makes tests readable and correct by design
- Tests must be independently runnable — no hidden dependencies on execution order
- Test behavior, not implementation — implementation tests break on refactors that do not change behavior
- Specific assertions catch specific failures; vague assertions catch nothing
- If a test has never failed, it may not be testing anything
