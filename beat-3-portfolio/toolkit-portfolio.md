# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

This file is Assignment 6, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. It has been waiting here since you created the repo in unit 1;
unit 9 is when you write it.

**Only this page is read.** Your `tools/` folders and your installed skill folders are never
opened, so every piece of evidence you want seen has to live inline here: an output excerpt,
a before/after pair, a dated commit reference.

**Write every sentence yourself.** AI may gather diffs, dates and excerpts for you; it does
not draft entries.

**Keep every section header below under its exact name** — Featured Tools, Inventory, The
Arc, and Limitations and What's Next. Feature three or four tools, each in the entry shape
shown below; give every other tool one inventory line.

**Some lines below are labelled, and the label is how they are read.** Three places on this
page use a `Label: your words` shape — the arc's beats, the tool-limits list, and nothing
else. Keep those labels exactly as written, one per line, and never delete a labelled line:
where you have nothing to put after a label, write `none` and move on. A deleted label reads
as a deleted answer.

**Before you finish**, replace every `[bracketed prompt]` with your own words, then delete
the unused `[Tool name]` entry stub, its copy-me sentence, and the prompt sentences under
each header. A leftover bracketed prompt reads as unfilled.

**Student:** Melina Marjani

# Toolkit Portfolio

## Featured Tools

I chose these tools because they represent the main parts of my open-source contribution workflow: discovering potential issues, evaluating whether they are appropriate for my skills and constraints, and narrowing the search to manageable work. I focused on tools that demonstrate how the workflow developed through actual use, particularly where an initial evaluation exposed a weakness that needed to be addressed.

**issue-scout**

**What it is, and the judgment hole I wrote:** An AI-assisted workflow for finding and evaluating open-source issues. It searches GitHub for good-first-issue and help-wanted issues, then evaluates candidates against criteria such as project activity, contribution policy, whether an issue is claimed, and whether the work is manageable. The judgment I contributed was defining what makes an issue a worthwhile opportunity rather than treating every search result as a good candidate.

**How it evolved, dated:** October 18–19, 2026: I ran a scan combining good-first-issue and help-wanted searches. The results exposed a weakness in relying too heavily on repository-level information when evaluating whether an issue matched my experience. The evaluation was refined to pay closer attention to the actual task and its requirements.

**Evidence:**
- Scan dated October 18, 2026, with results through October 19, 2026 at 01:12 UTC.
- Combined search results: **180 unique issues**.
- Issues remaining unassigned after the initial filter: **173**.
- Results were ranked by comment count, then update date, then search order.
- The workflow evaluated project activity, AI contribution policy, issue status, release recency, language, scope, and profile fit.

**Issue-fit rubric**

**What it is, and the judgment hole I wrote:** A set of evaluation criteria used to decide whether an issue is worth pursuing. It considers recent maintainer activity, AI contribution restrictions, whether the issue is unclaimed, release recency, preferred language, task scope, and fit with my software engineering and AI engineering experience. The judgment I contributed was distinguishing an issue's apparent suitability from whether its actual requested work was appropriate for my skills and interests.

**How it evolved, dated:** October 2026: The rubric was adjusted after an issue demonstrated that a repository's primary programming language could be misleading. The scope assessment was also refined so that broad or multi-part tasks could be evaluated by their actual difficulty rather than automatically being rejected. The revised approach looked for at least one identifiable piece of work and classified difficulty as straightforward, moderate, or ambitious.

**Evidence:**
- `ecogetaway/oss-language-inclusion#24` exposed a false positive: the repository was identified as Python, but the actual work involved a Hindi translation of a `.po` file in a TypeScript application.
- The Rikaikun issue evaluation passed the scope and profile-fit checks despite TypeScript being outside my preferred language.
- Rikaikun issue #790 requested replacing `let rp: any` in `rikaicontent.ts` with appropriately typed variables, providing a bounded type-safety task.

**Search strategy**

**What it is, and the judgment hole I wrote:** A repeatable approach to finding contribution opportunities through GitHub issue searches. It combines good-first-issue and help-wanted searches and uses filtering and ranking to reduce the results to a manageable candidate pool. The judgment I contributed was balancing broad discovery with criteria that prioritize relevant, actionable issues instead of simply selecting the first available result.

**How it evolved, dated:** October 18–19, 2026: The search strategy was used to collect 180 unique results from two issue categories. The results were then filtered for assignment status and ranked using comment count and update recency. The subsequent evaluation showed that search results still needed task-level review before being considered suitable.

**Evidence:**
- Search categories: good-first-issue and help-wanted.
- 180 unique results collected.
- 173 unassigned results after the initial filter.
- LogSpecter issues #23, #12, #24, and #29 were rejected because their requested work was broad or involved multiple parts.
- Rikaikun issue #790 was accepted as a candidate because it described a single, bounded TypeScript refactor.

## Inventory

- **GitHub CLI (`gh`):** Used to authenticate with GitHub and support issue discovery and repository research.
- **`issue-scout` skill:** Main AI-assisted workflow for discovering and evaluating open-source issues.
- **Issue-fit rubric:** Evaluation criteria for project activity, AI policy, claim status, release recency, language, scope, and profile fit.
- **Search strategy:** Combines good-first-issue and help-wanted searches and filters and ranks the results.
- **Scope guidance:** Helps distinguish a manageable, identifiable work item from a broad or multi-part issue.
- **Voice guard:** A `PreToolUse` Bash hook that checks commands against a voice guide before execution. Its behavior was demonstrated when it blocked a GitHub issue-comment command without a comment body.

## The Arc

**Beat 1**

Date: Sep 16 - Oct 7, 2026

Friction: Searching GitHub produced a large number of potential issues, making it difficult to identify which ones were actually suitable for a contribution.

Change: I combined good-first-issue and help-wanted searches and applied filters and ranking criteria to narrow the results.

Result: The scan collected 180 unique issues and reduced the initial candidate pool to 173 unassigned issues.

**Beat 2**

Date: Oct 14 - Nov 4, 2026

Friction: Repository-level information could make an issue appear suitable even when the actual task did not match my skills or preferences. For example, a Python repository contained an issue involving a Hindi translation in a TypeScript application.

Change: I refined the evaluation to distinguish the repository's primary language from the language and work actually required by the issue. I also adjusted scope evaluation to consider identifiable work and difficulty rather than automatically rejecting broader issues.

Result: The updated evaluation identified Rikaikun issue #790 as a suitable candidate despite its TypeScript language, because the requested refactor was bounded and aligned with my software engineering experience.

**Beat 3**

Date: Nov 11 - 18, 2026

Friction: Some issues appeared relevant but required too much work or contained several separate tasks, making them difficult to approach as a focused contribution.

Change: I used the scope criteria to identify whether an issue contained at least one clearly identifiable piece of work and considered its difficulty.

Result: LogSpecter issues #23, #12, #24, and #29 were rejected because their requested work was broad or multi-part.

**Beat 4**

Date: Nov 11 - 18, 2026

Friction: An issue could pass the initial evaluation but still be difficult to implement if the required local environment could not build or test the relevant software.

Change: I added an environment-feasibility consideration when evaluating the ExecuTorch candidate.

Result: ExecuTorch issue #10580 was accepted as a candidate to investigate, with a follow-up check to determine whether the local environment could build and test the QNN runner before implementation.

## Limitations and What's Next

The toolkit improves issue discovery and evaluation, but it does not guarantee that a selected issue can be implemented successfully. GitHub issue information can become outdated, an issue can be claimed after it is found, and passing the rubric does not prove that the local development environment has all the required dependencies. The workflow also stops at issue selection and evaluation; it does not independently complete implementation, testing, pull-request submission, or maintainer review.

Next, I would connect issue evaluation more closely with repository setup and feasibility checks. I would also make the scan easier to reproduce, preserve dated evaluation results, and track selected issues through implementation and pull-request feedback. This would help measure whether the workflow identifies not just promising issues, but issues that can realistically become completed contributions.

**Tool limits.**

issue-scout: It identifies and evaluates potential issues, but it cannot guarantee that an issue remains available, that the local environment can build and test the project, or that a selected issue will result in a successful contribution.

Issue-fit rubric: Its results depend on the accuracy and completeness of repository and issue information. A passing evaluation is a judgment aid, not proof that an issue is the right choice.

Search strategy: It depends on GitHub search results and filters, so relevant issues may be missed, and a large candidate pool still requires manual review.
