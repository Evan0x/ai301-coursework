# Evidence Guide

## 1. Plan and Scope Evidence
- **Practice Submission:** Found in the bundle description or plan file.
- **Your PR:** Found in `plan.md` and branch commit history.
- **Good Looks Like:** Clear mapping from issue requirements to planned implementation steps without undocumented drift.

## 2. Code Diff Evidence
- **Practice Submission:** Diff section in the package bundle.
- **Your PR:** Output of `git diff main...HEAD`.
- **Good Looks Like:** Clean changes matching the plan with no debugging debris or unrelated refactoring.

## 3. Test Evidence
- **Practice Submission:** Test logs in the package bundle.
- **Your PR:** `test_evidence.md` containing `make test-unit`, `make lint`, `make typecheck`, and repro output.
- **Good Looks Like:** Honest reporting of test runs with all relevant checks passing and no hidden suppressions.

## 4. PR Description Evidence
- **Practice Submission:** PR title and body in the package bundle.
- **Your PR:** `pr_draft.md` using Path Review's PR template and AI-use disclosures.
- **Good Looks Like:** Fully completed template sections, clear issue reference, and explicit AI disclosure under Notes for Reviewers.
