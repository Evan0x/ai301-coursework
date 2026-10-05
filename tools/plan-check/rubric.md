# Rubric

| Check | Evidence | Pass condition | Weight |
| --- | --- | --- | --- |
| Diagnosis | Root cause explanation | Explains the root cause of the bug and identifies the buggy file or location | Required |
| Scope | Boundaries of proposed changes | Explicitly lists the specific files to be modified | Required | 
| Test Plan | Re-runnable reproduction steps | Defines exact steps to run and the expected output after the fix | Required |
| Conventions | Repository and comment formatting | Adheres to repository code structure and issue thread guidelines | Required |

### Verdict Rule
A plan is **ready** (`accept`) if all Required checks pass. Any missing, failed, or unclear (`?`) check defaults to a fail and results in **hold** (`reject`).
