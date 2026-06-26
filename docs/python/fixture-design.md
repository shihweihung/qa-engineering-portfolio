# Fixture Design in Pytest

## Problem

Test setup code that lives inside test functions has two problems: it is duplicated across tests that need the same setup, and it is coupled to the test itself — making it hard to change without touching every test that uses it.

The common workaround is a base class with setup and teardown methods. This works, but it hides setup in inheritance hierarchies that are difficult to follow and make dependencies between tests implicit.

## Solution

pytest fixtures provide explicit, composable, scope-controlled setup that is injected into tests by name rather than inherited. They solve the duplication problem without introducing class hierarchies.

**Design fixtures around what the test needs, not what the test does.**

A fixture that creates a user and logs them in is better than a fixture that does the login flow. The first is reusable across any test that needs an authenticated user. The second is coupled to the specific flow.

```python
@pytest.fixture
def authenticated_user(api_client):
    user = api_client.create_user(email="test@example.com", password="secure123")
    api_client.login(user.email, user.password)
    yield user
    api_client.delete_user(user.id)  # teardown
```

**Use scope to control how often setup runs.**

A database connection does not need to be created once per test. A user account for read-only tests does not either. Use `scope="session"` for expensive setup that is safe to share, `scope="function"` (the default) for anything with state that must be isolated.

```python
@pytest.fixture(scope="session")
def db_connection():
    conn = create_connection()
    yield conn
    conn.close()
```

**Keep fixtures composable, not monolithic.**

A fixture that does everything makes tests hard to understand and hard to maintain. Compose small fixtures into larger ones when needed.

```python
@pytest.fixture
def order(authenticated_user, product):
    return create_order(user=authenticated_user, product=product)
```

## Real-world example

A test suite had a `setUp` method in a base class that created a user, logged in, added a product to a cart, and initiated checkout — even for tests that only needed an authenticated user. Refactoring checkout broke tests that had nothing to do with checkout.

After extracting each concern into its own fixture, each test declared exactly what it needed. Checkout changes only affected tests that used the checkout fixture.

## Key takeaways

- Fixtures make dependencies explicit; base class setup hides them
- Design fixtures around what the test needs, not what it does
- Use scope to avoid redundant expensive setup
- Compose small fixtures rather than building monolithic ones
- Always include teardown to leave the environment clean — use `yield`, not `return`
