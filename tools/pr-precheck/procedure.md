# PR Precheck Procedure

## Read Order
1. Read `scope.md` in live mode to verify repository access and prevent unauthorized checks.
2. Read `plan.md` including any deviation notes, alongside the assigned GitHub issue description.
3. Read the draft PR title and body from `pr_draft.md` and the test results from `test_evidence.md`.
4. Read the repository's pull request template (`.github/PULL_REQUEST_TEMPLATE.md`) and contribution guidelines (`docs/CONTRIBUTING.md`).

## Evidence Gathering
1. Extract the full branch diff using `git diff main...HEAD` to inspect all code changes.
2. Collect test execution logs from `test_evidence.md`, verifying that unit tests, lints, and type checks were run honestly without hidden suppressions or unresolved xfail markers.
3. Review every section of the draft PR description against the required template fields and AI-use disclosure standards.

## Check Execution
1. Compare the code diff side-by-side against `plan.md` to ensure no silent drift or undocumented features were introduced.
2. Evaluate test evidence and reproduction outcomes to confirm all core requirements are fully tested and passing.
3. Inspect formatting, linter output, and PR template completeness against repository standards.

## Verdict Assembly
1. Grade each rubric check as `pass`, `fail`, or `unclear`, providing a strict one-line evidence quote or fact for every grade.
2. Apply the verdict rule: output `accept` if all required checks pass, or `reject` if any check fails or is unclear.
3. Output the final result ending with the exact required JSON block and nothing else.

## Eval Mode Mapping
In eval mode there are no separate files. Map them to sections of the bundle text:
- `plan.md` = "Plan context"
- `pr_draft.md` = "Candidate PR" (Title, Description, Commits)
- `test_evidence.md` = "Test evidence"
- the diff = "Diff"
- repo template and CONTRIBUTING.md = "Repo facts"
Do not penalize a bundle because a file named above is absent. Never require `make lint`, `make typecheck`, or an AI disclosure unless "Repo facts" states it.
