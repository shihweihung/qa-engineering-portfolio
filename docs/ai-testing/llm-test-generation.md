# LLM Test Generation

## Problem

Writing test cases is time-consuming, especially for large feature surfaces with many input combinations. QA engineers spend significant time on test case authorship that could be spent on exploratory testing, risk analysis, and test infrastructure.

LLMs can generate test case drafts at scale — but generated tests require review, often miss domain-specific edge cases, and can produce tests that pass without actually testing the right behavior.

## Solution

Use LLMs as a first-draft accelerator, not a replacement for judgment.

**Effective uses:**

- Generating a comprehensive list of test cases for a specified feature, which QA then reviews, prunes, and supplements
- Converting manual test case descriptions into test code skeletons
- Generating boundary value and equivalence class test inputs for data validation scenarios
- Drafting test data sets for parametrized tests

**Prompt structure that produces useful output:**

Provide the feature specification, the expected behaviors, and the format you want. Vague prompts produce generic tests; specific prompts produce actionable drafts.

```
Generate pytest test cases for a user registration endpoint with the following rules:
- Email must be unique and in valid format
- Password must be 8+ characters, one uppercase, one number
- Username is optional, max 30 characters
- Returns 201 on success with user ID and email
- Returns 400 with field-specific error messages on validation failure

Format: pytest functions using AAA structure, no mocks, using an APIClient class.
```

**Review generated output before committing.**

Generated tests frequently:
- Test the same boundary twice with different names
- Miss domain-specific edge cases the LLM has no context for
- Include assertions on implementation details rather than behavior
- Generate plausible-looking but incorrect expected values

Treat LLM output as a draft that saves 60% of the authorship time, not a finished product.

## Real-world example

A QA engineer used LLM generation for a 15-field form validation feature. The LLM produced 40 test case drafts in 3 minutes. Manual review removed 8 duplicates, corrected 4 incorrect expected values, and added 6 domain-specific edge cases that the LLM had no context for. The final suite of 34 tests was ready in 45 minutes rather than an estimated 4 hours.

## Key takeaways

- LLMs accelerate test authorship but do not replace QA judgment
- Specific prompts with feature specifications produce actionable drafts; vague prompts produce generic tests
- Always review generated tests for correctness, duplication, and missing domain knowledge
- LLMs are better at breadth (covering many combinations) than depth (catching subtle domain edge cases)
- Measure value by time saved on authorship, not by number of tests generated
