# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
|Diagnosis|The plan's stated cause read against the reproduction evidence's observed behavior, inputs, and failure point|Pass if the diagnosis explains the reproduced failure without contradicting the evidence and identifies a cause that the proposed change can address; fail if it ignores, contradicts, or merely restates the symptom as the cause|required|
|Scope|The plan's scope statement read against the issue, diagnosis, and repo facts|Pass if the proposed change is bounded to the diagnosed problem and the plan clearly excludes unrelated changes; fail if the change expands beyond what the evidence and issue justify|required|
|Approach|The plan's proposed implementation read against its diagnosis, scope, and relevant repo facts|Pass if a stranger could use the described approach to make the intended change in the identified files without having to guess the core implementation decisions; fail if the approach is missing, targets only the symptom, or leaves essential implementation decisions unresolved|required|
|Test plan|The plan's test plan read against the reproduction evidence's steps and expected failure, plus the repo facts|Pass if the tests exercise the real affected behavior, include the reproduced failure case, and define an observable result that would demonstrate the fix; fail if the tests cannot distinguish the broken behavior from the fixed behavior or do not exercise the affected path|required|
|Unknowns|The plan's risks and unknowns read against the reproduction evidence, issue context, and repo facts|Pass if uncertainties that could affect the implementation or outcome are identified as uncertainties and are not presented as established facts; fail if important unknowns are ignored or unsupported assumptions are treated as certain|required|
|Conventions| The plan comment read against the issue thread highlights and repo-facts block|Pass if the proposed plan responds to relevant issue-thread context and follows stated repository conventions that affect the change; fail if it contradicts relevant thread requirements or repo conventions, or ignores them when they materially constrain the work|required|
|Execution-readiness| The plan's diagnosis, scope, files, approach, and test plan read together|Pass if a maintainer or developer who did not write the plan could start implementing the bounded change and know what behavior to verify without needing to infer a missing core decision; fail if essential execution information is absent or contradictory|required|

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept if every required check passes. Preferred checks, if any are added later, never change the verdict. Treat `unclear` as a fail. Reject if any required check fails or is unclear.