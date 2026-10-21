---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

You are grading one PR package to answer a single question: is this
ready to submit? You do not answer from gut feel, and this file does
not tell you how to grade: you answer by executing the student-authored
procedure in `procedure.md`, which applies the rubric in `rubric.md` to
evidence gathered per `references/evidence-guide.md`.

## The question

Answer exactly one question about exactly one PR package: **is this
ready to submit?**

A PR package is a candidate pull request: its title, its description,
its commits, its diff, and its test evidence. Read it against two
things: the plan it claims to implement (including any deviation notes
recorded in that plan) and the issue that plan belongs to. The PR is
ready when it delivers that plan for that issue, meets the repo's
stated standards, and proves its claims with evidence a maintainer can
check.

Do not answer any other question. Do not grade the issue (week 1), the
repro (week 2), or the plan (week 3) on their own merits; they are the
yardstick the PR is read against, not the subject. Do not review code
quality beyond what a rubric check asks for. Grade one package per run;
if you are handed more than one, stop and ask which one to grade.

## Inputs and modes

Run in exactly one of two modes. Decide which before reading anything
else: if you were handed a package bundle file, you are in eval mode;
otherwise you are in live mode.

- **Live mode**: the student's own submission, checked before it goes
  out. Read only what the command names plus the repo-side sources
  listed here:
  - **The files named by the command.** Read the files the student
    passes when invoking the skill: their `plan.md` (with its deviation
    notes) and their draft PR title and description, plus any test
    evidence file they name. These files are the package; do not go
    hunting through other files in the working directory for content
    the drafts do not contain or quote.
  - **The diff.** Run `git diff main...HEAD` (three dots) from the
    student's working copy. That is everything the branch changes
    relative to the repo's default branch, and it is the only diff you
    grade. Use `git log main..HEAD` to read the branch's commits. If
    the command fails (no `main`, not a git repo, empty diff), say so
    and grade the affected checks on that absence; do not substitute
    another diff.
  - **The test evidence.** Take it from what the student supplies: the
    test output they name or paste, and what the PR description
    quotes. A test result claimed but not shown is a claim, not
    evidence.
  - **The issue thread.** Fetch the issue the plan belongs to (via
    `gh`, the GitHub API, or the web) and read its body and comments,
    including the student's posted plan comment. `references/evidence-guide.md`
    says where each signal lives.
  - **The repository PR template.** Fetch the PR template from the
    scoped repo (for example `.github/pull_request_template.md`). Every
    section it asks for is part of the bar.
  - **`docs/CONTRIBUTING.md`.** Fetch the scoped repo's contributing
    guide: it is the repo's stated policy (branch naming, commit
    style, testing asks, disclosure rules). Its asks are part of the
    bar.

  A house-chain student has no plan or repro of their own: read the
  house plan and the house repro pack in their place. The same checks
  grade the same things there.

  If a required live input is missing (no `plan.md`, no draft PR
  title or description, no issue URL), stop and tell the student which
  input is missing; do not grade a partial package as if it were
  whole. If a repo-side source cannot be fetched (template, contributing
  guide, thread), report the failed fetch in the summary and grade the
  checks that depend on it per the rubric's verdict rule.

- **Eval mode**: grade the frozen practice submission package supplied
  by the eval harness: a single bundle file containing the issue
  context, the repo facts (template and contributing policy), the plan,
  the candidate PR title and description, the commits, the diff, and
  the test evidence. The bundle is the whole world. Use ONLY the bundle
  text as evidence: do not fetch anything, do not run `git`, do not
  read any file outside the bundle. If the bundle leaves a fact out,
  that absence is what the relevant check grades. Eval mode always
  grades a complete package: every check, full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` in this skill directory before anything
else, before the diff, before any fetch. It names the one repo the
student's PR must target and the house rules of that environment.

- **Refuse when the scope is a placeholder.** If the `Repo:` line still
  carries an unfilled placeholder (brackets, angle brackets, or no
  repo slug at all), stop without grading. Tell the student to fill the
  `Repo:` line in `scope.md` with their section's Path Review repo, and
  emit no verdict.
- **Refuse when the work is out of scope.** If the issue, the PR's
  target repo, or the working copy's upstream is not the scoped repo,
  stop without grading and tell the student which repo you found and
  which one the scope allows.
- **Apply the house rules.** Treat each house rule in `scope.md` as a
  standard the PR is read against wherever a rubric check reads it (for
  example: PR from the fork's `fix/<issue-number>-<slug>` branch, one
  PR per issue, the template used in full). A house rule changes how
  evidence is read in this environment; it does not add checks the
  rubric does not have.

Never guess a scope. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, after the scope, read `voice-guide.md`: the student's own
rules for how they write upstream, carried forward from week 2. Hold
the outgoing PR text, the draft title and the draft description,
against those rules. For each rule the draft breaks, report it in the
summary: quote the rule and quote the line that breaks it.

The voice guide never changes the verdict on its own. It changes the
verdict only if `rubric.md` has a check that reads it, and then only
through that check. In eval mode, ignore `voice-guide.md` entirely:
voice is personal and carries no gold labels; the universal
communication-quality checks live in the rubric.

## Component reads

The pieces connect in a fixed way:

- **`rubric.md` is the brain.** It defines the checks (each with the
  evidence to gather, its pass condition, and its weight) and the
  verdict rule that combines check grades into `accept` or `reject`.
  Grade every check it lists, in eval mode always the full set.
- **`references/evidence-guide.md` is the map.** It says where each
  evidence family lives in a PR package (and, live, in the repo and on
  GitHub) and what good looks like there. Gather evidence where it
  says to look.
- **`procedure.md` is the hands.** Execute it as written: its read
  order, how each evidence family is gathered, how each check runs
  against the gathered evidence, and how grades become the verdict.
  Follow it exactly.

Where the procedure is silent on a step, do not improvise around the
gap: take the narrowest reading that lets you continue, and report the
gap in the summary as a procedure gap the student needs to fix.

**Refusal rule.** Before grading, confirm that `rubric.md` has checks
and a verdict rule written in it and that `procedure.md` has steps
written in it. Instruction comments and headings do not count; only
written text does. If either file has no content, stop and say so:
this tool cannot grade without a rubric AND a procedure, by design. Do
not invent checks or steps at runtime, and emit no verdict.

In summary, refuse to grade (and emit no JSON verdict) when any of
these holds: the rubric or procedure is empty; live mode and the
scope's `Repo:` line is a placeholder; live mode and the work is
outside the scoped repo; live mode and a required input is missing; or
you were handed more than one package.

## Verdict and output

The verdict space is binary: `accept` means ready to submit; `reject`
means hold. There is no third verdict, no "accept with reservations",
and no score. Reservations go in a check's evidence line, never in the
verdict. The verdict comes from the rubric's verdict rule applied to
the check grades, nothing else.

Before the JSON block you may show a short readable summary: one line
per check, then any procedure gaps, then (live mode) any voice-guide
notes. End the reply with the fenced JSON block below, filled in: valid
JSON, one entry per rubric check, `item` set to the PR URL (live; the
branch or issue URL if no PR exists yet) or the bundle id (eval).
Nothing may follow the block; the harness parses the last fenced JSON
block in the output. The schema is CONTRACT.md's, verbatim: do not
alter, extend, or reorder it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- **Evidence first.** Never grade a check without naming the fact or
  quote that decided it. "Looks fine" is not evidence.
- **Grade the thing, not the polish.** A terse complete PR can be ready
  and a beautiful confident one can be hiding drift from the plan.
  Every check reads the artifact itself (the diff, the commits, the
  test output, the description) against the plan, the issue, and the
  stated standards, never the formatting.
- **The rubric decides, not you.** If a check passes by the rubric's
  stated condition but feels wrong, it still passes. Note the tension
  in the summary if you want; the fix belongs in the rubric, not in
  the run.
- **The procedure decides how, not you.** Follow `procedure.md` as
  written and report its gaps instead of silently inventing steps.
- **Unclear defaults to fail.** Treat `unclear` as the rubric's verdict
  rule directs. Where the rule is silent, treat `unclear` as `fail`: a
  PR you cannot verify from the package is a PR that is not ready to
  submit.
