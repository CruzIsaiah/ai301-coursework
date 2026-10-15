# Plan: Fix parenthesized US phone number redaction



## Diagnosis



Issue #53 reports that `PIIScrubber` does not redact or detect parenthesized US phone numbers such as `(555) 123-4567`.



My Unit 2 reproduction confirmed the reported behavior on the fork's `main` branch:



    'Call me at (555) 123-4567 or [REDACTED]'



and:



    []



for:



    s.detect("Call me at (555) 123-4567")



The dashed control worked correctly:



    'Call me at [REDACTED]'



and `detect()` returned a `phone_us` match for `555-123-4567`.



The four phone-specific tests named in the issue also reproduced the problem as expected:



    test_us_phone_number_redaction XFAIL

    test_us_phone_formats XFAIL

    test_detect_phone_pii XFAIL

    test_phone_at_start_of_text XFAIL



After reproducing the issue, I inspected `PII_PATTERNS["phone_us"]` in `safety/pii_scrubber.py`. The current pattern is:



    \b(?:\+?1[-.]?)?\(?([0-9]{3})\)?[-.]?([0-9]{3})[-.]?([0-9]{4})\b



There are two relevant problems.



First, the separator positions allow only `-` or `.`, so the literal space after `)` in `(555) 123-4567` cannot match.



Second, the leading `\b` occurs before the optional opening parenthesis. A complete parenthesized match can therefore fail to begin at `(`. The fix should redact and detect the complete phone number, including the parentheses, instead of matching only the digits and leaving `(` behind.



## Scope



### In scope



- Update only `PII_PATTERNS["phone_us"]` in `safety/pii_scrubber.py`.

- Support `(555) 123-4567` and the other US formats already expected by the test suite.

- Preserve dashed and dotted formats.

- Make `scrub()` redact the complete parenthesized number.

- Make `detect()` return the complete parenthesized value and correct positions.

- Update all test metadata currently tied to issue #53.



### Out of scope



- Changes to `email`, `phone_intl`, `ssn`, or `street_address`.

- Changes to the public `scrub()` or `detect()` APIs.

- Fixing the unrelated `street_address` false positive that currently affects `test_mixed_pii_and_text`.

- A broader redesign of the PII scrubber.



## Files to change



### `safety/pii_scrubber.py`



Change only `PII_PATTERNS["phone_us"]`.



The intended form is:



    (?<!\w)(?:\+?1[-. ]?)?(?:\([0-9]{3}\)|[0-9]{3})[-. ]?[0-9]{3}[-. ]?[0-9]{4}(?!\w)



This changes the boundaries so a complete match may begin at `(`, requires balanced parentheses when the parenthesized area-code form is used, and allows a literal space in addition to dash and dot separators.



### `tests/unit/test_pii_scrubber.py`



Remove the issue #53 `strict=True` xfail markers from the four phone-specific tests once they pass:



- `test_us_phone_number_redaction`

- `test_us_phone_formats`

- `test_detect_phone_pii`

- `test_phone_at_start_of_text`



There is also a fifth test, `test_mixed_pii_and_text`, whose current `xfail` reason names issue #53. Its phone number is already in the supported dashed form, and its actual failure is the separate `street_address` over-match. I will remove issue #53 as the reason that suppresses this test. I will keep the unrelated failure explicitly identified as a separate known `street_address` failure rather than fixing that regex as part of this change.



This ensures issue #53 is no longer used as an xfail reason anywhere after the phone bug is fixed while keeping the unrelated defect outside this implementation.



## Approach



1. Replace the leading and trailing word boundaries with lookarounds that prevent matching inside a larger word or identifier while allowing the complete match to begin with `(`.



2. Represent the area code as either three bare digits or three digits enclosed by balanced parentheses.



3. Allow a literal space alongside `-` and `.` at the supported separator positions.



4. Do not use `\s`, because that would also allow tabs and newlines and could join unrelated text across lines.



5. Keep `scrub()` and `detect()` unchanged. Both already consume the regex match, so correcting the pattern should fix both behaviors.



6. Remove the four phone-specific issue #53 xfail markers after the updated pattern makes those tests pass.



7. Remove the issue #53 association from `test_mixed_pii_and_text` while keeping its unrelated `street_address` failure clearly separated from this fix.



## Test plan



First, rerun the Unit 2 reproduction.



Before the fix:



    'Call me at (555) 123-4567 or [REDACTED]'

    []



After the fix, I expect:



    'Call me at [REDACTED] or [REDACTED]'



For:



    s.detect("Call me at (555) 123-4567")



I expect one `phone_us` detection whose value is exactly:



    (555) 123-4567



and whose positions cover the complete value.



Then run the four phone-specific issue tests and confirm they pass normally instead of `XFAIL`.



Verify existing and newly supported forms, including:



    555-123-4567

    555.123.4567

    (555) 123-4567

    (555)123-4567

    +1 555 123 4567



Also add or run negative controls to make sure the broader separator support does not match inside longer identifiers or join groups across a newline.



Then run:



    .\.venv\Scripts\python.exe -m pytest tests/unit/test_pii_scrubber.py -v -m unit



Finally, run the repository-required checks that are available in the local environment. Any failure unrelated to the phone-number change will be recorded rather than silently fixed.



## Risks and unknowns



Allowing literal spaces makes the phone regex more permissive, so it could create false positives for unrelated groups of digits. I will test representative negative cases and keep the separator class limited to literal space, dash, and dot rather than using `\s`.



Changing the opening boundary could also cause matches inside larger identifiers if it is too permissive. The lookarounds are intended to prevent that, and I will verify this with negative controls.



`test_mixed_pii_and_text` is currently marked as issue #53 even though its reproduced failure comes from `street_address`. I will remove issue #53 from that suppression without expanding this fix into the address regex.



## Deviations



There were no implementation deviations from the accepted plan. The `phone_us` regex was updated as planned, the four phone-specific issue #53 xfail markers were removed, and `test_mixed_pii_and_text` remained isolated under its separate `street_address` failure.



Post-change verification:

- PII scrubber tests: 24 passed, 1 xfailed.

- Full test suite: 379 passed, 49 xfailed.

- Ruff: all checks passed.

- Black: 110 files unchanged.

- Mypy passed when run with the repository's CI scope.

