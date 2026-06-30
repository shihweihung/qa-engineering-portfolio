# AI Resume Evaluation System

## Situation

I participated in the QA process for an AI-powered resume evaluation platform. The system allowed recruiters to upload resumes through a web interface or API, after which an AI model would analyze the content and return structured candidate evaluation data — extracted fields, skill assessments, and ranking scores.

The platform was being prepared for production use by recruiting teams. My role was to design the test strategy, execute functional and API testing, and identify gaps in how the system handled real-world resume diversity.

---

## Challenge

This project didn't fit the mold of traditional software QA. The core difficulty was that AI-generated outputs are non-deterministic — the same resume might produce slightly different scores or phrasing on different runs, and two reasonable outputs might look different without either being wrong.

That created a problem with the most basic QA assumption: what does "correct" mean here?

**No fixed expected results.** I couldn't write a test that said "this resume should score 82." I had to shift from exact-value validation to consistency and coverage checks — did the system extract the right fields? Did similar resumes produce similar rankings? Did the scores make sense against business expectations?

**Resume diversity as a test surface.** Real resumes vary enormously. Different layouts, PDF versus DOCX, missing sections, embedded tables, scanned images, multi-page documents, and widely varying writing styles all needed to work without crashing the system or silently producing garbage output.

**API reliability beyond status codes.** The API surface needed validation that went further than "did it return 200." Response structure, field mapping, null handling, authentication, error messages, and data consistency across calls were all in scope.

**Defining AI correctness without a ground truth.** The hardest part wasn't executing tests — it was deciding what the tests were trying to prove. With non-deterministic output, every assertion needed a rationale grounded in business expectation, not just technical specification.

---

## My Role

I was responsible for designing the test strategy from the ground up, executing functional and API test scenarios, and documenting findings in a way that the team could act on.

I also led the thinking on how to approach AI-specific validation — what questions to ask about scoring behavior, how to structure consistency checks, and how to communicate test results when "pass/fail" wasn't a clean binary.

---

## Solution

**Shifted from output validation to behavior validation.** Rather than checking for specific scores, I focused on whether the system behaved reliably: Did it always extract names, dates, and job titles? Did it rank an obviously stronger resume above a weaker one? Did it handle edge cases without crashing? These behavioral checks gave us meaningful signal without requiring a fixed expected output.

**Designed a resume test corpus.** I assembled a set of test resumes that covered the important variation axes: file formats, layouts, section completeness, length, and content quality. This gave regression testing a stable, repeatable foundation that covered the edge cases we cared about.

**Consistency testing over exact accuracy.** I ran the same resumes through the system multiple times and compared outputs. Score variation within a small range was acceptable; large swings or contradictory field extractions were not. This framing made the pass/fail criteria defensible.

**API validation depth.** Beyond basic response codes, I verified request validation behavior, authentication boundaries, response schema consistency, null and empty field handling, and error message accuracy. I also checked that data returned through the API matched what the UI displayed — surface-level consistency that's easy to miss.

**Documented evaluation principles.** Because the system would keep evolving, I wrote up the evaluation approach explicitly: what we were testing for, why exact-value assertions weren't appropriate, and what thresholds we'd use for consistency checks. This gave the team a framework to apply in future test cycles, not just a batch of one-time results.

---

## Outcome

We surfaced several meaningful issues: inconsistent field extraction for certain resume formats, score instability on edge-case inputs, and API error responses that didn't match the documented contract. None of these would have been caught by a simple functional checklist.

The evaluation principles document became the starting point for ongoing QA on the platform. The team had a clear rationale for why AI testing looks different from traditional software testing — and a practical approach to execute it.

---

## Lessons Learned

This project changed how I think about validation. In deterministic software, a wrong answer is obvious. In AI systems, the question is more nuanced: is the behavior consistent, is it aligned with business intent, and are failures caught before they matter to users?

A QA engineer working on AI products has to understand the business problem deeply enough to define what "good" looks like — and then build tests that verify that standard rather than a fixed output. That's a different skill than traditional test case writing, and it's one I came to value a lot through this work.
