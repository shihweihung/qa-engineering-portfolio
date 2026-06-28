# Release Readiness

## What It Actually Means

"Release readiness" sounds simple. In practice, it's one of the most negotiated concepts in software development.

The trap is treating it as a binary state — ready or not ready — when it's actually a risk assessment. The real question is: what is the risk profile of releasing now, and who is authorized to accept that risk?

---

## What I've Learned

**Define it before testing starts, not at the end.** Release criteria defined at the end of a cycle are defined by the current bug list. Criteria defined at the beginning are defined by quality standards. These produce different outcomes.

The approach I've pushed for: agree on release criteria in the sprint kickoff as a brief, explicit statement. "No open P1 bugs, regression suite passing, payment flow validated on real devices." When that standard is defined in advance, the release conversation is factual rather than negotiable.

**Distinguish between "ready" and "shippable."** Sometimes a team makes an explicit decision to ship with known issues — a P2 bug that's deferred to the next cycle, a feature that's partially complete, a known issue with a documented workaround. This is a legitimate business decision. The problem is when it's implicit: everyone knows there's a quality gap but nobody names it.

I've found it useful to make this distinction explicit. "We are shipping with two known issues. Here they are, here's their impact, here's the plan to resolve them." This documents the decision and keeps it out of the unspoken zone.

**QA doesn't decide.** QA's role in the release conversation is to provide accurate risk information. The decision about what risk is acceptable belongs to product and leadership. I've occasionally seen QA engineers refuse to sign off on a release as a form of influence. This is usually counterproductive — it conflates the risk assessment role with the decision-making role.

The more useful version: provide a clear picture of what's known, what's unknown, what was tested, and what wasn't. Then let the stakeholders with the authority to make the call make it.
