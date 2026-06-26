# API Testing

Automated validation for backend services.

API tests are fast, reliable, and not tied to UI rendering. They belong close to the service boundary, run in CI on every commit, and catch integration failures before they become user-visible bugs. These articles cover the patterns that make API test suites durable over time.

## Articles

- **[Contract Testing](contract-testing.md)** — Verifying that producer and consumer APIs stay in sync without end-to-end tests
- **[API Automation Patterns](automation-patterns.md)** — Structuring API tests for maintainability and coverage
- **[Response Validation](response-validation.md)** — Beyond status codes: schema validation, data consistency, and error handling
