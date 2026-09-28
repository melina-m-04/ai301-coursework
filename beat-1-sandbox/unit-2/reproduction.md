# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

melina-m-04

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5861015535

"I’d like to investigate issue #72: verify_password in core/security.py raises passlib.exc.UnknownHashError when given the malformed stored hash used by test_verify_with_wrong_hash_format, instead of returning False.

I’ll reproduce the reported behavior against the documented test case in a clean environment, record the environment, commands, and result, and share the reproduction evidence here before proposing a fix. If reproduced, I’ll also check the covering xfail test (manifest H-05) as part of the follow-up."

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5861277597

"Reproduced.

Environment: macOS 15.7.3 (build 24G419, arm64), Python 3.11.3 in a fresh virtual environment. Repo at commit f89c06f on main, clean working tree. Installed: passlib 1.7.4, bcrypt 4.3.0, python-jose 3.5.0, cryptography 50.0.1, pydantic 2.13.5, pydantic-settings 2.15.0, pytest 9.1.1. The package itself is not installed (pip install -e . not run), so both commands below are run from the repository root. Docker/database services were not required because verify_password in core/security.py has no database dependency.

Steps:

Ran:

python -m pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format -v
Result: 1 xfailed, confirming the test is currently marked as an expected failure for issue verify_password raises UnknownHashError on malformed stored hashes instead of returning False #72 / manifest H-05.

Ran:

python -m pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format -v --runxfail
Result: 1 failed.

The failure occurs when the test calls:

verify_password("password", "not_a_valid_bcrypt_hash")
The traceback ends with:

passlib.exc.UnknownHashError: hash could not be identified
Inspected core/security.py. verify_password currently delegates directly to:

return bool(pwd_context.verify(plain_password, hashed_password))
with no handling for an unrecognized stored hash.

Result: The issue is reproduced. A malformed/unrecognized stored hash causes verify_password to raise passlib.exc.UnknownHashError instead of returning False, matching the behavior described in issue #72."

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

18/20 → 18/20 → 20/20

**Package analysis**

pkg-19: The rubric decided reject, and the gold label was reject. The revised rubric required the candidate comment to state issue-specific intent rather than making a generic commitment that could apply to any issue. For this package, the rubric's required checks were not satisfied, so it correctly matched the gold reject label.

**Check rationale**

""The comment states what the author actually did and what they intend to do next in terms specific to this issue, and makes no commitment the author cannot honestlyback: no fixed delivery deadline, no guaranteed fix, no request to reserve or hold the issue. A comment whose stated intent would read identically on any other issue fails""

I revised the rubric to add the claim-intent check because the earlier rubric could accept comments that did not clearly state issue-specific intent. This makes the rubric distinguish a genuine, issue-specific claim from a generic or unfollowable commitment.

**Trade-offs**

The revised claim-intent check changed the treatment of cases where a comment sounded like a claim but did not contain issue-specific intent. I accepted that this could reject some superficially plausible comments in exchange for avoiding false accepts. The final full evaluation confirmed that this change did not reduce agreement elsewhere: the run achieved 20/20, with all category floors passing.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
