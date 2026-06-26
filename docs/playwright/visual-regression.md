# Visual Regression Testing

## Problem

Functional tests verify that a feature works. They do not verify that it looks correct. A button that triggers the right API call but is invisible due to a CSS conflict passes all functional tests and ships broken.

Visual regressions are silent failures. They are introduced by unrelated changes — a dependency update, a global style refactor, a new component that overrides inherited styles — and are only caught when a human notices something looks wrong.

## Solution

Playwright's `expect(page).to_have_screenshot()` captures screenshots and compares them against stored baselines. Differences above a configurable threshold fail the test.

**Capture at the component level, not the full page.** Full-page screenshots are sensitive to any content change — including dynamic data, ads, or date-based content that changes legitimately. Component-level screenshots are more stable and more actionable.

```python
# Capture a specific component rather than the full page
await expect(page.locator('[data-testid="product-card"]')).to_have_screenshot(
    "product-card.png",
    max_diff_pixel_ratio=0.02  # allow up to 2% pixel difference
)
```

**Mask dynamic content.** User-specific data, timestamps, and randomly generated content should be masked before comparison to prevent false positives.

```python
await expect(page).to_have_screenshot(
    "dashboard.png",
    mask=[page.locator('[data-testid="user-name"]'), page.locator(".timestamp")]
)
```

**Update baselines intentionally, not automatically.** When a baseline update is required — because the design changed deliberately — it should be a conscious action, not an automatic one. Treat baseline updates like schema migrations: reviewed, committed, and traceable.

**Run visual tests on a fixed environment.** Font rendering, anti-aliasing, and pixel density differ across operating systems and display configurations. Visual tests that run on inconsistent environments produce noisy results. Fix the environment to a specific OS and resolution in CI.

## Real-world example

A design system update introduced a new spacing token that changed padding on all card components. Functional tests passed because the card content and interactions were unchanged. Visual tests caught 12 affected components immediately — before the change reached staging.

The fix took 20 minutes. Without visual testing, it would have been caught by a designer during a visual review, reported as a bug, triaged, and fixed across multiple components — a process that typically takes several days.

## Key takeaways

- Visual regression testing catches failures that functional tests cannot
- Capture at the component level rather than full-page to reduce noise
- Mask dynamic content to prevent false positives
- Update baselines intentionally — treat them like production artifacts, not throwaway screenshots
- Run visual tests on a fixed, consistent environment in CI
