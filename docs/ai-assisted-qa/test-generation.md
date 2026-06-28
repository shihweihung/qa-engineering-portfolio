# Test Case Generation with AI

## What I Actually Do

When a new feature lands — or sometimes before it does — I use an AI assistant to draft a first pass at test cases. The workflow looks like this:

1. Paste the feature spec or user story into the prompt
2. Ask for test cases covering the happy path, main failure modes, edge cases, and boundary values
3. Review the output, prune duplicates, correct anything that's wrong about the domain, and add cases the AI missed
4. Use the result as the starting point for the test plan, not the final test plan

The time savings are real. A feature with 5-6 test scenarios might take 20-30 minutes to think through from scratch. With an AI draft to react to, I can cover the same ground in 5-10 minutes and usually end up with better coverage because the AI's suggestions prompt me to think about angles I might have skimmed.

---

## What Works

**Breadth coverage.** AI is good at generating comprehensive lists quickly — boundary values, error conditions, different user states, permission variations. The initial sweep is fast and catches many cases I would have gotten to anyway.

**Format translation.** If I have a bullet-point list of acceptance criteria and need it in a test case format (given/when/then or steps + expected result), AI handles that translation well.

**Parametrize inputs.** For data-driven test scenarios — email validation, input length limits, special character handling — AI generates a useful starting set of test inputs quickly.

---

## What Doesn't Work

**Domain-specific edge cases.** AI doesn't know about our specific data model, our specific user base, or the bugs we've seen before. The edge cases that come from domain knowledge and institutional memory still come from me.

**Correctness of expected results.** AI will generate expected results confidently that are simply wrong. The review step isn't optional — it's where the value is earned.

**Judgment about what matters.** AI doesn't know which test case is critical and which is low-value. Prioritization is still my job.

---

## Honest Assessment

AI-assisted test generation is a real productivity improvement for authorship work. It's not a shortcut that produces finished test plans — it's a way to get a better starting point faster.

The quality of the final test plan still depends on the engineer reviewing it. The AI is a fast first draft, not a replacement for thinking.
