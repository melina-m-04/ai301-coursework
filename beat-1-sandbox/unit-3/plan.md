# Plan: Fix `verify_password` handling of malformed hashes

## Diagnosis

Issue #72 occurs because `verify_password` delegates directly to `pwd_context.verify(plain_password, hashed_password)` without handling malformed or unrecognized stored-hash input.

My Unit 2 reproduction showed:

> `passlib.exc.UnknownHashError: hash could not be identified`

when calling:

> `verify_password("password", "not_a_valid_bcrypt_hash")`

The reproduction also showed that the existing regression test is currently reported as `1 xfailed`, while running the same test with `--runxfail` produces `1 failed`.

The issue requires malformed-hash verification to fail closed by returning `False`. The issue thread also contains evidence of another malformed-hash shape: a bcrypt-prefixed but structurally invalid value such as `$2b$notarealhash` can raise a bare `ValueError`.

Therefore, the implementation needs to handle the malformed-hash exceptions raised by `pwd_context.verify`, rather than only the specific exception from my original reproduction.

## Scope

### In scope

* Update `core/security.py` so `verify_password` catches `ValueError` raised by malformed or unrecognized stored-hash input and returns `False`.
* Update `tests/unit/test_security.py` so the existing malformed-hash regression test is no longer marked `xfail`.
* Add regression coverage for the malformed bcrypt-prefixed case `$2b$notarealhash`.
* Run the affected security tests and the repository's unit and code-quality checks.

### Out of scope

* Changing password hashing algorithms or `CryptContext` configuration.
* Changing behavior for valid bcrypt hashes or incorrect passwords.
* Changing authentication flows outside `verify_password`.
* Changing dependencies or Passlib versions.
* Changing JWT or token-related functions.
* Refactoring unrelated security code.
* Bulk lint, formatting, or type-check cleanup unrelated to this issue.

## Files to touch

* `core/security.py` — catch `ValueError` around `pwd_context.verify(...)` and return `False`.
* `tests/unit/test_security.py` — remove the existing `xfail` marker and add coverage for the malformed bcrypt-prefixed hash.

## Approach

1. Update `verify_password` in `core/security.py` to catch `ValueError` around the existing `pwd_context.verify(...)` call and return `False`.
2. Use `ValueError` rather than a broader `Exception` handler because the original reproduction raises `UnknownHashError`, while the issue-thread evidence shows that another malformed bcrypt-prefixed hash can raise `ValueError` directly. `UnknownHashError` is covered by this targeted `ValueError` handler.
3. Preserve the existing behavior for recognized hashes: matching passwords should continue to return `True`, and incorrect passwords should continue to return `False`.
4. Remove the `@pytest.mark.xfail` marker from `test_verify_with_wrong_hash_format`.
5. Add a regression test for `$2b$notarealhash` that asserts `verify_password` returns `False`.
6. Review the complete diff to ensure no unrelated code or tests are changed.

## Test plan

### Before the fix

Run:

```text
python -m pytest tests/unit/test_security.py -k test_verify_with_wrong_hash_format -v --runxfail
```

Expected baseline:

```text
1 failed
```

with the traceback ending in:

```text
passlib.exc.UnknownHashError: hash could not be identified
```

### After the fix

Run:

```text
python -m pytest tests/unit/test_security.py -k "wrong_hash_format or malformed_bcrypt_hash" -v
```

Expected result:

```text
2 passed
```

The two regression cases should both return `False` without raising `UnknownHashError` or `ValueError`.

Then run:

```text
python -m pytest tests/unit/test_security.py -v
```

Expected result: all tests in `test_security.py` pass.

Then run:

```text
make test-unit
```

Expected result: the repository unit-test suite passes with no failure or `XPASS(strict)` caused by issue #72.

Then run:

```text
make check
```

Expected result: Ruff, Black, and mypy complete successfully with no new failures caused by this change.

The decisive behavior is that both `not_a_valid_bcrypt_hash` and `$2b$notarealhash` cause `verify_password` to return `False` rather than raising.

## Risks and unknowns

* The exact malformed-hash exceptions depend on how Passlib parses the stored value. The current reproduction demonstrates `UnknownHashError` for `not_a_valid_bcrypt_hash`, while the issue-thread evidence reports `ValueError` for `$2b$notarealhash`.
* The exception handling should stay limited to `ValueError` rather than catching all exceptions, so unrelated runtime or programming failures are not silently converted into authentication failures.
* Existing valid bcrypt verification behavior should remain unchanged.
* No dependency upgrade is planned.
* The two malformed-hash examples in the available evidence may not represent every possible malformed stored-hash input; the implementation should therefore be tested against the demonstrated cases without claiming exhaustive coverage.

## Deviations

No implementation deviation occurred. The change was implemented as planned in `core/security.py` and `tests/unit/test_security.py`.

During validation, the existing `.venv` was initially missing the repository's declared runtime and development dependencies. As a result, the initial `make test-unit` and `make check` attempts could not complete. I installed the repository's declared `.[dev]` dependencies using the setup path defined by the Makefile and reran the checks successfully.

After dependency setup, `make test-unit` completed with 377 passed tests and 52 expected failures. `make check` passed: Ruff reported all checks passed, Black reported 110 files unchanged, and mypy reported no issues in 76 source files. See `test_evidence.md` for the recorded command results.
