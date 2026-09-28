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

CruzIsaiah

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53#issuecomment-5862143116

I'd like to work on reproducing this one as part of a course assignment. I'm a student contributor here, not a maintainer.
Concretely, I'll check the two behaviors the issue reports: that scrub() leaves (555) 123-4567 unredacted while redacting 555-123-4567 in the same string, and that detect() returns [] for the parenthesized format. I'll also run the four tests named above (test_us_phone_number_redaction, test_us_phone_formats, test_detect_phone_pii, test_phone_at_start_of_text) in tests/unit/test_pii_scrubber.py against current main.
I'll post a reproduction report with my environment, the exact commands I ran, and the output I observed. I'm not proposing a fix yet, just the reproduction.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53#issuecomment-5862221504

## Reproduction report

**Environment:** Windows 11 (10.0.26200), Git Bash; Python 3.12.10; fork of this repo at commit `f89c06f` (`main`, 2026-09-16), working tree clean (no local modifications).

**Setup deviation:** I did not run the documented `make setup` path in `docs/SETUP.md` (Docker, Postgres, Redis, `alembic upgrade head`, frontend install). `pyproject.toml` defines the `unit` marker as "Unit tests (fast, no external dependencies)" and `safety/pii_scrubber.py` is pure regex with no DB or API dependency, so I created a virtualenv, installed `pip install -e ".[dev]"`, and ran only this module's unit tests. Flagging that in case it matters to anyone re-running this.

**Steps:**

```
$ py -3 -m venv .venv
$ ./.venv/Scripts/python.exe -m pip install -e ".[dev]"
$ ./.venv/Scripts/python.exe -m pytest tests/unit/test_pii_scrubber.py -v -m unit
```

**Observed — the issue's snippet, run verbatim:**

```
$ ./.venv/Scripts/python.exe -c "
from safety.pii_scrubber import PIIScrubber
s = PIIScrubber()
print(repr(s.scrub('Call me at (555) 123-4567 or 555-123-4567')))
print(repr(s.detect('Call me at (555) 123-4567')))
"
'Call me at (555) 123-4567 or [REDACTED]'
2026-09-27 22:06:23 [info     ] pii_detected                   count=0 types=0
[]
```

Matches the issue exactly: in the same string the dashed number is redacted and the parenthesized one is not, and `detect()` returns `[]` for the parenthesized format.

**Control — dashed format alone, same build:**

```
$ ./.venv/Scripts/python.exe -c "
from safety.pii_scrubber import PIIScrubber
s = PIIScrubber()
print(repr(s.scrub('Call me at 555-123-4567')))
print(repr(s.detect('Call me at 555-123-4567')))
"
'Call me at [REDACTED]'
2026-09-27 22:06:23 [info     ] pii_detected                   count=1 types=1
[{'type': 'phone_us', 'value': '555-123-4567', 'start': 11, 'end': 23}]
```

The control redacts and detects normally, so phone redaction is working in general and the failure is specific to the parenthesized format.

**The four tests named in the issue:**

```
tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_us_phone_number_redaction XFAIL [ 12%]
tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_us_phone_formats XFAIL [ 16%]
tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_detect_phone_pii XFAIL [ 48%]
tests/unit/test_pii_scrubber.py::TestPIIScrubber::test_phone_at_start_of_text XFAIL [ 72%]
======================== 20 passed, 5 xfailed in 0.98s ========================
```

All four `xfail`, matching the report.

**Expected:** `scrub()` redacts `(555) 123-4567` the same way it redacts `555-123-4567`, and `detect()` reports it.

**Actual:** reproduced as described — the parenthesized format passes through `scrub()` unredacted and `detect()` finds nothing, while the dashed format is handled correctly, on current `main` in the environment above.

I have not diagnosed the cause in the pattern yet; this report covers the reproduction only.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

- First full run: `agreement: 18/20 scored items  (bar: 18/20: PASS)`, with `categories: clear-accept 6/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4`
- Targeted re-run on `pkg-09`, `pkg-10`, `pkg-02`, and `calib-03` after revising `behavior-match`: `agreement: 3/3 scored items` (all four packages matched gold; `calib-03` is unscored)
- Final full run: `agreement: 20/20 scored items  (bar: 18/20: PASS)`, with `categories: clear-accept 8/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4`

Two earlier single-package runs preceded the first full run: `pkg-20` alone graded `accept`
against a gold label of `reject` (`categories: disclosure 0/1`), which is what sent me back to
the `repo-rules` disclosure wording before the first full run.

**Package analysis**

`pkg-09` (`sharkdp/fd#2033`). On my first full run my rubric decided `reject` while the gold
label was `accept`; on my final run it decided `accept`, matching gold. The disagreement came
entirely from `behavior-match`, which reported:

> Log output 'ONE ONE ONE TWO TWO TWO' shows strictly in-order execution — the reported
> artifacts do not show the out-of-order flush behavior scenario 2 of the issue describes.

That reading was correct about the artifact and wrong about the package. `pkg-09` is an honest
cannot-reproduce: the contributor really ran the `fd --exec-batch` attempt, the reordering did
not occur, and they said so while naming what their setup may have lacked (uniform wrapper
string lengths against a 2 MiB `ARG_MAX`). My `honest-result` check passed it for exactly that
reason on the same run. The two required checks were reading the same package in opposite
directions: `behavior-match` demanded the issue's bug appear in the artifacts, which in a
genuine cannot-reproduce it cannot, so a package gold treats as a model result was held by a
required fail. `pkg-10` (`starship/starship#7648`) failed the same way on the same run.

**Check rationale**

The `behavior-match` check in `tools/repro-check/rubric.md` now reads:

> The artifacts support the report's claim about the issue's behavior. If the report claims the
> bug was reproduced, the artifacts must show the same bug or behavior the issue describes; a
> different error, an adjacent behavior, a partial run, or an unrelated failure does not pass.
> If the report concludes it could not reproduce, the artifacts must show that the stated
> attempt was actually run and that the reported bug did not occur, or that a different result
> occurred exactly as the conclusion states; a different observed result may pass in that case.

My first version read: "The artifacts show the same bug or behavior the issue describes. A
different error, an adjacent behavior, or a different failure mode does not pass." That
condition asked a single question — does the bug appear? — which is the right question only
when the report claims reproduction. I rejected the obvious loosening (allowing any "different
observed result" to pass) because that is precisely what a wrong-target package looks like: a
real failure that is not the issue's failure. The revision instead makes the report's own
conclusion the thing the artifacts are measured against, so what the check demands depends on
what the report claims. A claim of reproduction still has to show the issue's bug; a
cannot-reproduce has to show the attempt genuinely ran and describe its result accurately.

**Trade-offs**

The revision loosens the check, so before the confirming full run I re-ran targeted canaries
with `--only pkg-09,pkg-10,pkg-02,calib-03 --include-calibration` to test whether wrong-target
detection had leaked. It had not. Both canaries still failed `behavior-match` for the same
artifact-versus-issue mismatch as before: `pkg-02` for running `--line-range
18446744073709551614:` and getting a clap "Invalid value" error (exit 1) instead of the issue's
capacity-overflow panic (exit 101), and `calib-03` for an input using `:` instead of `=`,
producing an HCL "Missing key/value separator" parse error rather than the reported panic. All
four packages in that run showed "a different observed result"; the two claiming reproduction
failed and the two honestly reporting non-reproduction passed, which is the distinction the
revision was written to draw. The final full run confirmed no regression elsewhere:
`wrong-target` held at 4/4 and `clear-accept` rose from 6/8 to 8/8.

What the check still gives up: it now trusts the report's stated conclusion to decide which
standard applies. A report that hedges its conclusion rather than stating one plainly gives the
check less to measure against, and a cannot-reproduce whose artifacts are thin but not absent
sits closer to the line than it did under the stricter rule. I accepted that because
`honest-result` reads the same conclusion against the same artifacts independently, so a
conclusion that misrepresents its evidence is still caught by a second required check.

A separate revision earlier in the same session fixed `repo-rules`. On the `pkg-20` single run
the check passed the package with the evidence "no AI use is claimed, so the strict disclosure
rule has nothing to disclose", against a gold label of `reject`. The pass condition now states
that where a repo requires disclosure of all AI use and no disclosure appears, the check fails,
and the evidence guide's Comms section adds that "the absence of an explicit AI claim is not
evidence that no assistance occurred". `pkg-20` flipped to `reject` and `pkg-07`, the mirror
case where the comment does disclose under a policy requiring it, stayed `accept`. The
`disclosure` category has read 1/1 on every run since.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
