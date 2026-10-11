# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

<!-- Where the plan states its scope, boundary, and deviation notes,
and where the diff shows what actually changed. What it means for a
diff to match the plan, for an honest deviation to re-tie a mismatch,
and what silent drift looks like in each direction (more than the
plan, or less with no note). The description's fidelity claims read
against the diff live here too: a description claiming more or less
than the diff delivers is silent drift, not a comms problem. -->

Where it lives: In eval mode, inspect the plan-context block's scope pair, planned files, requirements, and deviation notes; then compare them with the candidate PR's unified diff, commit list, and description. In live mode, read plan.md and its deviation notes, compare them with the branch diff against the appropriate base branch, and check the draft PR title and description against the implementation.

What good looks like: Every changed file and material behavior falls within the plan's stated boundary or is covered by a documented, justified deviation. Required planned behavior is implemented, and the description does not claim functionality that the diff fails to deliver or omit a material limitation. Silent drift includes unrelated additions, missing planned work without explanation, and description claims that exceed or understate the actual change.

## Test evidence (harness category: not-tested)

<!-- Where the PR shows its proof: the test-evidence section's
before/after against the plan's test plan and the reproduction's own
steps, and the outcome of the repo's own checks or suite. What
decisive looks like (an observable behavior named, the expected-after
stated, the checks' outcome visible) next to "tests pass". -->

Where it lives: In eval mode, inspect the plan-context block's test plan and reproduction steps, the candidate PR's test-evidence section, and the outcomes of the repository's checks or test suite when supplied. In live mode, compare the test plan in plan.md with the captured test output, relevant test changes in the branch diff, reproduction steps, and available repository check results.

What good looks like: Evidence identifies the behavior tested, the command or reproduction steps used, the expected result, and the observed outcome. A statement such as "tests pass" without supporting results does not establish that the required behavior was tested. Missing test results or untested required behavior must be reported rather than assumed successful.

## Diff quality (harness category: unreviewable)

<!-- Where the change itself lives: the unified diff and the commit
list. What a reviewable change looks like (the fix visible, nothing
unrelated riding along) and the debris tells: debug leftovers, dead
code, commented-out blocks, formatting churn, drive-by edits. -->

Where it lives: In eval mode, inspect the candidate PR's unified diff and commit list. In live mode, inspect the branch diff against the appropriate base branch and the relevant commit history.

What good looks like: The diff makes the intended fix or feature identifiable, keeps changes relevant to the planned work, and provides enough context to review the implementation. Look for debug leftovers, dead code, commented-out blocks, accidental formatting churn, unrelated edits, and changes that obscure the intended behavior. Record concrete examples rather than labeling a diff "messy" without evidence.

## Standards and comms (harness category: standards-wall)

<!-- Where the repo states its asks (the repo-facts block's PR
template sections, contributing instructions, and stated policy,
including AI-use disclosure) and where the PR honors them: the
stated sections filled with real content, the disclosure present,
explicit maintainer direction in the thread engaged. What compliant
looks like next to boilerplate or a visibly ignored ask. (Whether
the description's claims match the diff is plan fidelity, above.) -->

Where it lives: In eval mode, inspect the repo-facts block's PR template asks, stated repository policy, contribution requirements, AI-use disclosure requirements, and maintainer direction in the issue or PR thread. In live mode, inspect the repository's PR template, docs/CONTRIBUTING.md, applicable policy, the issue thread, and the draft PR title and description.

What good looks like: Required PR template sections contain substantive, accurate information; applicable contribution and policy requirements are followed; required AI-use disclosures are present; and explicit maintainer requests are addressed. Boilerplate that does not answer the template's questions, missing required disclosures, or visibly ignored instructions are concrete violations. Assess whether description claims match the diff under plan fidelity, not as a separate communications failure. In eval mode, use only the supplied bundle and do not fetch external information or inspect unrelated local files.
