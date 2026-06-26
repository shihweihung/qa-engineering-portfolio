# Prompt Testing Strategies

## Problem

Products built on LLMs expose prompts as a core part of their behavior. A prompt change that improves one use case can degrade another. Prompt regressions are invisible without systematic testing — there is no compile-time check for "does this prompt still produce correct behavior."

## Solution

Treat prompts as versioned artifacts and test them with the same rigor as code.

**Define a prompt test suite.**

For each prompt in the product, maintain a set of test cases:

- Golden path inputs that should produce defined output characteristics
- Edge cases at the boundary of the prompt's intended scope
- Adversarial inputs that should trigger refusals or graceful degradation
- Previously failed inputs that caused production issues

**Use evaluation criteria, not exact match.**

Prompts produce different outputs on each run. Evaluation criteria should be:

- Structural (does the output contain required sections?)
- Behavioral (does it refuse when asked to do X?)
- Keyword-based (does it mention Y when given context about Z?)
- LLM-judged (is this response helpful/accurate/safe based on a rubric?)

**Run the suite on every prompt change.**

A prompt change without a test run is a deployment without tests. The suite may be small and fast — 20 cases running against the API takes under a minute. There is no reason not to run it.

**Track evaluation scores over time.**

A single evaluation run tells you the current state. A history of runs tells you whether the prompt is improving or degrading over time and which changes caused regressions.

## Real-world example

A team discovered that a prompt tuning session had introduced a regression on a specific question type — the model was producing a different output format than expected. The regression was not caught in code review because no prompt test suite existed.

After implementing a test suite with 30 cases and automated evaluation, subsequent prompt changes were validated before deployment. Three regressions were caught in the following two months before they reached users.

## Key takeaways

- Prompts are code; they deserve version control and automated testing
- Evaluation criteria should be deterministic checks or high-consistency LLM judgment — not exact match
- Include adversarial inputs in the test suite — refusal behavior is as important as happy path behavior
- Run the suite on every prompt change, not just major revisions
- Track scores over time to detect gradual degradation across prompt iterations
