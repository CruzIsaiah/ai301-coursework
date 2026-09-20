# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53

**Verdict output**

Accepted, in fit order

1. #53 — PII scrubber fails to redact parenthesized US phone numbers. Best fit: it ships a copy-pasteable Python reproduction with observed-vs-expected output and names the four failing tests (test_us_phone_number_redaction, test_us_phone_formats, test_detect_phone_pii, test_phone_at_start_of_text), which is exactly the "reproduce locally and verify with tests" profile. Single-regex surface area, and the timeline shows no one has touched it at all.
2. #72 — verify_password raises UnknownHashError on malformed hashes. Smallest estimate (1–2 hours), two named files, and an unambiguous target behavior (fail closed, return False). API-area work matches the profile; slightly behind #53 only because it carries no reproduction snippet.
3. #68 — Keyword search ZeroDivisionError when the index is empty. Still well-bounded, but the largest estimate (2–4 hours) and the fix sits against third-party rank-bm25 behavior rather than purely local code.

Per-check notes. The only wrinkle was claim evidence on #68 and #72: each has a referenced timeline event from a classmate's fork commit (yulijasso 2026-09-16 on #68, newairforces 2026-09-19 on #72). Neither is an assignee, an open PR, or even a claim comment — and the Path Review house rule in scope.md says classmate claims don't block an issue regardless. Both pass.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53",
    "checks": [
      {
        "name": "Maintainer activity",
        "grade": "pass",
        "evidence": "Human commit f89c06f by Aburke225 on main 2026-09-16 (4 days ago), plus COLLABORATOR comments by Aburke225 on 2026-09-16."
      },
      {
        "name": "Repository is active",
        "grade": "pass",
        "evidence": "archived=false; no releases exist, but human-authored main commit 2026-09-16 is within 90 days."
      },
      {
        "name": "Issue is appropriately scoped for a newcomer",
        "grade": "pass",
        "evidence": "Settled specific change: phone pattern 'matches dashed formats like 555-123-4567 but not the parenthesized format (555) 123-4567', with a runnable repro and four named failing tests."
      },
      {
        "name": "Issue is not already actively claimed",
        "grade": "pass",
        "evidence": "assignees: none; repo has zero PRs; 0 comments and no referenced/cross-referenced events on the timeline."
      },
      {
        "name": "AI-assisted contributions are permitted",
        "grade": "pass",
        "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md contain no AI-use prohibition; repo is silent on AI."
      },
      {
        "name": "Newcomer-fit signals",
        "grade": "pass",
        "evidence": "Labeled 'good first issue' and 'tier-1'; issue opened by COLLABORATOR Aburke225 with explicit reproduction steps and named covering tests."
      }
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72",
    "checks": [
      {
        "name": "Maintainer activity",
        "grade": "pass",
        "evidence": "Human commit f89c06f by Aburke225 on main 2026-09-16 (4 days ago), plus COLLABORATOR comments by Aburke225 on 2026-09-16."
      },
      {
        "name": "Repository is active",
        "grade": "pass",
        "evidence": "archived=false; no releases exist, but human-authored main commit 2026-09-16 is within 90 days."
      },
      {
        "name": "Issue is appropriately scoped for a newcomer",
        "grade": "pass",
        "evidence": "Settled specific change: 'Verification against a malformed hash should fail closed (return False), not raise'; files core/security.py and tests/unit/test_security.py; est. 1-2 hours."
      },
      {
        "name": "Issue is not already actively claimed",
        "grade": "pass",
        "evidence": "assignees: none; repo has zero PRs; only a 'referenced' event from newairforces' own fork commit 2026-09-19, which the scope.md Path Review house rule says does not block."
      },
      {
        "name": "AI-assisted contributions are permitted",
        "grade": "pass",
        "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md contain no AI-use prohibition; repo is silent on AI."
      },
      {
        "name": "Newcomer-fit signals",
        "grade": "pass",
        "evidence": "Labeled 'good first issue' and 'tier-1'; COLLABORATOR-authored with named files, effort estimate, and an explicit acceptance step (remove the H-05 xfail marker)."
      }
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68",
    "checks": [
      {
        "name": "Maintainer activity",
        "grade": "pass",
        "evidence": "Human commit f89c06f by Aburke225 on main 2026-09-16 (4 days ago), plus COLLABORATOR comments by Aburke225 on 2026-09-16."
      },
      {
        "name": "Repository is active",
        "grade": "pass",
        "evidence": "archived=false; no releases exist, but human-authored main commit 2026-09-16 is within 90 days."
      },
      {
        "name": "Issue is appropriately scoped for a newcomer",
        "grade": "pass",
        "evidence": "Settled specific change: \"index() shouldn't raise on an empty corpus either\"; files rag/retriever/keyword_search.py and tests/unit/test_keyword_search.py; est. 2-4 hours."
      },
      {
        "name": "Issue is not already actively claimed",
        "grade": "pass",
        "evidence": "assignees: none; repo has zero PRs; only a 'referenced' event from yulijasso's own fork commit 2026-09-16, which the scope.md Path Review house rule says does not block."
      },
      {
        "name": "AI-assisted contributions are permitted",
        "grade": "pass",
        "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md contain no AI-use prohibition; repo is silent on AI."
      },
      {
        "name": "Newcomer-fit signals",
        "grade": "pass",
        "evidence": "Labeled 'good first issue' and 'tier-1'; COLLABORATOR-authored with named files, effort estimate, and an explicit acceptance step (remove the H-01 xfail marker)."
      }
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

**Run history**

- First full run: `agreement: 16/20 scored items  (bar: 18/20: below the bar)`
- First partial re-run on issue-01, issue-15, issue-19, and issue-20: `agreement: 0/4 scored items`
- Second partial re-run after the updated scope check was actually saved: `agreement: 2/4 scored items`
- Final full run: `agreement: 19/20 scored items  (bar: 18/20: PASS)`

**Issue analysis**

`issue-19  accept  reject   NO     failed: Issue is appropriately scoped for a newcomer, Newcomer-fit signals (preferred)`

My rubric decided `reject`, while the gold label was `accept`. The required scope check caused the rejection. The issue described a performance problem with multiple possible causes and implementation ideas. My rubric treated parts of the requested behavior as not settled enough for a newcomer. The gold label treated the maintainer's identification of the likely causes as useful scoping rather than evidence that the issue was too open-ended.

**Check rationale**

Current check:

> `PASS if the issue names a settled, specific change and none of these hold: (a) it is an umbrella or tracking issue whose sub-items are meant to be split into separate work; multiple sub-steps serving one deliverable are not an umbrella; (b) it is a pure usage or support question; (c) a maintainer warns that the fix requires reworking core internals; a maintainer diagnosing the cause or naming files/components is scoping help and does not fail by itself; (d) the specific change is left for the contributor to choose rather than stated; (e) the required behavior is still unsettled, such as an unanswered design question in the body/thread or repeated closed-unmerged attempts with no maintainer resolution; (f) it depends on an unresolved product decision or missing required artifact. A terse description or missing reproduction steps does not fail by itself, especially when the opener is a maintainer or the issue carries a good-first-issue label.`

I changed this check because my first version used "one reasonably bounded deliverable," which was too broad. It could reject an issue just because the work touched multiple files or had multiple steps. The current version focuses more on whether the requested behavior is settled and whether the contributor can implement it without first making a design or product decision.

**Trade-offs**

The stricter settled-scope rule can still reject an issue that is technically workable when the description contains multiple possible causes or implementation choices. `issue-19` is the example from my final run: the gold label was `accept`, but my scope check still produced `reject`. I accepted that trade-off because the rule helps avoid issues where a newcomer would need to make an unresolved design or product decision before starting.

---

## Selection rationale

**Selection rationale**

1. Issue #53 fits my interests because it is a focused Python bug with a clear reproduction case and named failing tests. The scope is small enough to fit the time available.

2. The verdict correctly identified that the issue is active, unclaimed, well-scoped, and easy to verify with tests. I also preferred it because the expected behavior is very clear and the fix appears more contained than the authentication and retrieval issues I also evaluated.

3. I expect claiming it to be straightforward because it is open and has no assignee or pull request. Other students may also select it, but the Path Review house rules allow shared issues.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
