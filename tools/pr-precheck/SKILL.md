---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

<!-- State, in your words, the one question this tool answers and what
a PR package is: what artifacts it contains and what they are read
against. CONTRACT.md fixes the question; your frame has to say it so
the tool cannot wander into grading something else. -->

Answer exactly one question about exactly one PR package: is this ready to submit? Treat the package as a candidate pull request containing a title, description, commits, diff, and test evidence, read against the plan it claims to implement and the issue that plan belongs to. Do not grade a different artifact, combine multiple packages, or decide from gut feel. Execute the rubric and procedure supplied in this tool directory.

## Inputs and modes

<!-- Define both modes. Live mode: name every input (your plan.md with
its deviation notes, your branch's diff, your draft PR title and
description, your test evidence, your issue), where each comes from,
and what a house-chain student reads instead. The branch's diff is
everything the branch changes relative to the repo's default branch:
`git diff main...HEAD` (three dots), run from the working copy, is
the command that produces it; name the source that concretely. Eval
mode: state that the bundle is the whole world, nothing is fetched,
and every check runs with the full verdict rule. -->

Operate in exactly one of two modes.

Live mode: Review the student's own proposed PR using all of the following:

plan.md, including its ## Deviations notes, from the working copy.

The branch's committed diff relative to main, obtained from the working copy with git diff main...HEAD.

The draft PR title and description in pr_draft.md.

The test results and before/after reproduction output in test_evidence.md.

The issue's actual discussion thread in the scoped repository.

The repository's .github/PULL_REQUEST_TEMPLATE.md.

The repository's docs/CONTRIBUTING.md, including applicable contribution and AI-use policies.

For a house-chain student, read the supplied house plan and house repro pack instead of the student's own plan and repro materials, while reviewing the corresponding working branch and PR artifacts. Compare the diff with the plan and its deviations, test results with the plan's test plan, and the PR description with the actual diff and repository requirements. Do not claim to have inspected evidence you could not access.

Eval mode: Treat the supplied package bundle as the entire world. Use only facts contained in that bundle. Do not fetch external information, inspect the working repository, or read unrelated local files. Grade every rubric check and apply the complete verdict rule to the package.

## The scope seam (live mode only)

<!-- Tell the tool when to read scope.md, what to do with the rules it
finds there, what to refuse, and what to do when the scope's repo line
is an unfilled placeholder. State that eval mode ignores scope.md
entirely. CONTRACT.md names the required behavior; your frame has to
instruct it. -->

In live mode, read scope.md before inspecting any other input. Confirm that the target repository matches the repository named by its Repo: line and obey all scope restrictions. If the Repo: line contains an unfilled placeholder, stop without grading and tell the student to replace it with their section's Path Review repository. If the PR is outside the permitted repository, refuse to grade it. Never guess or silently expand scope. In eval mode, ignore scope.md entirely.

## The voice seam (live mode only)

<!-- Tell the tool when to read voice-guide.md, which outgoing text it
gates (the PR title and description), how to report a broken rule, and
why it never changes the verdict on its own. State that eval mode
ignores it entirely. -->

In live mode, read voice-guide.md and check the outgoing PR title and description against its writing rules. Report each identifiable violation in the readable summary, with evidence from the draft and the relevant rule. The voice guide does not independently change the verdict; only rubric checks and the rubric's verdict rule determine acceptance or rejection. In eval mode, ignore voice-guide.md entirely.

## Component reads

<!-- Tell the tool how the pieces connect: rubric.md defines the
checks and the verdict rule, references/evidence-guide.md maps where
each evidence family lives, procedure.md is executed as written. Say
what the tool does when the procedure is silent on a step (report the
gap, never improvise around it) and what it does when rubric.md or
procedure.md has no content (the refusal rule, stated as an
instruction). -->

Read and execute procedure.md as written. Use rubric.md as the sole authority for the named checks, their evidence requirements, pass conditions, weights, and verdict rule. Use references/evidence-guide.md to locate and interpret each evidence family in the package. Complete every check required by the rubric and provide one evidence line for each check.

If rubric.md has no substantive content or procedure.md has no substantive content, refuse to grade and explain which component must be completed. Do not invent checks or procedures to compensate for empty files. If a procedure step is silent or underspecified, report the gap rather than improvising an alternative process. Do not silently substitute your own judgment for the rubric's criteria.

## Verdict and output

<!-- State the binary verdict space (accept means submit, reject means
hold) and instruct the tool to end its reply with the fenced JSON
block below, valid and last, with nothing after it. The schema is
CONTRACT.md's, verbatim; do not edit it. -->

Return only one of two verdicts: accept means the package is ready to submit; reject means hold it and address the problems. Assemble the verdict strictly according to the rule in rubric.md, including its treatment of unclear grades. Do not introduce a third verdict, reservations verdict, or independent scoring system.

Provide a readable per-check summary before the final output. End the reply with the following fenced JSON block, valid and last, with nothing after it. Preserve the schema, key names, field order, and allowed values exactly:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```
Use the actual PR URL or practice bundle ID for item. Include every rubric check in checks, using pass, fail, or unclear as the grade and one concise, evidence-based line for each. Ensure the JSON parses correctly. Never append text after the closing JSON code fence.

## Grading discipline

<!-- Write the standing rules the tool grades under: evidence first,
grade the thing not the polish, the rubric decides, the procedure
decides how, and how unclear grades are treated when the rubric's
verdict rule is silent. CONTRACT.md states each as a guarantee; your
frame has to make them instructions. -->

Evidence first: Grade no check without citing the fact, artifact, or quote that determined its result. Never use unsupported statements such as "looks fine."

Grade the artifact, not the polish: Judge completeness, correctness, scope, testing, reviewability, and compliance against the plan, issue, diff, and applicable repository standards. Do not reward attractive formatting or confident wording in place of evidence.

The rubric decides: Apply each check's written pass condition consistently, even when its outcome feels counterintuitive. Revise the rubric, not an individual grade, when a criterion is wrong.

The procedure decides how: Follow the written procedure. Report missing or ambiguous steps instead of silently inventing a process.

Unclear defaults to fail: Apply the rubric's explicit rule for unclear. If the rubric does not specify how an unclear grade affects the verdict, treat it as failing. Do not treat an unverifiable claim as proof that the PR is ready.
