# Automation Planning

## My Role in Automation

I've participated in automation planning discussions and framework evaluation throughout my career, but I haven't been the primary person building and shipping automation suites. My contribution has been on the strategy and decision side — what to automate, which framework to adopt, how to sequence the work — while implementation was typically owned by other team members or an offshore team.

This distinction matters. The thinking I describe below is genuine; the hands-on implementation experience is limited.

---

## What I've Contributed to Automation Discussions

**What's worth automating**

Not everything should be automated. In planning discussions, I've pushed for focusing automation on: high-frequency regressions that are tedious to run manually, critical user flows where missing a failure would be a serious problem, and stable areas where the investment pays off over time.

The common mistake I've seen is automating everything, including rapidly-changing UI and complex setup scenarios where the maintenance cost exceeds the value. Part of my contribution has been arguing for selectivity over volume.

**Framework evaluation**

I participated in a multi-month evaluation of BDD (Gherkin/Behave) versus Python pytest for a shared automation effort between teams. The discussion was as much about team dynamics and ownership as it was about technical merit — which team would maintain it, what their skill set was, whether the "readable tests" promise of BDD would actually be realized in practice. The outcome was pytest, and the reasoning is documented in the [projects section](../projects/automation-framework-decision.md).

**Communicating automation coverage to stakeholders**

Automation coverage is invisible unless you make it explicit. I've contributed to discussions about how to report what's automated, what that means for release confidence, and what still depends on manual testing.

---

## What I'm Learning

I'm currently building hands-on implementation skills — Python/pytest basics, Appium concepts, Playwright exploration — using AI tools to help me write and understand code. The goal is to make my strategy-level judgment more grounded in implementation reality.
