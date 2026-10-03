# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

1. Read the reproduction evidence before reading the candidate plan. Record the reproduced behavior, the inputs or steps that trigger it, the observed failure, and any evidence that points toward its cause.
2. Read the issue context and repo-facts block. Record the issue's requested problem, relevant constraints, affected area, and repository conventions or facts that could constrain the change.
3. Read the candidate plan. Record its diagnosis, proposed scope, files to touch, implementation approach, test plan, risks, unknowns, and any deviations.
4. Read the candidate plan comment. Record what it communicates about the proposed change and compare it with the issue context and relevant thread requirements.
5. Keep the reproduction evidence and issue/repo context as the reference point while grading the plan. Do not treat statements in the candidate plan as established facts when the package evidence does not support them.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

1. For the Diagnosis check, compare the plan's stated cause with the reproduction evidence. Record the specific reproduced behavior, failure point, and any evidence supporting or contradicting the proposed cause.
2. For the Scope check, compare the plan's stated changes and exclusions with the issue, diagnosis, and repo facts. Record which files or behaviors the plan proposes to change and whether those changes are bounded to the diagnosed problem.
3. For the Approach check, read the proposed implementation against the diagnosis, scope, affected files, and repo facts. Record the core implementation steps and identify any essential decision that a stranger would still have to guess.
4. For the Test plan check, compare the proposed tests with the reproduction evidence's steps and failure case. Record the affected behavior being exercised, the expected result after the fix, and whether the test can distinguish the broken behavior from the fixed behavior.
5. For the Unknowns check, read the plan's risks and unknowns against the reproduction evidence, issue context, and repo facts. Record material uncertainties and whether the plan labels them as uncertainties rather than unsupported facts.
6. For the Thread and conventions check, compare the plan comment with relevant issue-thread context and the repo-facts block. Record any thread requirements, stated conventions, or constraints that the comment follows or contradicts.
7. For the Execution-readiness check, use the evidence already gathered for the diagnosis, scope, approach, and test plan. Record whether a developer who did not write the plan could begin the intended change and know what behavior to verify without making a missing core decision.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Grade each check using only the evidence gathered for that check and the pass condition in `rubric.md`.
2. Grade the checks in this order: Diagnosis, Scope, Approach, Test plan, Unknowns, Thread and conventions, Execution readiness.
3. Mark a check `pass` only when the evidence satisfies its pass condition.
4. Mark a check `fail` when the evidence contradicts the pass condition or shows that the required outcome is not met.
5. Mark a check `unclear` when the package does not provide enough evidence to determine whether the pass condition is satisfied. Do not fill an evidence gap with assumptions.
6. When evidence is absent, identify the missing evidence in the check's evidence line and grade the check `unclear` unless the pass condition can still be established from the available evidence.
7. Do not grade a check based on formatting, section count, writing length, or other properties of the plan's presentation unless those properties directly affect the outcome described by the pass condition.
8. Do not re-grade an earlier check based on a later preference or impression. Apply each check exactly as written in `rubric.md`.
9. For every check, record one concise fact, quote, or comparison that explains the grade. The evidence must be specific enough for another executor to understand why the grade was assigned.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

1. Collect the final grade for all seven checks.
2. Apply the verdict rule from `rubric.md`: every required check must pass for the package to be accepted.
3. Treat every `unclear` grade as a fail for verdict purposes.
4. Return `accept` only when all required checks are `pass`.
5. Return `reject` when any required check is `fail` or `unclear`.
6. In the output for each check, quote or identify the specific fact that decided the grade rather than giving a general impression.
7. Emit the required final JSON object with the issue URL or bundle ID, every check and its grade/evidence, and the final binary verdict.