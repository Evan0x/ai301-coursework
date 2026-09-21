# Issue Evaluation Rubric

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer_active | Repo-facts block (commit dates, maintainer comments). | At least one maintainer commit, PR merge, or comment within the last 90 days. | required |
| repo_in_use | Repo-facts block (commit/PR history). | At least 3 merged PRs or active commits in the last 6 months, and the repo is not archived. | required |
| clear_scope | Issue title, body, and comment thread. | Pass only if the issue names ONE specific, implementable change with a settled approach. Reject if any of the following apply: (a) it is a tracking/umbrella issue that lists or links out to multiple sub-tasks rather than describing a single change (a "megaissue"); (b) it reflects unresolved, long-running design debate or repeated abandoned attempts with no spec the maintainers have actually agreed on; (c) the request leaves a core product or design decision undecided — what exactly should be built, for whom, using what asset/approach — rather than describing a bounded task ready to implement. Do NOT reject merely for informal wording, missing minor details, brevity, or ordinary small/medium size — only the three structural reasons above justify a fail. | required |
| no_duplicate_work | Linked PRs, open PR list, issue comments. | No currently open or merged PR already addresses or resolves this exact issue. | required |
| policy_compliant | Issue body/labels, repo-facts, and any CONTRIBUTING/policy text in repo-facts. | Reject if any of the following apply: the repo is explicitly frozen, archived, or stated as not accepting external contributions; the issue is a security vulnerability report; the repo restricts contributions to internal/core maintainers only (no external PRs); or the repo's contribution policy explicitly bans AI-generated code, documentation, or contributions. Otherwise pass. | required |
| good_first_issue_fit | Issue labels. | Tagged `good first issue` or `help wanted`. | preferred |

## Verdict rule

- **ACCEPT**: Accept if and only if EVERY `required` check passes.
- **REJECT**: Reject if ANY `required` check fails.
- **UNCLEAR**: If evidence for any `required` check is missing or ambiguous, treat `unclear` as a **fail** (result is **REJECT**).
- **PREFERRED**: `preferred` checks never change the binary verdict (`ACCEPT`/`REJECT`); they are used solely to rank accepted issues.
