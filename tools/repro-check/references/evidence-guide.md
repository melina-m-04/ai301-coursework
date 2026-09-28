# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

Where it lives: In an eval bundle, look at the repro report's environment record and the issue context for the environment the issue targets. Also check the repo-facts block for repository-specific version or configuration facts. In live mode, look at the issue thread, relevant repo documentation, and the student's draft reproduction report.

What good looks like: The environment record identifies the relevant OS, software/dependency versions, configuration, and other conditions needed to reproduce the issue. The versions and conditions match what the issue targets, or any relevant difference is explicitly called out.

## Steps

Where it lives: In an eval bundle, look at the repro report's reproduction steps and any setup commands, scripts, fixtures, or other artifacts referenced by those steps. In live mode, look at the student's draft reproduction steps and the referenced repository files or commands.

What good looks like: Starting from the stated starting state, a person unfamiliar with the original reproduction can follow the steps in order and reach the point where the reported behavior can be observed. Essential setup actions, inputs, and commands are present or directly available in the package.

## Behavior shown

Where it lives: In an eval bundle, look at the output excerpts, logs, screenshots, test results, or other artifacts produced by the reproduction, and read them against the issue description and expected behavior. In live mode, inspect the evidence attached to or referenced by the student's draft and compare it with the issue's reported behavior.

What good looks like: The evidence shows the same underlying behavior described by the issue, including the relevant error, output, or observable result. Evidence of a different or merely related failure does not establish the issue's behavior.

## Honesty

Where it lives: In an eval bundle, compare the claim comment and the repro report's stated outcome with the actual reproduction evidence, output, and logs. In live mode, compare the student's draft claim with the evidence they actually produced.

What good looks like: The claim describes what the evidence supports and does not imply more certainty than the reproduction establishes. An evidenced cannot-reproduce result is stated as such and is acceptable; a claim of reproduction or confirmation without supporting evidence is not.

## Comms

Where it lives: In an eval bundle, compare the claim comment against the issue, and compare the reproduction report/comments against the repo-facts block, repository documentation, templates, contribution policy, and any stated AI-use disclosure requirements. In live mode, inspect the issue thread, repo documentation, contribution guidelines, and student's draft comment/report.

What good looks like: The wording accurately identifies the issue and the evidence without boilerplate claims or unsupported conclusions. Repository-specific requirements, including applicable templates and AI-use disclosures, are followed, and the communication distinguishes observed facts from assumptions or unsupported claims.
