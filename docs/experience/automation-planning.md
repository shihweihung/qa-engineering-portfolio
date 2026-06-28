# Automation Planning

## What I've Done

Automation planning is about deciding where automation investment will actually pay off — not just writing tests because automation is supposed to be good.

I've built automation roadmaps from early stages where there was no automation at all, through to established frameworks with CI integration. The decisions about what to automate, when, and how much to invest have been mine to make and defend.

---

## Responsibilities

**Identifying what's worth automating**

Not everything should be automated. The scenarios worth automating are: high-frequency regressions that are tedious to run manually, critical user flows where a failure would be embarrassing to miss, and stable features where the automation ROI improves over time.

The scenarios that are often not worth automating (at least early on): rapidly changing UI, features with complex setup requirements that make stable automation expensive, and edge cases that only manifest under very specific conditions.

**Sequencing the work**

When building an automation suite from scratch, sequencing matters. I start with the highest-risk, highest-frequency scenarios — the ones that provide value immediately and build team confidence in the framework. Complex, lower-value scenarios come later, after the infrastructure is proven.

**Framework selection and architecture**

Choosing a framework isn't just a technical decision. It also depends on who will maintain it, what the team's skill set is, and how much investment is realistic. I've been in situations where a simpler, lower-capability framework was the right choice because the team could actually maintain it, and a more powerful but complex framework would have been abandoned within a year.

**Communicating automation coverage to stakeholders**

Automation coverage is invisible to most stakeholders unless you make it visible. I report on what's automated, what that coverage means for release confidence, and what's still dependent on manual testing. That information shapes release decisions and helps product understand what they're getting from QA investment.

---

## Challenges

**Building automation while also doing manual testing**

Automation work competes with sprint work. Building good test infrastructure while also covering current sprint features is a capacity problem that doesn't go away. I've managed it by treating automation work as part of sprint planning — it goes on the board, gets estimated, and doesn't happen invisibly in the background.

**Keeping automation maintained as the product changes**

An automation suite that isn't maintained becomes a liability. I've seen suites that took significant engineering effort to build become useless in six months because no one owned keeping them current through product changes. I treat automation maintenance as a normal cost of development, not an exceptional task.

**Managing expectations about what automation does and doesn't guarantee**

Automated tests passing doesn't mean the product works. Stakeholders sometimes read a green CI build as "QA done." I try to be clear about what the automation covers and what still requires judgment — automated regression plus exploratory testing on new features is a different coverage level than automated regression alone.

---

## Lessons Learned

Automation is most valuable when it frees up QA time for the work that can't be automated — exploratory testing, judgment calls, cross-platform comparison, and catching the things that don't fit a predefined scenario.

The worst automation investments I've seen were driven by the goal of high test counts rather than by the goal of useful signal. More tests is not always better. Reliable, fast, meaningful tests are better.
