# PR Precheck Skill

## Purpose
This skill evaluates a pull request (PR) package to determine whether it is ready for submission (`accept` or `reject`), enforcing correctness against the approved `plan.md`, the issue requirements, and repository standards.

## Modes
1. **Live Mode:** Used when checking your own local PR before opening it. Reads `plan.md` (including deviation notes), the branch diff (`git diff main...HEAD`), your draft PR title and description (`pr_draft.md`), your test evidence (`test_evidence.md`), the issue thread, the repository PR template, and `docs/CONTRIBUTING.md`.
2. **Eval Mode:** Used by the evaluation harness to grade a frozen practice submission bundle (`pkg-XX` or `calib-XX`). Relies solely on the package bundle text with no external fetching.

## Refusal Rules
- Refuses to grade if `scope.md` still carries the placeholder repository or if required rubric/procedure files are empty.

## Output Format
Ends with a fixed JSON block:
{ "item": "<PR URL or bundle id>", "checks": [
    { "name": "<check name>", "grade": "pass|fail|unclear", "evidence": "<one line: the fact or quote that decided it>" }
  ], "verdict": "accept|reject" }
