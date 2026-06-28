# Flaky Test Management

## The Actual Problem

A flaky test is a test that sometimes passes and sometimes fails for reasons unrelated to the code under test. The obvious fix is to make the test deterministic. The less obvious problem is that flaky tests undermine trust in the entire test suite — once engineers learn to ignore intermittent failures, they'll ignore real failures too.

---

## How I Think About It

**Flakiness is a spectrum.** A test that fails 1-in-100 runs is different from a test that fails 1-in-5. The appropriate response depends on the failure rate and the importance of what the test covers.

**Flakiness has causes, not just symptoms.** Common causes:
- Timing dependencies (waits that are too short or that depend on machine load)
- Test order dependencies (shared state that one test leaves dirty for the next)
- External dependencies (network calls, third-party APIs, time-based behavior)
- Race conditions in the product itself

Finding the cause usually requires running the test in isolation, with logging, and often multiple times. "I can't reproduce it" is not a diagnosis.

---

## What I've Done

**Quarantine, don't delete.** A flaky test that covers something real shouldn't be deleted — the coverage is still valuable. I've used skip markers and quarantine suites to separate flaky tests from the blocking CI suite while the underlying issue is investigated.

**Fix the root cause, not the symptom.** Adding a retry or increasing a timeout treats the symptom. These fixes are sometimes appropriate for tests that depend on inherently variable external resources, but they hide the actual problem for timing or state issues.

**Track the pattern.** A test that flakes in CI but never locally usually indicates a timing or resource issue specific to the CI environment. A test that flakes everywhere usually indicates a product-level race condition or a test design problem.

---

## The Honest Reality

Some flakiness in a large suite is probably unavoidable, especially for end-to-end mobile or UI tests. The goal isn't zero flakiness — it's keeping flakiness rates low enough that the suite remains trustworthy, and having a clear process for investigating and resolving individual failures.
