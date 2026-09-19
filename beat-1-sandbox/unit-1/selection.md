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
https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72


**Verdict output**

```
All required evidence gathered. Grading:

Check: maintainer-commits
Grade: pass
Evidence: Newest default-branch commit 2026-09-16T21:42:18Z (Andrew Burke) — 3 days
before today (2026-09-19)
────────────────────────────────────────
Check: AI policy
Grade: pass
Evidence: No AI ban anywhere: no root/.github CONTRIBUTING, and docs/CONTRIBUTING.md,
PULL_REQUEST_TEMPLATE.md, README contain no AI-use restriction. Silence passes.
────────────────────────────────────────
Check: unclaimed-issue
Grade: pass
Evidence: "assignees":[], "comments":[], issue timeline has only 4 LabeledEvents (no
connected/cross-referenced PR), and gh search prs "72" returned []
────────────────────────────────────────
Check: latest-release-within-a-year (preferred)
Grade: fail
Evidence: "latestRelease":null; /releases returns 0
────────────────────────────────────────
Check: preferred-language (preferred)
Grade: pass
Evidence: "primaryLanguage":{"name":"Python"}
────────────────────────────────────────
Check: scope
Grade: pass
Evidence: One bounded fix — catch passlib's UnknownHashError in core/security.py so
verification returns False, plus remove the @pytest.mark.xfail in
tests/unit/test_security.py; "Estimated effort: 1–2 hours"

All three required checks pass → accept. It also carries good first issue and tier-1 labels, is written by the repo maintainer, and names its two relevant files. Of the two preferred checks, it wins on language (Python) and loses on releases — but this repo has no releases at all, so that will be true of every candidate here and won't separate it from other accepted issues.

{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72",
  "checks": [
    {"name": "maintainer-commits", "grade": "pass",
     "evidence": "Newest default-branch commit is 2026-09-16T21:42:18Z (Andrew Burke), 3 days before today 2026-09-19"},
    {"name": "AI policy", "grade": "pass",
     "evidence": "No AI-contribution ban in docs/CONTRIBUTING.md, .github/PULL_REQUEST_TEMPLATE.md, or README; no AI_POLICY.md present"},
    {"name": "unclaimed-issue", "grade": "pass",
     "evidence": "assignees [], comments [], timeline has only LabeledEvents (no connected/cross-referenced PR), PR search for '72' returned none"},
    {"name": "latest-release-within-a-year", "grade": "fail",
     "evidence": "latestRelease is null and the releases endpoint returns 0 entries"},
    {"name": "preferred-language", "grade": "pass",
     "evidence": "Repo primaryLanguage is Python"},
    {"name": "scope", "grade": "pass",
     "evidence": "Single bounded fix: return False on passlib UnknownHashError in core/security.py and drop the xfail in tests/unit/test_security.py; 'Estimated effort: 1-2 hours'"}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

**Run history**

agreement: 1/1 scored items
agreement: 18/20 scored items (bar: 18/20: PASS)
agreement: 18/20 scored items (bar: 18/20: PASS)

**Issue analysis**

issue-20 — rubric decision: accept; gold label: reject.

The required maintainer-commits, AI policy, unclaimed-issue, and scope checks passed. The latest-release-within-a-year check failed, but it is a preferred check and therefore does not change the verdict. The preferred-language check passed. Because all required checks passed, the rubric returned accept. The gold label was reject, so this was one of the cases where my rubric did not match the expected decision.

**Check rationale**

|scope|"Issue body" under Issue|Pass only if the issue describes a single, bounded contribution that can be implemented without first selecting or implementing another issue. Fail if the issue is an index that primarily lists or links to other issues, or if the requested change explicitly requires implementing a new multi-part feature across multiple application components (for example, toolbar + element behavior + export + app wiring).|Required|

I added this check to make the rubric account for whether an issue is appropriate for a newcomer, rather than relying only on repository activity, contribution policy, and whether the issue is unclaimed. The check specifically targets issues that span over multiple areas or are actually a bundle of multiple issues, which is to avoid.

**Trade-offs**

The scope check changed issue-10 from an incorrect accept to the correct reject. I re-ran issue-10 and issue-20 with --only after adding the check. Issue-10 then matched the gold reject, while issue-20 remained an accept. This shows that the check catches the megaissue case but still misses at least one scope case that the gold labels reject.

---

## Selection rationale

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

---
1. Issue #72 fits my interests because it is a Python issue involving error handling and existing application behavior, which is relevant to the Software and AI Engineering skills I am developing. The estimated effort is 1–2 hours, so it also fits the time available for Unit 2.

2. The verdict correctly identified that the repository is active, the issue is unclaimed, the project uses Python, and there is no contribution-policy restriction on AI assistance. I also considered the issue's estimated effort and whether the specific bug sounded manageable for my personal skill set, which my rubric did not directly measure.

3. The main difficulty I anticipate is getting familiar with the existing password/hash verification code and understanding how malformed stored hashes are currently handled. I expect the coding change itself to be relatively contained, but reproducing the problem and understanding the project's tests may take some time.

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
