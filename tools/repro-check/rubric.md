| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| names-the-issue | Claim comment and Repro report | References the target issue by its number, URL, or by accurately describing the bug. Fails if the comment claims or reproduces a completely different bug than the one provided in the issue context. | required |
| steps-rerunnable | Repro report steps | Provides clear, actionable commands or steps allowing a reader to reproduce or attempt reproduction. | required |
| environment-recorded | Repro report environment block | Mentions relevant environment details (OS, runtime, versions, or setup context) for the reproduction attempt. | required |
| claim-voice | Claim comment text | Promises an investigation or reproduction attempt without asserting a confirmed fix or specific delivery date. | required |
| ai-disclosure | Repo policy and comment text | If the repository policy explicitly requires AI disclosure, the comment must contain an AI disclosure. If the policy does not mandate it, this check automatically passes. | required |

### Verdict Rule
* **Accept:** If all `required` checks pass.
* **Reject:** If any `required` check fails.
