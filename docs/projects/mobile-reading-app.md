# Mobile Reading App

## Situation

I was the QA lead for a cross-platform reading application that ran on iOS, Android, and a line of dedicated e-ink hardware devices. The app handled content delivery, user accounts, library management, and an in-app purchase flow.

The product was under active development, with a distributed engineering team and a release cadence of every few weeks. The QA process when I joined was primarily manual, with limited automation and no consistent test strategy.

---

## Challenge

The product complexity was significant: three distinct platforms with meaningfully different behavior, a content delivery pipeline with its own failure modes, purchase flows integrated with a third-party payment provider, and a user base that included both casual readers and heavy users with large libraries.

The key challenges were:

**Coverage without capacity.** Testing three platforms thoroughly on a compressed sprint cycle wasn't possible with a small team. I needed a coverage strategy that was honest about what was being tested and what wasn't.

**Platform-specific behavior.** The same feature behaved differently on iOS, Android, and e-ink devices in ways that weren't always documented. Finding these divergences before users did required deliberate cross-platform testing habits.

**No automation foundation.** When I took over the QA role, there was minimal automation. Every regression cycle was manual. This was unsustainable as the product grew.

**App rewrite mid-lifecycle.** During my time on the project, engineering began rewriting the app in a new technology stack. That meant automation written for the current app would need to be rebuilt — which changed how and what I chose to automate.

---

## My Role

I was responsible for the full QA lifecycle: test strategy, sprint test planning, regression coverage, automation roadmap, release readiness, and stakeholder communication on quality status.

I also worked directly with the engineering team on testability — catching requirements gaps early, flagging features that would be difficult to test without additional hooks or observability, and advocating for quality practices that reduced the number of bugs that reached QA in the first place.

---

## Solution

**Risk-tiered test coverage.** I built a coverage framework based on failure impact and frequency. Critical flows — authentication, purchase, core reading functionality — got full regression every release. Secondary features got spot-checked. Minor UI elements were covered incidentally or not at all. This was documented and shared with the team.

**Cross-platform test discipline.** I established a habit of testing key scenarios on all three platforms, not just the primary one. Even when a ticket was iOS-only, I'd spot-check the same scenario on Android if the underlying code was shared. This caught several divergence bugs before release.

**Automation for high-frequency regression.** I prioritized automation on the scenarios we ran every sprint without fail — login, content load, library operations. Starting there gave the most immediate payback and built team confidence in the automation.

**Clear release criteria.** I introduced explicit release criteria at the start of each sprint: what must pass, what severity of issue can be deferred, what a blocker looks like. This made the end-of-sprint release conversation factual rather than subjective.

---

## Outcome

Test coverage on critical flows became consistent. Release decisions moved from judgment calls to documented criteria. Automation coverage on regression-priority scenarios reduced manual regression time meaningfully. Platform-specific issues that had previously reached production were being caught in QA.

The larger shift was cultural: the team started thinking about testability during development, not after. Requirements reviews surfaced edge cases earlier, and quality became a shared concern rather than a QA-only concern.

---

## Lessons Learned

Three platforms means three times the surface area and roughly three times the ways something can break differently. The answer isn't testing everything on everything — it's being very deliberate about which scenarios get cross-platform coverage and why, and making that decision visible to the team.

App rewrites are a forcing function for automation strategy. If you're building automation on an app that's being rewritten, the ROI calculation changes significantly. I learned to balance short-term coverage needs against longer-term framework investment based on the stability of what I was testing.
