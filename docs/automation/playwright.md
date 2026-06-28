# Playwright

I use Playwright for web automation. My experience includes building test suites with Page Object patterns, handling async UI reliably, and integrating with CI pipelines.

---

## How I Use It

**Reliable async handling**

The biggest practical challenge with Playwright (and web automation generally) is writing tests that wait for the right thing rather than waiting for a fixed amount of time. I use Playwright's `expect()` assertions — which retry automatically — rather than fixed sleeps. When a UI change is driven by a network request, I wait on the network event directly using `expect_response`.

This eliminates the most common source of flakiness in web automation: tests that fail because the page hadn't finished loading when the assertion ran.

**Page Object patterns**

I structure Playwright tests with page objects that encapsulate locators and interactions, exposing user-facing methods rather than DOM details. A page object exposes `search(query)` and `get_result_count()` — the test doesn't need to know what element IDs are involved.

The benefit is maintenance: when locators change (and they always do), I update one file rather than hunting through every test that uses those elements.

**Locator strategy**

I prefer `data-testid` attributes over CSS selectors or text-based locators. They're stable across refactors, consistent across browsers, and communicate intent clearly. I work with engineering teams to add `data-testid` attributes to elements that automation needs to interact with.

**CI integration**

Playwright tests run headless in GitHub Actions. I configure them to capture screenshots and traces on failure, which makes debugging CI failures significantly faster than parsing log output alone.

---

## What I've Built

- E2E test suites for web application features using Playwright and Python
- Page object libraries for reuse across multiple test files
- CI pipeline integration with artifact capture on failure

---

## Honest Assessment

Web automation is more stable than mobile automation in my experience, but it's not without complexity — especially on products with heavy JavaScript rendering, complex routing, or frequent front-end changes. I've had to investigate and fix flakiness in Playwright suites, and that investigation experience is as valuable as the initial build.
