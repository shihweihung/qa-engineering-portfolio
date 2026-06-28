# Python & Pytest

Python is my primary language for test automation. I've used it to build mobile automation frameworks (via Appium), API test suites, and utility tooling that supports QA workflows.

---

## How I Use It

**Test structure with pytest**

I write tests using pytest because its fixture system is significantly better than `unittest` for the kind of test setup that's common in real projects — shared API clients, authenticated sessions, test data that needs to be set up and torn down cleanly.

I use fixtures to make test dependencies explicit. A test that needs an authenticated user requests an `authenticated_user` fixture, not a base class with a `setUp` method that does five other things besides authentication.

**Parametrize for coverage at scale**

When I need to verify the same behavior across many inputs — validation rules, boundary values, error conditions — I use `@pytest.mark.parametrize` rather than writing duplicate test functions. The output is cleaner, the test count is accurate, and adding a new case is a one-line change.

**Fixture scope for expensive setup**

A database connection or an authenticated API session shouldn't be created once per test. I use `scope="session"` for expensive setup that's safe to share across tests, and `scope="function"` (the default) for anything with state that needs to be isolated per test.

**Custom markers for targeted runs**

I tag tests with markers — `@pytest.mark.critical`, `@pytest.mark.regression`, `@pytest.mark.slow` — so CI can run targeted subsets. A pre-merge pipeline runs only critical tests. A nightly run covers everything.

---

## What I've Built

- A shared Appium automation framework for iOS/Android with pytest as the test runner and fixture layer
- API test suites against REST services using `requests` and `pytest`
- Utility scripts for test data generation, log parsing, and release validation

---

## Where I'm Developing

Python is not my strongest language — I'm more confident in test engineering than in software engineering. I can read and write code, but I'm more deliberate about things like error handling and code structure than an experienced developer would be.

I've been using AI tools to help with the more complex coding problems, and treating those interactions as a way to build my understanding alongside getting the work done.
