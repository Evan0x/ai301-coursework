## Read order
1. Read issue thread context and reproduction details.
2. Read proposed plan in `plan.md` and comment draft in `comment.md`.
3. Read repository guidelines and code conventions.

## Evidence gathering
1. Extract file paths and bug diagnosis from `plan.md`.
2. Extract proposed code modifications and untouched files.
3. Extract verification steps and test script outputs.

## Check execution
1. Verify root cause diagnosis maps to reported issue.
2. Verify scope explicitly defines touched vs. untouched files.
3. Verify test plan re-runs original reproduction with expected fix state.
4. Verify code and comment formatting follow repository conventions.

## Verdict assembly
1. Evaluate each check in `rubric.md` against gathered evidence.
2. If all High weight checks pass, output `accept`.
3. If any check fails or is unclear (`?`), output `reject`.
