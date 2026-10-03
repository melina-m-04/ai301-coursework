# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

## Posted upstream

**GitHub username**

melina-m-04

**Plan comment**

<https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5974313997>

I reproduced issue #72 on the current `main` commit.

The affected call is `verify_password("password", "not_a_valid_bcrypt_hash")`. With `--runxfail`, the existing regression test fails with:

```text
passlib.exc.UnknownHashError: hash could not be identified
```

`verify_password` currently delegates directly to `pwd_context.verify(...)` without handling an unrecognized stored hash.

### Plan

I’ll make the smallest change in `core/security.py`: catch `passlib.exc.UnknownHashError` in `verify_password` and return `False`, while preserving the existing behavior for recognized hashes.

I’ll update `tests/unit/test_security.py` by removing the existing `xfail` marker from `test_verify_with_wrong_hash_format`, so the test directly verifies that a malformed hash returns `False`.

I’ll re-run the reproduced test case, then run `make test-unit` and `make check`. I’m not planning dependency changes, hashing-algorithm changes, or unrelated security refactors.

The issue's expected behavior is a fail-closed `False` result for an unrecognized stored hash.

## Your branch

**Branch**

fix/72-handle-malformed-hash

**Evidence**

Before:

```text
Reproduced.

Environment: macOS 15.7.3 (build 24G419, arm64), Python 3.11.3 in a fresh virtual environment. Repo at commit `f89c06f` on `main`, clean working tree. Installed: passlib 1.7.4, bcrypt 4.3.0, python-jose 3.5.0, cryptography 50.0.1, pydantic 2.13.5, pydantic-settings 2.15.0, pytest 9.1.1. The package itself is not installed (`pip install -e .` not run), so both commands below are run from the repository root. Docker/database services were not required because `verify_password` in `core/security.py` has no database dependency.

Steps:

1. Ran:
   python -m pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format -v

   Result: `1 xfailed`, confirming the test is currently marked as an expected failure for issue #72 / manifest H-05.

2. Ran:
   python -m pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format -v --runxfail

   Result: `1 failed`.

   The failure occurs when the test calls:
   verify_password("password", "not_a_valid_bcrypt_hash")

   The traceback ends with:
   passlib.exc.UnknownHashError: hash could not be identified

3. Inspected `core/security.py`. `verify_password` currently delegates directly to:
   return bool(pwd_context.verify(plain_password, hashed_password))

   with no handling for an unrecognized stored hash.

Result: The issue is reproduced.
```

After:

```text
(.venv) melina@mac pathreview-ai301-fa26-s1 % python -m pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format -v

tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED

==================================== 1 passed, 25 deselected, 2 warnings in 0.22s ====================================
```

```text
(.venv) melina@mac pathreview-ai301-fa26-s1 % python -m pytest tests/unit/test_security.py -k test_verify_password_with_malformed_bcrypt_hash -v

tests/unit/test_security.py::TestSecurity::test_verify_password_with_malformed_bcrypt_hash PASSED

==================================== 1 passed, 25 deselected, 2 warnings in 0.20s ====================================
```

```text
(.venv) melina@mac pathreview-ai301-fa26-s1 % python -m pytest tests/unit/test_security.py -k "wrong_hash_format or malformed_bcrypt_hash" -v

tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED
tests/unit/test_security.py::TestSecurity::test_verify_password_with_malformed_bcrypt_hash PASSED

================================================== 2 passed, 24 deselected, 2 warnings in 0.15s ================================================
```

```text
(.venv) melina@mac pathreview-ai301-fa26-s1 % python -m pytest tests/unit/test_security.py -v

================================================== 26 passed, 2 warnings in 5.55s ============================================
```

```text
(.venv) melina@mac pathreview-ai301-fa26-s1 % make test-unit

==================================== 377 passed, 52 xfailed, 4 warnings in 6.55s =====================================
```

```text
(.venv) melina@mac pathreview-ai301-fa26-s1 % make check

.venv/bin/ruff check .
All checks passed!
.venv/bin/black .
All done! ✨ 🍰 ✨
110 files left unchanged.
.venv/bin/mypy api/ core/ ingestion/ rag/ agent/ safety/
Success: no issues found in 76 source files
```

## Eval iterations

**Run history**

20/20 scored items (first and only full eval run)

**Package analysis**

pkg-01: my rubric decided `reject`, and the gold label was `reject`.

The package is in the `wrong-cause` category. The candidate plan says the request-item tokenizer is the cause, but the reproduction evidence shows that the failure occurs in argparse while consuming positional arguments. My `Diagnosis` check therefore rejected the plan because its stated cause contradicts the reproduced failure point. The rubric correctly agreed with the gold label.

**Check rationale**

Exact check from `tools/plan-check/rubric.md`:

> `| Diagnosis | The plan's stated cause read against the reproduction evidence's observed behavior, inputs, and failure point | Pass if the diagnosis explains the reproduced failure without contradicting the evidence and identifies a cause that the proposed change can address; fail if it ignores, contradicts, or merely restates the symptom as the cause | required |`

I wrote this check to force the diagnosis to be grounded in the reproduction rather than judged by how convincing or detailed the explanation sounds. I specifically chose to require the stated cause to explain the observed failure and to reject plans that contradict the failure point or merely restate the symptom.

**Trade-offs**

This check can reject a plan when the available reproduction evidence does not fully establish the root cause, even when the proposed implementation might ultimately work. I accepted that trade-off because the purpose of the rubric is to prevent unsupported diagnoses from being posted and built from; uncertainty should be recorded instead of treated as a confirmed cause.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
