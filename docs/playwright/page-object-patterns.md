# Page Object Patterns

## Problem

Playwright tests that interact with the UI directly — inline locators, repeated `page.locator()` calls scattered across test files — become difficult to maintain as the product grows. When a locator changes, it breaks every test that uses it. When a flow changes, it requires edits across multiple files.

The immediate pain is the cost of maintenance. The deeper problem is that tight coupling between test logic and implementation detail makes tests fragile by design.

## Solution

Page objects encapsulate the locators and interactions for a specific UI surface, exposing a high-level interface that tests can use without knowing how the UI is implemented.

**Structure page objects around user actions, not DOM elements.**

A well-designed page object exposes methods like `search(query)` and `get_results()`, not `fill_input_with_id_search()`. Tests read like user behavior; locators are implementation details hidden inside the page object.

```python
class SearchPage:
    def __init__(self, page):
        self._page = page
        self._search_input = page.locator('[data-testid="search-input"]')
        self._search_button = page.locator('[data-testid="search-button"]')
        self._results = page.locator('[data-testid="result-item"]')

    async def search(self, query: str):
        await self._search_input.fill(query)
        async with self._page.expect_response(lambda r: "/api/search" in r.url):
            await self._search_button.click()

    async def get_result_count(self) -> int:
        return await self._results.count()
```

**Keep page objects free of assertions.**

Page objects return data and perform actions. Assertions belong in the test. This separation keeps page objects reusable across tests with different expected outcomes.

**Use fixtures to provide page object instances.**

pytest fixtures initialize and inject page objects, so tests do not manage setup manually.

```python
@pytest.fixture
async def search_page(page):
    return SearchPage(page)

async def test_search_returns_results(search_page):
    await search_page.search("example query")
    assert await search_page.get_result_count() > 0
```

## Real-world example

A test suite for a content platform had 60 tests that all used inline locators. When the engineering team updated the data-testid attributes as part of a redesign, it broke 42 tests — each requiring individual updates.

After introducing page objects, locator changes required editing one file per page surface, not one file per test. The same redesign was absorbed in under an hour.

## Key takeaways

- Page objects encapsulate locators and interactions, shielding tests from implementation changes
- Expose user actions as methods, not DOM interactions
- Keep assertions out of page objects — they belong in the test
- Use fixtures to provide page object instances rather than constructing them in each test
- One page object per distinct UI surface; avoid one-size-fits-all base classes
