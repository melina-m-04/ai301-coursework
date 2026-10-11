# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->


## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides where the plan sits in the order (before the diff? before the
description?) and says why the order matters for the side-by-side
checks that come later. -->

1. In live mode, read scope.md first. Stop if the repository is outside the declared scope or the repository field is still a placeholder. Skip this step in eval mode.

2. Read rubric.md and identify each required check, its evidence sources, pass condition, and weight. If the rubric or procedure has no usable content, refuse to grade.

3. Read plan.md, including its scope, test plan, acceptance criteria, and deviation notes. Record the files and behaviors the plan expects, the tests it calls for, and any documented deviations.

4. Read the issue thread and extract the requirements and acceptance criteria that define the intended change.

5. Read the branch diff against the appropriate base branch. List changed files, implemented behaviors, added or modified tests, and changes not accounted for by the plan.

6. Read the test evidence and compare reported commands and results against the plan's test plan and relevant repository checks.

7. Read the draft PR title and description after reviewing the plan and diff. This order makes it possible to verify that the description accurately represents the implementation rather than accepting its claims at face value.

8. Read the repository PR template and docs/CONTRIBUTING.md for applicable submission requirements. In eval mode, use only equivalent artifacts included in the package bundle.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which file, diff,
or page per your evidence guide) to pull the fact from, and what to
record. The load-bearing gathers this week are pairings: diff files
against plan scope, claimed evidence against the plan's test plan and
the repo's checks, description claims against diff contents. A
complete procedure leaves no check whose evidence an executor would
have to hunt for. -->

1. Scope alignment: Compare the changed files and behaviors in the diff against the files, scope, and behaviors named in the plan and issue. Record each material addition, omission, or unrelated change.

2. Plan deviations: Compare the diff with the plan and read its deviation notes. Record each material deviation and the stated justification. If no deviation is apparent, record that the reviewed diff contains no identified material deviation.

3. Implementation completeness: Map each planned requirement and issue acceptance criterion to the relevant diff hunk or test. Record requirements with no supporting implementation and any implementation that contradicts a requirement.

4. Test evidence: Compare the plan's test plan with the supplied test commands, results, and relevant test changes. Record which planned tests have evidence, their outcomes, and any relevant failures or missing results. Do not treat a claim that tests passed as proof without supporting evidence.

5. Repository requirements: Extract applicable requirements from the issue, PR template, and docs/CONTRIBUTING.md. Compare each requirement with the package and record the supporting evidence or the specific violation.

6. PR title and description: Compare the draft title and description against the plan, issue, and diff. Record inaccurate claims, omitted material information, and violations of explicit repository conventions.

7. Evidence quality: Check material claims against their cited or supplied evidence. Record claims contradicted by the package and claims that cannot be independently verified from the available evidence.

8. In live mode, read voice-guide.md and check the draft title and description against it. Record any violations, but do not let a voice-only violation determine the verdict unless the rubric explicitly makes it a grading criterion.

9. Use references/evidence-guide.md when deciding how to locate and report evidence. In eval mode, do not fetch external resources or inspect files outside the supplied bundle.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Execute the checks in the exact order in rubric.md. Use the evidence gathered for each check rather than restarting the review.

2. For each check, compare the gathered facts with its pass condition and assign exactly one grade: pass, fail, or unclear.

3. Assign pass only when the evidence supports the pass condition. Assign fail when evidence establishes a violation, omission, contradiction, or unmet requirement. Assign unclear when the available evidence cannot establish whether the pass condition is met.

4. If a required artifact or fact is absent, identify which check depends on it and grade that check unclear unless the available evidence independently establishes a failure. Do not invent missing facts or assume that an unreported test passed.

5. Reuse gathered evidence when it supports multiple checks, but evaluate each check against its own pass condition. Do not let a passing result for one check substitute for evidence required by another.

6. Record one concise evidence statement per check. Include the specific file, diff detail, test result, or requirement that determined the grade. Keep the statement to one line and avoid unsupported conclusions.

7. Do not introduce new grading criteria during execution. If a genuine grading question cannot be resolved by the rubric or procedure, do not improvise; report the limitation according to the skill's required output rules.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check: the
check whose failure the verdict turned on. When more than one check
failed, your procedure picks which one gets quoted (first failing
required check in rubric order is a fine rule); nothing picks it for
you, so write the rule down. A complete procedure produces the same
verdict from the same grades, every time. -->

1. Review the final grades in rubric order. Return accept only if every required check is pass.

2. Return reject if any required check is fail or unclear. Do not average grades, assign numerical scores, or allow passing checks to offset a failed or unclear required check.

3. Select the deciding check as the first required check in rubric order whose grade is fail or unclear. If several checks fail, use this same rule consistently.

4. In the output, preserve every required check, its exact grade, and its one-line evidence statement. The selected deciding check's evidence must make clear why the verdict is reject.

5. Identify the item using the actual PR URL in live mode or the supplied bundle identifier in eval mode. Never invent an identifier.

6. End the response with the exact fenced JSON schema specified in SKILL.md. Use only accept or reject for the verdict, and include no text after the JSON block.
