# Testing AI Products

## Problem

Traditional QA assumes deterministic behavior: given the same input, the system produces the same output. AI systems — particularly those powered by LLMs — do not behave this way. The same prompt can produce different responses. The "right" response is often subjective. Test cases that fail intermittently cannot be easily distinguished from genuine regressions.

Standard pass/fail test frameworks are the wrong tool for AI product quality.

## Solution

Testing AI products requires a different mental model: instead of verifying exact outputs, verify that outputs meet defined quality criteria with sufficient consistency.

**Define quality dimensions explicitly.**

Before writing any tests, define what "correct" means for the AI behavior under test:

- **Factual accuracy** — Does the output contain verifiable claims? Are they true?
- **Format compliance** — Does the output match the expected structure (JSON, markdown, length)?
- **Behavioral boundaries** — Does the system refuse appropriately? Does it respond when it should?
- **Tone and safety** — Does the output meet content policy requirements?

**Test with a large enough sample to detect regressions.**

A single prompt run does not tell you whether behavior changed. Run each test case multiple times and define a threshold: "this behavior must occur in at least 90% of runs" or "this refusal must occur in at least 95% of runs."

**Use LLM-as-judge for subjective quality evaluation.**

For outputs that cannot be evaluated with string matching — tone, helpfulness, coherence — use a second LLM to evaluate the output against a rubric. This is not perfect, but it scales and provides more consistent signal than human review for high-volume test runs.

**Maintain a regression set of known-good and known-bad examples.**

As the model or prompts change, run the same inputs and compare outputs. Significant drift from known-good outputs is a regression signal even when you cannot define exactly what the "correct" output is.

## Real-world example

A team shipping a conversational feature found that prompt changes intended to improve tone were also reducing accuracy — the model was hedging more and sometimes giving wrong information to avoid appearing confident. Standard unit tests could not catch this.

After implementing an LLM-as-judge evaluation that scored each response on accuracy (factual) and appropriateness (tone) separately, they could see the trade-off clearly and tune the prompt to improve tone without sacrificing accuracy.

## Key takeaways

- AI product testing requires probabilistic thresholds, not binary pass/fail
- Define quality dimensions before writing tests — "does it work" is not a testable criterion
- Sample-based testing (run N times, pass if X% meet criteria) handles non-determinism correctly
- LLM-as-judge provides scalable evaluation for subjective quality dimensions
- Maintain regression examples: known-good and known-bad inputs that must remain stable across model changes
