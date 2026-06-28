# QA Planning

## What Planning Actually Means

QA planning is not about writing a comprehensive test plan document. It's about making explicit decisions before the sprint starts: what will we test, what level of coverage is appropriate, what are the release criteria, and where are we accepting risk?

These decisions are engineering decisions. They should be informed by data, made transparently, and communicated to stakeholders — not left implicit until something breaks.

---

## How I Structure Test Planning

**Start with risk assessment.** Before deciding what to test, I identify what can go wrong and what the impact would be. Features that handle money, user data, or core functionality get more coverage depth. Stable areas with low change activity get lighter coverage.

**Define release criteria explicitly.** What does "ready to release" mean for this cycle? I've pushed teams to define this before testing starts, not at the end when the answer becomes negotiable. Criteria typically include: no open critical bugs, regression suite passing, specific high-risk scenarios validated on real devices.

**Communicate scope and gaps.** I tell stakeholders what is and isn't being tested and why. This keeps expectations accurate and gives stakeholders the information they need to make release decisions. A QA team that says "all clear" when it has only tested half the surface area is creating false confidence.

---

## Release Criteria in Practice

I've developed pre-sprint release criteria as a standing agreement with product and engineering. The format is simple:

- Blocker-level issues: zero open
- High-priority issues: agreed list reviewed and accepted or resolved
- Regression coverage: specified scenarios passing
- Device coverage: release validated on agreed representative devices

This makes the release decision explicit and keeps it out of last-minute negotiation.

---

## Adapting Plans When Reality Doesn't Cooperate

Sprint plans don't survive contact with reality. Features slip, bugs are found late, scope changes. The planning skill that matters in practice is knowing how to adjust coverage decisions under pressure and communicate those adjustments clearly.

When I've reduced test scope under time pressure, I've always done it explicitly — naming what isn't being tested and what risk that creates — rather than silently covering less and hoping nothing goes wrong.
