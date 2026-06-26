# Cross-Browser Reliability

## Problem

Playwright supports Chromium, Firefox, and WebKit, but running the same test across all three does not automatically produce consistent results. Browser engines handle timing, CSS rendering, and JavaScript behavior differently. A test that passes on Chromium may fail on WebKit because of a subtle rendering difference or a timing edge case that only surfaces on slower execution.

The result: teams either run tests on a single browser (lower confidence) or run them on all three and spend significant time investigating failures that are test-environment issues, not product bugs.

## Solution

Cross-browser reliability requires deliberate decisions about what to test across browsers, how to write tests that tolerate browser differences, and how to triage browser-specific failures.

**Test product behavior, not browser rendering.** Most product logic is identical across browsers. The question "does this API call succeed" has the same answer in Chromium and Firefox. The question "does this element look correct" may not. Focus cross-browser execution on behavior tests; reserve visual assertion tests for a single baseline browser.

**Use `data-testid` attributes as locators.** CSS selectors and text-based locators are more likely to behave differently across browsers due to rendering differences. `data-testid` attributes are set explicitly by the application and behave identically in all engines.

**Set consistent timeouts and avoid timing assumptions.** Firefox and WebKit typically execute JavaScript more slowly than Chromium in test environments. Tests with tight timing assumptions fail on slower engines. Use Playwright's auto-waiting mechanisms rather than time-based assumptions.

**Tag browser-specific failures explicitly.** When a test fails on one browser but not others, document the failure as browser-specific before investigating. This avoids spending time on a WebKit rendering quirk that does not affect users of a Chromium-based product.

## Real-world example

A team enabled all three browsers in CI and immediately saw 15–20% of tests failing on WebKit. Most failures were not product bugs — they were tests using `page.wait_for_timeout()` with values tuned for Chromium's speed. WebKit execution was slower, so tests timed out before the UI finished rendering.

Replacing fixed timeouts with `expect()` assertions eliminated 80% of the browser-specific failures without changing any product code. The remaining failures were genuine cross-browser issues worth investigating.

## Key takeaways

- Run behavior tests across browsers; limit visual assertions to a single baseline browser
- `data-testid` locators are more reliable than CSS selectors or text across browser engines
- Avoid fixed `wait_for_timeout()` calls — use auto-waiting assertions instead
- Triage browser-specific failures separately from product failures
- WebKit is typically slowest in CI environments; calibrate global timeouts accordingly
