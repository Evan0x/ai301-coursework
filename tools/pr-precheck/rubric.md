# PR Precheck Rubric

## Core Failure Modes
1. **Silent Drift:** The diff goes beyond the approved plan (extra files, extra behavior) without a documented deviation.
2. **Not Tested:** No test evidence, tests skipped or suppressed, or the plan's test plan was not run.
3. **Unreviewable:** The PR description is missing, does not link the issue, or the diff is too tangled to review.
4. **Standards Wall:** The PR violates a requirement that the repo itself states (PR template, CONTRIBUTING.md, AI policy).

## Grading Principle
Judge every check against the package's "Repo facts" section, not against a fixed list of commands. A requirement the repo does not state (for example an AI policy, `make lint`, or `make typecheck`) can never be failed or marked unclear.
- **pass:** the evidence meets the pass condition.
- **fail:** the bundle shows an affirmative violation (diff outside the plan's files, failing or suppressed test, missing template item the repo requires, stated policy broken).
- **unclear:** the bundle genuinely lacks information that the repo facts say is required.

## Test Evidence Principle
Test Execution is `fail` when the evidence only asserts that testing happened. A pass needs observable results: pasted output, a before/after comparison, or a named test with its result. If the plan lists a repro, a unit test and a control case, each must appear. A missing step is `fail`, not `unclear`.

## Check Table
| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Plan Compliance | Diff vs. plan context | Diff touches only the plan's named files and behavior; no extra scope | required |
| Test Execution | Test evidence section vs. the plan test plan | Each step of the plan test plan is addressed with a specific, checkable result: the observed before/after behavior, the named test and that it passed, or the control case outcome. Prose is fine if it is specific. A generic claim with nothing checkable (tested locally, works; cargo test passes) does not count. No skipped, xfailed or suppressed tests. | required |
| PR Description | Candidate PR description vs. Repo facts template | Links the issue, summarizes the change, and addresses each item in the repo's PR template | required |
| Standards Compliance | Repo facts (template checklist, CONTRIBUTING.md) | Every requirement the repo states is addressed; no stated requirement is violated | required |

## Verdict Rule
- **Reject** if any required check is `fail`.
- **`unclear`** is rejected only when the missing evidence is something the repo facts explicitly require. Absence of an unrequired artifact is `pass`.
- **Accept** otherwise.
