# Mobile Automation Framework

## Situation

The mobile product I was working on had no meaningful automation when I began building out QA infrastructure. Manual regression was taking several days per release cycle, and the team was growing. The regression burden wasn't going to shrink on its own.

The product ran on iOS and Android, which meant whatever framework I built had to support both platforms without duplicating test logic.

---

## Challenge

**Starting from nothing.** There was no existing automation infrastructure, no established patterns, and no prior investment to build on. Every decision about architecture and tooling was mine to make — and the wrong decisions at this stage would be expensive to undo later.

**Supporting two platforms.** iOS and Android use different element identifiers, different automation drivers in some cases, and different behaviors for platform-specific flows. A naive approach is to write two separate test suites. A better approach is to write test logic once and vary only the platform-specific implementation details.

**Practical automation speed.** I couldn't spend all my time on framework work — I still had sprint QA responsibilities. The framework had to reach a useful state quickly, cover the most important scenarios, and be maintainable by someone who wasn't the original author.

**App instability during the build phase.** I was building automation against an app that was actively in development. Locators changed, flows changed, and features that existed one sprint might be redesigned the next. Building automation during active development requires absorbing that instability gracefully.

---

## My Role

I designed the framework architecture, wrote the foundational code, and built the initial test scenarios. I also integrated the framework into CI, handled device provisioning, and documented the patterns so other team members could contribute.

---

## Solution

**Shared test logic, platform-specific locators.** I structured the framework so test scenarios (what to do and verify) were written once, and platform-specific implementation (how to find and interact with elements) was encapsulated in separate page object classes per platform. A pytest fixture handled platform selection at runtime based on configuration.

This meant adding a new test scenario required writing one file. Adding a new platform would require adding platform implementations to each existing page object, but not rewriting the tests themselves.

**Targeting stable elements.** Where possible, I worked with engineering to add accessibility identifiers to elements that tests needed to interact with. This made locators more stable than using UI hierarchy paths or coordinates, and the elements were less likely to break on UI changes.

**Simulator-first with real device runs pre-release.** Running on simulators was faster and easier for CI. I kept simulator runs in the CI pipeline for continuous feedback and reserved real device runs for pre-release validation, where hardware-specific behavior mattered more.

**Starting with the highest-value scenarios.** The first scenarios I automated were the ones we ran manually every sprint without fail: login, content load, library sync, and the core reading flow. These had the most obvious ROI and gave the team immediate evidence that the automation was working.

---

## Outcome

The automation framework reached useful coverage within a few sprints. The CI integration meant that regression failures on the critical flows were caught automatically. Manual regression time on covered scenarios dropped significantly.

The shared architecture proved its value when a UI change broke locators — I updated the page object once per affected element, and all tests that used that element continued to work. Before the shared architecture, the same change would have required hunting through individual test files.

---

## Lessons Learned

Start small and useful rather than comprehensive and ambitious. A framework that's running in CI covering 10 critical scenarios after two weeks is more valuable than a framework covering 100 scenarios that isn't stable or integrated after three months.

The decision about what to automate first matters as much as the framework design. I've seen automation projects stall because the first scenarios chosen were complex, flaky, or low-value — which killed team confidence in the automation before it had a chance to prove itself.
