# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

[Link to the pull request you opened. It must be the pull request's own page on the Path
Review repo, not your fork's branch page.]

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/133

**Branch**

[The name of the branch the pull request comes from, exactly as it appears in your fork.
The naming shape is a type prefix, then the issue number, then a short description. **The
issue number in the branch name must be the number of the issue the pull request fixes** —
a name carrying any other number does not satisfy this field.]

fix/72-handle-malformed-hash

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

The recorded full evaluation achieved 20/20 agreement:

clear-accept: 7/7

not-tested: 4/4

silent-drift: 4/4

standards-wall: 2/2

unreviewable: 3/3

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

pkg-12 — My rubric decided reject, and the gold label was reject. This package belongs to the unreviewable category. The matching verdict supports the rubric's use of required checks: a PR should be held when reviewability problems prevent a reliable assessment of the change. The package result agrees with the gold label (agree: yes).

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/pr-precheck/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

Exact rubric check: Material deviations are documented and justified

This is the pass condition for plan-deviations. I kept this outcome-based check so a justified deviation can still pass when it is documented, rather than automatically rejecting every change that differs from the original plan. This is consistent with the rubric's requirement to judge the diff against the plan and its deviation notes.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

The rubric requires every required check to pass and treats unclear evidence as a failure. This favors avoiding premature submission when evidence is insufficient, but it can reject a PR when a claim is difficult to verify from the supplied package. I made the rule explicit in the verdict section: “Return reject if any required check fails or is unclear.” The evaluation achieved 20/20 agreement across all five categories, providing evidence that this trade-off did not cause disagreements on the scored packages in the recorded run.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
