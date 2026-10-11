# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|scope-alignment|Plan, issue acceptance criteria, and branch diff|Changes match the approved plan and issue scope; no unjustified unrelated work|Required|
|plan-deviations|Plan deviation notes and branch diff|Material deviations are documented and justified|Required|
|implementation-completeness|Plan requirements, acceptance criteria, and branch diff|All required functionality is implemented|Required|
|test-evidence|Test results, commands, and relevant test changes|Relevant tests support the changed behavior; no unresolved relevant failures|Required|
|repository-requirements|Issue thread, PR template, and `docs/CONTRIBUTING.md`|Applicable repository and issue requirements are satisfied|Required|
|pr-title-description|Draft PR title and description, compared with the diff|Accurately describes the change and follows applicable conventions|Required|
|evidence-quality|Evidence supplied for implementation and test claims|Material claims are supported by specific, consistent evidence|Required|

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

The final verdict must be exactly accept or reject.

Return accept only when every required check passes.

Return reject if any required check fails or is unclear.

Do not invent evidence, assume tests passed, or treat a claim as proof.

For every check, include a one-line evidence statement identifying the decisive fact or quote.

Apply the grading procedure and the repository's explicit requirements when resolving overlapping criteria.

If the rubric or procedure is missing or has no usable content, refuse to grade rather than inventing grading rules.

Mode-specific rules:

In live mode, follow the scope and voice rules in SKILL.md and consult the required repository sources.

In eval mode, use only the supplied package bundle. Do not fetch external information or inspect unrelated local files.

In eval mode, do not apply live-mode scope or voice checks unless the supplied evaluation rubric explicitly requires them.
