# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
|maintainer-commits|"last 5 default-branch commits" under Repo facts|Newest commit is dated within the past 30 days|Required|
|AI policy|"contribution policy" line under Repo facts|AI-assisted contribution is not banned|Required|
|unclaimed-issue| The "this issue:" line under Repo facts plus every comment in the Comments section| ALL of these hold: (1) assignees is `none`; (2) no linked PR is open, and no comment mentions an open PR for this issue; (3) no comment dated within 30 days before the capture date says the writer is taking or working on the issue (examples: "I'll take this", "can I work on this", "working on this"), unless a later comment withdraws it. A claim older than 30 days with no PR mentioned after it does not count. A closed, unmerged PR is not a claim.|Required|
|latest-release-within-a-year|"latest release" under Repo facts|Newest release/ship is dated within the past 365 days|Preferred|
|preferred-language|"language" line under Repo facts|The repo's primary language is Python|Preferred|
|scope|"Issue body" under Issue|Pass only if the issue describes a single, bounded contribution that can be implemented without first selecting or implementing another issue. Fail if the issue is an index that primarily lists or links to other issues, or if the requested change explicitly requires implementing a new multi-part feature across multiple application components (for example, toolbar + element behavior + export + app wiring).|Required|

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

1. Grade every check in the table as `pass`, `fail`, or `unclear`, using only the evidence source named in its row.
2. Accept the issue if every `required` check passes.
3. Reject the issue if any `required` check fails.
4. `unclear` on a required check counts as `fail`.
5. `preferred` checks never change the verdict, whatever their grade, including `unclear`. For accepted issues, report each preferred grade in the summary. An accepted issue with more preferred passes ranks higher.
6. The verdict is always exactly `accept` or `reject`, never a third value.