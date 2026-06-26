# Data-Driven Testing

## Problem

Many test scenarios are identical in structure but differ only in their inputs and expected outputs. Writing a separate test function for each input combination produces repetitive code that is tedious to maintain and easy to get wrong. Adding a new case requires duplicating a function; removing a case requires finding and deleting it.

## Solution

pytest's `@pytest.mark.parametrize` decorator runs a single test function with multiple input sets. Each combination is a separate test case with its own pass/fail result.

**Basic parametrize for input/output pairs.**

```python
@pytest.mark.parametrize("email,expected_valid", [
    ("user@example.com", True),
    ("user@example", False),
    ("", False),
    ("@example.com", False),
    ("user+tag@example.com", True),
])
def test_email_validation(email, expected_valid):
    assert validate_email(email) == expected_valid
```

**Load test data from external files for large datasets.**

When a test needs dozens or hundreds of cases, embed them in a JSON or CSV file and load them as fixture parameters. This keeps test code clean and makes data easy to update without touching the test.

```python
def load_test_cases(filename):
    with open(f"tests/data/{filename}") as f:
        return json.load(f)

@pytest.mark.parametrize("case", load_test_cases("search_cases.json"))
def test_search(case, search_client):
    results = search_client.search(case["query"])
    assert results.total >= case["min_expected_results"]
```

**Use `ids` to make test output readable.**

By default, parametrize generates test IDs from the parameter values. For complex objects, provide explicit IDs so failing test output is immediately interpretable.

```python
@pytest.mark.parametrize("user_type,expected_role", [
    ("admin", "ADMIN"),
    ("subscriber", "USER"),
    ("trial", "LIMITED"),
], ids=["admin-user", "subscriber", "trial-user"])
def test_user_role_assignment(user_type, expected_role):
    user = create_user(type=user_type)
    assert user.role == expected_role
```

## Real-world example

An API test suite had 40 separate test functions for input validation — one per invalid input case. When the validation logic changed, all 40 functions needed updating. After converting to parametrize with an external data file, the same coverage was expressed in one function and one data file. The next validation change required editing the data file only.

## Key takeaways

- `parametrize` eliminates repetitive test functions while preserving individual pass/fail results
- External data files are appropriate when test cases number in the dozens or hundreds
- Use `ids` to make test output readable — cryptic IDs make debugging slower
- Data-driven tests are easy to extend; adding a case requires only a new data entry
- Keep parametrize inputs simple — complex setup logic belongs in fixtures, not parameter lists
