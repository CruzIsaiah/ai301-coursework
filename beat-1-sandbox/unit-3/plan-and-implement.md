# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

CruzIsaiah

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53#issuecomment-6180327397

Following up on my Unit 2 reproduction for issue #53.

I reproduced the reported behavior on the fork's current main: scrub() leaves (555) 123-4567 visible while redacting 555-123-4567 in the same string, and detect() returns no phone match for the parenthesized form. The four phone-specific tests named in the issue also xfail.

After the reproduction, I inspected PII_PATTERNS["phone_us"] in safety/pii_scrubber.py. The pattern allows dash and dot separators but not the literal space after ), and its leading \b comes before the optional opening parenthesis. My plan is to change only this pattern so the complete parenthesized value can match, allow literal spaces alongside the existing dash/dot separators, and preserve protection against matching inside larger identifiers.

I will update tests/unit/test_pii_scrubber.py as part of the same change. The four phone-specific issue #53 tests should become normal passing tests. A fifth test, test_mixed_pii_and_text, also currently has an issue #53 xfail marker, but while checking it separately I found that its failing assertion is caused by the street_address pattern over-matching ordinary text rather than the phone pattern. I plan to keep that address defect outside this fix. Would you prefer that I relabel its xfail reason to describe the address over-match, or leave it for a separate issue?

For verification, I will rerun the Unit 2 reproduction and require (555) 123-4567 to be fully replaced by [REDACTED] and returned by detect() as one complete phone_us match. I will run the phone-specific tests, the full PII scrubber test file, and negative controls for over-matching. I am using a literal space rather than \s so the pattern cannot span tabs or newlines.

The main risk is that accepting spaces makes the regex more permissive, so I will specifically check that the change does not match inside longer identifiers or join unrelated digit groups across lines.

---

## Your branch

**Branch**

fix/53-parenthesized-phone-redaction

**Evidence**

Before, from my Unit 2 reproduction:

```text
>>> s.scrub("Call me at (555) 123-4567 or 555-123-4567")
'Call me at (555) 123-4567 or [REDACTED]'

>>> s.detect("Call me at (555) 123-4567")
[]
```

I also ran:

```text
$ ./.venv/Scripts/python.exe -m pytest tests/unit/test_pii_scrubber.py -v -m unit
```

Relevant output before the fix:

```text
tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_us_phone_number_redaction XFAIL
tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_us_phone_formats XFAIL
tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_detect_phone_pii XFAIL
tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_phone_at_start_of_text XFAIL
======================== 20 passed, 5 xfailed in 0.98s ========================
```

After building the change, I reran the behavior check:

```text
PS> .\.venv\Scripts\python.exe -c "from safety.pii_scrubber import PIIScrubber; s=PIIScrubber(); print(s.scrub('Call me at (555) 123-4567 or 555-123-4567')); print(s.detect('Call me at (555) 123-4567'))"
```

Output:

```text
Call me at [REDACTED] or [REDACTED]
[{'type': 'phone_us', 'value': '(555) 123-4567', 'start': 11, 'end': 25}]
```

Then I reran the PII scrubber tests:

```text
PS> .\.venv\Scripts\python.exe -m pytest tests/unit/test_pii_scrubber.py -v -m unit
```

Result:

```text
24 passed, 1 xfailed
```

The four phone-specific issue #53 tests now pass normally. `test_mixed_pii_and_text` remains the single expected failure under its separate `street_address` reason.

I also verified the full suite and repository checks:

```text
pytest: 379 passed, 49 xfailed
ruff: All checks passed!
black: 110 files would be left unchanged
mypy using the repository CI scope: no issues found in 76 source files
```

## Eval iterations

**Run history**

The eval runs, in order, were:

```text
16/20
3/3 targeted rerun
4/4 targeted canary rerun
17/20
2/2 targeted rerun
19/20
```

The final full run was:

```text
Agreement: 19/20
```

which matches the final `eval-run.txt`.

**Package analysis**

I analyzed `pkg-20`.

The final rubric verdict was `reject`, and the gold label was also `reject`.

Earlier, my rubric incorrectly accepted this package. The technical plan itself was plausible, but the package omitted an AI-use disclosure that the repository explicitly required for the contribution. My original conventions check was too general, so the evaluator could treat the missing disclosure as irrelevant.

I revised the rubric so repository contribution requirements were part of plan readiness. After that change, `pkg-20` was rejected because the draft comment omitted a contribution requirement that explicitly applied to it.

**Check rationale**

The final `Thread and conventions` check in my rubric is:

```text
| Thread and conventions | The draft plan comment read against the issue thread highlights and the repo's stated conventions, contribution policies, and repo-facts block. | Pass if the proposed plan and comment respect relevant maintainer requests, issue constraints, and repository conventions, including any required contribution or AI-use disclosures. Fail when the comment omits a requirement the repository explicitly says applies to that comment or contribution. | required |
```

I revised this check after `pkg-20` was incorrectly accepted. The earlier wording said to respect repository conventions but did not make an explicit required disclosure decisive. That left too much room for the grader to overlook a contribution-policy requirement.

I added the phrase:

```text
including any required contribution or AI-use disclosures
```

and the explicit failure condition:

```text
Fail when the comment omits a requirement the repository explicitly says applies to that comment or contribution.
```

I preferred this over making all missing information an automatic failure because only requirements that the repository explicitly says apply should block the plan.

**Trade-offs**

Strengthening `Thread and conventions` makes the grader stricter about repository-specific contribution requirements. A technically executable plan can now be rejected when its draft comment omits something the repository explicitly requires, such as an AI-use disclosure.

After making that change, I reran:

```text
--only pkg-20,pkg-04
```

and both packages matched their gold labels:

```text
2/2
```

`pkg-20` changed to the intended rejection, while `pkg-04`, an already-rejecting canary, remained a rejection. This gave me evidence that the change fixed the disclosure case without broadly changing unrelated package results.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.