# Automation Framework Adoption Across Teams

## Context

A cross-regional QA team is evaluating automation frameworks for a mobile app undergoing a full rewrite in Kotlin. The client has stated a clear goal: all existing manual test cases (approximately 1000) should eventually be covered by automation, with the intention of reducing release cycle time.

Two candidate frameworks are on the table, each backed by a different regional team:

**Framework A — Local team**

- Built on Python and pytest
- Already in active use; existing test cases are written in this style
- Claims fast applicability to the new app
- Reportedly 100+ cases written over several years
- Single-device execution by default; parallel or multi-device support would require additional infrastructure

**Framework B — Overseas team**

- BDD-based (Gherkin/Cucumber style)
- Existing manual test cases can map directly to feature files
- CI integration already in place (Jenkins)
- Claims multi-platform support across iOS and Android
- The overseas team asserts it is already production-ready

## The real decision criteria

When evaluating automation frameworks at scale, the right questions are:

**1. Which framework can realistically cover 1000 cases?**

BDD has a structural advantage here. Gherkin scenarios are written in natural language, which means QA engineers without deep coding skills can contribute. Manual test cases can be translated into feature files systematically. This lowers the barrier to scale.

A pytest-based framework is more flexible and better suited for complex technical scenarios, but it requires programming competence to maintain. Scaling to 1000 cases with a small automation team is a significant commitment.

**2. What is the actual coverage today?**

If an existing framework has produced 100+ cases over several years with a dedicated team, that is a meaningful signal about sustainable throughput. Any projection that the same team can rapidly scale to 1000 cases with the same approach deserves scrutiny.

**3. Can it run across iOS, Android, and other device types?**

This is a hard requirement if the product targets multiple platforms. Appium-based frameworks support cross-platform execution in principle, but real-device testing introduces provisioning complexity. Both frameworks need to answer this concretely, not theoretically.

**4. What happens when the app changes?**

The app is being rewritten. That means locators, flows, and APIs will change. The framework with lower maintenance cost per case change will win in the long run. BDD feature files tend to be more readable and easier for non-authors to update. Pytest code can become brittle if not structured well.

## Recommendation

If the stated goal is to cover a large volume of manual test cases with a mixed-skill team in a reasonable timeframe, BDD is the stronger choice. The Gherkin layer reduces the dependency on individual automation engineers and makes test cases more durable as the underlying app changes.

A pytest framework is not wrong — it is better suited for API testing, performance testing, and cases requiring complex logic. A hybrid approach is worth considering: BDD for functional regression coverage, pytest for technical and integration tests.

The question of who builds and owns the framework should follow the technical decision, not precede it.

## What this situation reveals

Framework debates often reflect organizational dynamics more than technical ones. Signs that a framework decision has become political rather than technical:

- Teams advocate for their own solution without objectively evaluating the alternative
- Arguments shift to implementation speed ("we can do it faster") rather than long-term maintainability
- Decision makers avoid committing because they are managing relationships, not the problem
- The client's actual requirement (reduce release time, cover more cases) gets lost in the debate

The most useful intervention is to reframe the conversation around the client's measurable goal: how many cases can be reliably automated per sprint, and which framework gets there faster without creating unsustainable maintenance debt?

That is the question worth answering.
