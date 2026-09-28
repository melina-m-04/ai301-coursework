# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
|env-recorded|The environment record in the repro report, including the versions/configuration needed to reproduce the issue; look specifically at the report's environment section/record|The recorded environment contains enough concrete information to determine what environment produced the observed result and to reproduce it without guessing essential details|required|
|steps|The reproduction steps in the repro report, together with any referenced setup commands or fixtures in the package; look at the report's steps/instructions section and the referenced setup files, scripts, or fixtures|A person with access to the package can follow the steps in order and reach the reported test point without needing undocumented essential actions or information|required|
|honest-outcome|The claim comment and stated outcome in the repro report, read against the actual reproduction evidence/output excerpt in the package|The stated outcome accurately reflects the evidence, and the package does not claim reproduction or confirmation that the evidence does not support|required|
|claim-intent|The candidate claim comment, read against the issue it is posted on|The comment states what the author actually did and what they intend to do next in terms specific to this issue, and makes no commitment the author cannot honestly back: no fixed delivery deadline, no guaranteed fix, no request to reserve or hold the issue. A comment whose stated intent would read identically on any other issue fails|required|
|disclosure|The AI/contribution policy in the repo-facts block, read against both candidate comments; treat every package as AI-assisted work|If the stated policy requires disclosing AI assistance in comments of this kind, the comments disclose it in the terms the policy asks (the tool used, and the extent of the assistance). If the stated policy imposes no such requirement on issue comments, including when the repo-facts block states no AI policy, this check passes; that is a pass, not an unclear|required|

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->
Accept if every required check passes. Reject if any required check fails. An unclear result is the same as a fail for that check.