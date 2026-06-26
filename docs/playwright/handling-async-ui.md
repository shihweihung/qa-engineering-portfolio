# Handling Async UI in Playwright

## Problem

Modern web interfaces are asynchronous. Data loads in the background, elements appear after animations, network requests complete at unpredictable times, and state changes trigger cascading UI updates.

Automation that does not account for this becomes flaky. Tests that pass locally fail in CI because CI machines are slower. Tests that pass in isolation fail under parallel execution because shared state settles at different times.

The naive fix — adding `sleep()` calls — makes tests slower without eliminating the underlying race condition.

## Solution

Playwright's built-in waiting mechanisms handle most async UI scenarios without manual sleeps. The key is knowing which mechanism applies to which situation.

**Use `expect(locator)` assertions for element state.**

Playwright's `expect` assertions automatically retry until the timeout is reached. This handles elements that appear after a network request or animation without any manual waiting.

```python
# Waits up to the configured timeout for the element to be visible
await expect(page.locator('[data-testid="result-list"]')).to_be_visible()

# Waits for text content to match
await expect(page.locator('[data-testid="status"]')).to_have_text("Complete")
```

**Use `wait_for_selector` with a state argument for conditional elements.**

When an element may or may not appear depending on product state, target the state explicitly rather than assuming presence.

```python
# Waits for element to appear and be visible
await page.wait_for_selector(".notification-banner", state="visible")

# Waits for loading spinner to disappear
await page.wait_for_selector(".loading-spinner", state="hidden")
```

**Use `expect_response` for network-dependent UI.**

When a UI change is triggered by a network request completing, wait on the network event directly rather than guessing elapsed time.

```python
async with page.expect_response(
    lambda r: "/api/search" in r.url and r.status == 200
) as response_info:
    await page.locator('[data-testid="search-button"]').click()

await response_info.value  # ensures request completed before proceeding
await expect(page.locator('[data-testid="result-item"]').first).to_be_visible()
```

**Avoid `page.wait_for_timeout()` in committed tests.**

`wait_for_timeout` is a fixed sleep. It does not adapt to fast environments and does not retry on failure. Use it only during debugging — never in a test that gets committed.

**Set timeouts at the right scope.**

Set a reasonable global default, tighten for assertions that should be fast, and expand only for known slow operations.

```python
# playwright.config.py
expect_timeout = 10_000  # 10 seconds — global default for expect() assertions
```

## Real-world example

A search results page loads results via an API call after the user submits a query. The results container exists in the DOM immediately but is empty until the response arrives.

A flaky version:

```python
await page.locator('[data-testid="search-input"]').fill("example query")
await page.locator('[data-testid="search-button"]').click()
# Flaky: results may not have loaded yet
results = await page.locator('[data-testid="result-item"]').all()
assert len(results) > 0
```

A reliable version:

```python
await page.locator('[data-testid="search-input"]').fill("example query")

async with page.expect_response(
    lambda r: "/api/search" in r.url and r.status == 200
):
    await page.locator('[data-testid="search-button"]').click()

await expect(page.locator('[data-testid="result-item"]').first).to_be_visible()
results = await page.locator('[data-testid="result-item"]').all()
assert len(results) > 0
```

The second version ties the assertion to a real event — the API response — rather than elapsed time. It passes consistently across environments regardless of machine speed or network latency.

## Key takeaways

- Playwright's `expect` assertions retry automatically — use them instead of assertion + sleep
- Wait on network events when UI changes are driven by API responses
- `wait_for_selector` with a `state` argument handles elements that appear or disappear conditionally
- Never use `wait_for_timeout` in committed tests — it hides flakiness instead of eliminating it
- Set global timeouts to enforce a baseline; override locally only for known outliers
