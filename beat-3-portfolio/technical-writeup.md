# An AI toolkit for open source contribution

## Overview
An AI toolkit for open-source contribution is a Claude Code-powered workflow I built to help identify suitable open-source issues and guide contributors through making meaningful contributions. The problem was that finding a project that matched a given contributor's skills, experience, and contribution preferences required manually evaluating repositories, issue availability, maintainer activity, and project policies. I developed a structured issue-scanning workflow with a custom fit rubric, search strategy, and contribution guidelines to automate discovery and evaluate issues against these criteria. I wrote the rubric, search strategy, and supporting project instructions myself, including rules for assessing project fit, contribution scope, and AI-assistance policies. I used the toolkit to scan and evaluate hundreds of issues, refine its filtering criteria, and select a suitable contribution for myself: [rikaikun #790](https://github.com/melink14/rikaikun/issues/790), addressing overly broad TypeScript `any` types. The project resulted in a repeatable, AI-assisted process for moving from issue discovery to a well-scoped open-source contribution.

## What Happened: Building and Improving the Toolkit

I started by building an AI-assisted issue discovery workflow using Claude Code. My goal was to find open-source issues that were actively maintained, unclaimed, well-scoped, and compatible with my background in software engineering and AI engineering. I created a search strategy and an issue-fit rubric to evaluate candidates against those requirements.

On October 18, my first scan returned 180 unique issues, with 173 remaining after filtering for unassigned issues. However, the results exposed a weakness in my rubric. The toolkit accepted `ecogetaway/oss-language-inclusion#24` because its repository was primarily Python, even though the actual task involved translating Hindi strings in a `.po` file. The repository's language was passing the check, but the work itself did not match my software engineering goals.

**Proof 1 – First scan exposed a false positive:**

From my actual `scan-output.md`:

```text
ACCEPTED
ecogetaway/oss-language-inclusion#24

language pass (Python)

Fit: Python repo with 2/2 preferred passes.
Tension: the real work is a Hindi translation of a
.po file in a different repo.
```

This made me realize that repository-level language matching was not enough to establish whether an issue was a good fit.

I revised my evaluation approach to distinguish between a repository's primary language and the actual work required by an issue. I also refined my profile criteria: Python remained my preferred language, but other programming languages were no longer automatic dealbreakers. I adjusted the scope evaluation to distinguish between work that was too broad and work that was simply more challenging than expected.

I then used the revised criteria to evaluate additional candidates. The toolkit identified opportunities such as PyTorch ExecuTorch issue #10580, involving adding `etdump` output to `qnn_llama_runner`, and eventually surfaced a particularly suitable TypeScript issue in Rikaikun.

**Proof 2 – Updated evaluation of the selected issue:**

From my actual issue evaluation output:

```json
{
  "item": "melink14/rikaikun#790",
  "checks": [
    {"name": "maintainer-commits", "grade": "pass"},
    {"name": "AI policy", "grade": "pass"},
    {"name": "unclaimed-issue", "grade": "pass"},
    {"name": "latest-release-within-a-year", "grade": "pass"},
    {"name": "preferred-language", "grade": "fail"},
    {"name": "scope", "grade": "pass"},
    {"name": "profile-fit", "grade": "pass"}
  ],
  "verdict": "accept"
}
```

The issue proposed replacing a broadly typed `any` variable in `extension/rikaicontent.ts` with properly typed variables. Although the repository used TypeScript rather than Python, the actual task was a bounded software engineering improvement that matched my experience.

The outcome was a refined, repeatable issue-discovery toolkit and a selected contribution target: [Rikaikun #790](https://github.com/melink14/rikaikun/issues/790). At the end of this stage, the issue had no assignee or linked pull request, and I had identified the specific code location requiring improvement. The issue selection was complete, but an implementation, pull request, or maintainer acceptance had not yet been documented.

## Limitations and what's next

The toolkit successfully narrowed down hundreds of open-source issues into a smaller set of relevant opportunities, but it does not guarantee that an issue will ultimately lead to an accepted contribution. Its evaluations depend on the information available through GitHub, which can be incomplete or outdated. For example, an issue may appear unclaimed even if someone is already discussing it outside the issue thread. The toolkit also evaluates whether an issue appears suitable, but it cannot fully determine complexity or guarantee that a local development environment will support the required tests and hardware.

Another limitation I identified was that repository-level language information could produce misleading recommendations when the actual task involved a different type of work. I addressed this by making profile fit depend more heavily on the issue's specific requirements rather than the repository's primary language.

Next, I would improve the toolkit by adding a stronger issue-level task classification step, more explicit confidence ratings, and a way to track selected issues through implementation, testing, pull request submission, and maintainer feedback. I would also expand the evaluation process to verify build and test prerequisites before recommending an issue. This would move the toolkit toward a more complete, end-to-end open-source contribution workflow.