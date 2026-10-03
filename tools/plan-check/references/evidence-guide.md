# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

Where it lives: In an eval package, read the Repro evidence block for the reproduced behavior, steps, environment, expected result, and actual result. Read the Candidate plan for its stated cause. In live mode, use the student's posted reproduction comment on the issue for the reproduction evidence and the draft plan.md for the diagnosis.

What good looks like: The stated cause explains the failure that the reproduction actually demonstrates and is consistent with the observed failure point. A diagnosis that only repeats the symptom, ignores important reproduction evidence, or contradicts it is not grounded.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

Where it lives: In an eval package, read the Issue block for the problem being addressed, the Repo facts block for repository constraints and relevant facts, and the Candidate plan for its stated change, exclusions, and affected files or areas. In live mode, read the issue, repository facts or contribution documentation identified in the package, and the draft plan.

What good looks like: The proposed work is limited to the diagnosed problem and identifies meaningful boundaries on what will and will not change. The scope should not introduce unrelated cleanup, redesign, or behavior changes that the issue and evidence do not require.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

Where it lives: In an eval package, read the Candidate plan for the files or areas to change, implementation approach, and order of work, then compare those statements with the Repo facts block. In live mode, use plan.md and the relevant repository files or documentation named by the evidence guide.

What good looks like: A developer unfamiliar with the plan can identify where the change belongs and the core sequence of implementation without having to guess a missing essential decision. The plan should connect the diagnosed cause to concrete changes in the affected code or documentation.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

Where it lives: In an eval package, read the Repro evidence block for the original reproduction steps, expected result, and actual result, then read the Candidate plan for its test plan and expected post-fix behavior. Use the Repo facts block when repository-specific test commands or conventions affect how the behavior can be verified. In live mode, use the student's posted repro comment and the draft plan's test plan.

What good looks like: The planned test exercises the real affected behavior, includes the reproduced failure case, and states an observable result that should occur after the fix. A decisive test can distinguish the broken behavior from the fixed behavior rather than only showing that a command ran.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

Where it lives: In an eval package, read the Candidate plan for risks and unknowns and, when present, its deviations. Compare those statements with the Issue, Repro evidence, and Repo facts. In live mode, read the draft plan's risks, unknowns, and ## Deviations section.

What good looks like: Material uncertainty is explicitly treated as uncertainty, and unsupported assumptions are not presented as established facts. After implementation, a change from the posted plan is recorded under ## Deviations with what changed and why; a blank or omitted deviation record does not provide evidence that the build matched the plan.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

Where it lives: In an eval package, read the Candidate plan comment against the Issue and Thread highlights, then compare it with the Repo facts block for contribution conventions, templates, maintainer requests, and any AI-use disclosure requirement. In live mode, read the actual issue thread and repository contribution guidance alongside the draft comment.

What good looks like: The comment communicates the proposed change in a way that responds to relevant issue and maintainer context instead of using generic boilerplate. It follows stated repository conventions and does not omit a required disclosure or other material thread/repository requirement.
