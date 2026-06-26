# Shared iOS/Android Test Architecture

## Problem

Mobile apps that target both iOS and Android need test coverage on both platforms. The naive approach is two separate test suites: one for iOS, one for Android. This doubles the maintenance burden and creates divergence over time — tests get added to one platform but not the other, bugs get fixed in one suite but not both.

The challenge is that iOS and Android behave differently enough that a single test written identically for both will fail on one platform in unexpected ways — but similar enough that rewriting everything twice is wasteful.

## Solution

The architecture that balances reuse with platform flexibility has three layers:

**1. Shared test logic (platform-agnostic).**

Test scenarios — what to do and what to verify — are written once. Business logic does not know it is running on iOS or Android.

```python
# test_search.py — runs on both platforms
async def test_search_returns_results(app):
    await app.search("example query")
    results = await app.get_search_results()
    assert len(results) > 0
```

**2. Platform-specific page objects.**

Each page object has an iOS and Android implementation. The shared test calls `app.search()` and the correct implementation is injected at runtime based on the target platform.

```python
class IOSSearchPage:
    async def search(self, query: str):
        await self._driver.find_element(
            AppiumBy.ACCESSIBILITY_ID, "search_field"
        ).send_keys(query)

class AndroidSearchPage:
    async def search(self, query: str):
        await self._driver.find_element(
            AppiumBy.ID, "com.example.app:id/search_input"
        ).send_keys(query)
```

**3. Platform-aware fixtures.**

A fixture reads the target platform from the environment or config and returns the correct implementation.

```python
@pytest.fixture
def app(driver, platform):
    if platform == "ios":
        return IOSApp(driver)
    return AndroidApp(driver)
```

## Real-world example

A cross-platform team maintained two separate test suites that had diverged over 18 months. iOS had 120 tests, Android had 85 — different scenarios, different assertions, different levels of reliability.

After consolidating to a shared architecture, the team maintained 110 shared scenarios with platform-specific locator implementations. New tests were written once. Platform-specific bugs were handled in the page object layer, not the test layer.

## Key takeaways

- Separate test logic (what to do) from platform implementation (how to do it)
- Page objects are the right place to absorb platform differences, not the test files themselves
- Fixtures handle platform selection — tests should not know which platform they are running on
- A shared test suite is not the same as identical locators; expect different element identifiers per platform
- Start with shared architecture on day one — retrofitting is significantly more expensive
