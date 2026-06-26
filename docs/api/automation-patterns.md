# API Automation Patterns

## Problem

API test suites that grow without structure become difficult to maintain. Tests reference hardcoded URLs. Authentication is duplicated across every test. The same request is constructed five different ways in five different files. When the API changes, updates are scattered across the entire suite.

## Solution

Structure API tests around three layers: a client that handles requests and authentication, fixtures that provide test data and setup, and test functions that express scenarios in terms of the business behavior being verified.

**Centralize the API client.**

```python
class APIClient:
    def __init__(self, base_url: str, token: str):
        self._session = requests.Session()
        self._session.headers.update({"Authorization": f"Bearer {token}"})
        self._base_url = base_url

    def get_user(self, user_id: int) -> dict:
        response = self._session.get(f"{self._base_url}/users/{user_id}")
        response.raise_for_status()
        return response.json()

    def create_user(self, data: dict) -> dict:
        response = self._session.post(f"{self._base_url}/users", json=data)
        response.raise_for_status()
        return response.json()
```

**Provide the client via fixture.**

```python
@pytest.fixture(scope="session")
def api(config):
    return APIClient(base_url=config.api_url, token=config.api_token)
```

**Test business behavior, not HTTP mechanics.**

```python
def test_new_user_defaults_to_standard_role(api):
    user = api.create_user({"email": "new@example.com", "password": "secure"})
    assert user["role"] == "STANDARD"
```

## Real-world example

A team's API test suite had 80 tests, each constructing `requests.Session` objects with manual headers. When authentication moved from a token to an OAuth flow, 80 tests needed updating. After centralizing authentication in the client, the same migration was a one-line change in one file.

## Key takeaways

- Centralize authentication and base URL in a client class, not in test functions
- Provide the client via session-scoped fixture to avoid repeated initialization
- Test functions should express business behavior, not HTTP mechanics
- Raise exceptions on unexpected status codes at the client level, not in every test
- Keep request construction DRY — duplicated request logic is the most common source of maintenance cost
