# Unit 1 — Issue Selection
Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12

**Verdict output**

Grading issue: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12

maintainer_active: pass

clear_scope: pass

reproducible: pass
Verdict: accept
{
"issue": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12",
"verdict": "accept",
"reason": "Clear bug report with exact reproduction steps and scope well within individual capability."
}

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

15/20, 17/20

**Issue analysis**

issue-05: My rubric decided `reject`, matching the gold label. The reasoning that produced this result was that the issue involved an undecided core design debate, triggering the rejection rule under `clear_scope`.

**Check rationale**

"Issues must have a well-defined boundary and a single primary bug or feature request without sprawling dependencies." This wording was chosen to filter out vague megaissues and ensure isolated changes.

**Trade-offs**

issue-03: The `clear_scope` check gives up minor multi-file refactoring enhancements that touch several independent modules, preferring strict containment over broad architectural updates.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the reasoning is, and not on length — a short honest answer to each earns the full marks. This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. The issue fits my interest in backend code cleanup and can be easily completed within my available time window.
2. The verdict correctly identified the clear reproduction steps and isolated bug scope, weighing the practical feasibility that a static rubric template might miss.
3. The anticipated difficulty in claiming it is low due to well-defined code boundaries and straightforward error messages.
