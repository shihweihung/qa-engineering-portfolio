# QA Engineering Portfolio

**Senior QA / QA Lead / SDET**

A curated collection of practical articles, engineering decisions, and case studies from quality engineering work across mobile, web, and API products.

---

## Professional Summary

Quality engineer with experience leading QA for cross-platform products. Background spans test strategy, automation architecture, mobile testing (iOS and Android), and AI-assisted quality workflows. Comfortable as both a hands-on automation engineer and a team lead building quality culture from the ground up.

**Core skills:** Python · Playwright · Appium · pytest · CI/CD · API testing · AI-assisted testing · Team leadership

---

## Portfolio Categories

| Category | Focus |
|---|---|
| [Test Strategy](docs/test-strategy/) | Risk-based planning, coverage decisions, release readiness |
| [Playwright](docs/playwright/) | Web automation patterns, async UI, cross-browser reliability |
| [Appium & Mobile](docs/appium/) | iOS/Android architecture, device farms, mobile-specific challenges |
| [Python & Pytest](docs/python/) | Fixture design, data-driven testing, custom reporting |
| [API Testing](docs/api/) | Contract testing, automation patterns, response validation |
| [CI/CD Integration](docs/cicd/) | Pipeline design, parallel execution, flaky test management |
| [AI-Assisted Testing](docs/ai-testing/) | LLM test generation, testing AI products, AI-based maintenance |
| [Leadership](docs/leadership/) | QA culture, bug triage, team metrics, cross-team influence |
| [Defect Analysis](docs/defect-analysis/) | Root cause analysis, incident retrospectives, regression prevention |

---

## Featured Articles

- **[Risk-Based Testing in Practice](docs/test-strategy/risk-based-testing.md)** — How to prioritize coverage when you cannot test everything
- **[Handling Async UI in Playwright](docs/playwright/handling-async-ui.md)** — Reliable patterns for dynamic web interfaces
- **[Building QA Culture Without Authority](docs/leadership/building-qa-culture.md)** — Influencing quality as a lead, not a gatekeeper
- **[iOS and Android Shared Test Architecture](docs/appium/shared-architecture.md)** — One framework, two platforms
- **[Automation Framework Adoption Decisions](docs/notes/automation-framework-adoption.md)** — When technical choices become political

---

## Article Format

Every article follows the same structure:

1. **Problem** — What goes wrong, or why this decision is hard
2. **Solution** — The engineering approach
3. **Real-world example** — A generalized scenario with concrete detail
4. **Key takeaways** — What to remember and reuse

---

## Other Repositories

- **playwright-web-automation** — Production-grade Playwright framework with Page Object Model, CI integration, and parallel execution
- **appium-mobile-framework** — Shared iOS/Android test architecture using Appium and pytest
- **pytest-api-testing** — API test suite with contract testing, data-driven cases, and custom reporting

---

## Local Preview

```bash
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/mkdocs serve
```

Published site: `https://shihweihung.github.io/qa-interview-bible/`

*All examples are generalized. No confidential employer information is included.*
