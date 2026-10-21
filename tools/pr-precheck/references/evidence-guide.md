# Evidence guide: where evidence lives in a PR package

This guide is the map for `rubric.md`'s checks. For each evidence family
it says where the evidence lives in an eval or practice package (a
bundle such as `eval/packages/calib-01.md`), where it lives in the
live PR workflow, and what good looks like. `procedure.md` says when
each family is gathered; this file says where.

The four families are the harness's failure categories. A package that
fails none of them is a clear accept.

| Family | Harness category | Rubric checks it feeds |
|---|---|---|
| Plan fidelity | silent-drift | Plan fidelity, Description matches diff |
| Test evidence | not-tested | Test evidence, Repo checks run |
| Diff quality | unreviewable | Diff focus, Commit hygiene (preferred) |
| Standards and comms | standards-wall | Template completeness, Contribution policy, AI-use disclosure |

In eval mode the bundle is the whole world: every location below is a
section of the bundle, and if a section is missing, that absence is the
evidence. In live mode the locations are the files named by the
command, the branch's git output, and the scoped repo on GitHub.

## Plan fidelity (harness category: silent-drift)

**Where it lives in a practice package.**

- The plan: `## Plan context`. It holds the repro evidence the plan
  built on, the plan's steps, its boundary ("Not in scope: ..."), its
  `Files:` list, and its `Test plan:`. Any Deviations appear in this
  section; if the section records none, the plan stands as written.
  In calib-01: two steps, "Not in scope: any other theme", "Files:
  `themes.gitconfig`", no Deviations.
- What actually changed: `## Candidate PR` > `### Diff` (files and
  hunks) and `### Commits`.
- The PR's claims about the change: `### Title` and `### Description`.

**Where it lives in the live PR workflow.**

- The plan: `plan.md`, including its `## Deviations` section (each
  deviation with its reason).
- What actually changed: `git diff main...HEAD` (three dots) and the
  branch's commits from `git log main..HEAD`, run from the working
  copy.
- The PR's claims: `pr_draft.md` (draft title and description).

**What good looks like.**

- Every hunk in the diff falls inside the plan's scope, approach, and
  `Files:` list, or inside a recorded Deviation that says what changed
  and why.
- Every step the plan committed to is visible in the diff, or a
  Deviation or the description says it was dropped and why.
- Every change the description claims is a hunk in the diff, every
  material hunk is mentioned in the description, and any fidelity claim
  ("implements the plan", "rendering is unchanged") is true of the diff.
- calib-01 is a good example: the plan says remove the first,
  shadowed `file-decoration-style` line in `themes.gitconfig`; the diff
  removes exactly that one line (`- file-decoration-style = "#434C5E"
  ul`) in that one file; the description claims exactly that.

**Silent drift looks like:** a hunk in a file the plan never names, or
in a theme the plan puts out of scope, with no Deviation; a planned
step missing from the diff with no note; a description that claims a
change the diff does not make, or omits one it does.

## Test evidence (harness category: not-tested)

**Where it lives in a practice package.**

- The plan's test plan: `## Plan context` > `Test plan:`, read with the
  repro evidence in the same section (the before-state the test must
  flip). In calib-01: re-run the `configparser` repro and expect a
  clean parse; a `delta --show-syntax-themes` smoke check.
- The proof: `## Candidate PR` > `### Test evidence` (commands, output,
  before/after).
- The PR's testing claims: `### Description`.
- The repo's own checks: `## Repo facts` (stated test, lint, or build
  commands, and contribution policy). If Repo facts names none, the
  repository states no required checks. calib-01's Repo facts names
  none.

**Where it lives in the live PR workflow.**

- The plan's test plan: `plan.md` (its test plan, plus any
  `## Deviations` that change it).
- The proof: `test_evidence.md` (captured commands and output), plus
  any output quoted in `pr_draft.md`.
- The PR's testing claims: `pr_draft.md`.
- The repo's own checks: `docs/CONTRIBUTING.md` and the repository PR
  template (stated test, lint, or build commands).

**What good looks like.**

- The primary bug-fix evidence, the plan's own reproduction re-run on
  the branch's code, has shown output with an observable result that
  distinguishes the fix from the reproduced bug: the same scenario, its
  before-state, and its after-state.
- Supporting items (test suite, lint, typecheck, smoke check, negative
  control) name the command or check and state a specific result
  ("`go test ./...` passes (4108 tests)", "fmt and clippy clean",
  "control unchanged") that nothing else in the package contradicts.
  They support the primary evidence; they never replace it.
- Every "tested" or "verified" claim in the description is backed by
  shown output or a named command with a specific result.
- Each repo-required check is named (by command or template checklist
  item) with its result on the branch; a failure is reported and
  honestly explained as unrelated.
- A test-plan item that was not run is disclosed as not run, with why.
- calib-01 is a good example: the primary repro, the same strict
  `configparser` command, is shown with its before
  (`DuplicateOptionError ... already exists`) and after (`parsed OK`),
  and `git config --get-all` now prints exactly one value. Its
  supporting smoke check names the command (`delta
  --show-syntax-themes`) and states a specific result ("renders
  gruvmax-fang unchanged").

**Not tested looks like:** primary evidence that is only an assertion
("colors work now", "verified working on my machine") with no
observable output; output for a different scenario than the plan's
repro (a one-file case when the bug needs two files); "tests pass" or
"all tests pass" with no command and no specific result; output that
cannot be tied to this branch; a test that would pass before the fix
too; a repo-required check that is never mentioned.

## Diff quality (harness category: unreviewable)

**Where it lives in a practice package.**

- The change: `## Candidate PR` > `### Diff` (every file and hunk).
- The history: `## Candidate PR` > `### Commits` (hash and message per
  commit).

**Where it lives in the live PR workflow.**

- The change: `git diff main...HEAD`.
- The history: the branch's commits, `git log main..HEAD` (use
  `git show <hash>` to see what one commit contains).

**What good looks like.**

- Every hunk serves the described change, so a reviewer sees the fix
  without separating it from noise.
- Each commit message describes the change it contains; no "wip",
  "oops", or reverted experiments.
- calib-01 is a good example: one hunk removing one line, inside one
  commit whose message (`themes: remove shadowed file-decoration-style
  from gruvmax-fang`) describes exactly that change.

**Unreviewable looks like (the debris tells):** debug prints or
logging left in; commented-out blocks; dead code; stray or generated
files; whitespace, formatting, or lockfile churn in untouched lines;
drive-by edits unrelated to the issue.

## Standards and comms (harness category: standards-wall)

**Where it lives in a practice package.**

- The repo's asks: `## Repo facts`, specifically the `pull requests:`
  line (PR template, or that there is none, and any contribution asks)
  and the `contribution policy (CONTRIBUTING.md):` line (stated
  policy, including any AI-use disclosure rule). In calib-01: "no PR
  template; the contribution docs ask that PRs stay small and
  reference the issue" and "no stated AI policy".
- Maintainer direction: `## Issue` and `## Thread highlights`. In
  calib-01 the thread has no comments.
- Where the PR honors the asks: `### Title`, `### Description`,
  `### Commits`, and the size of `### Diff`. A branch name appears only
  if the bundle states one; calib-01 does not, and its Repo facts state
  no branch-naming rule.

**Where it lives in the live PR workflow.**

- The repo's asks: the repository PR template (for example
  `.github/pull_request_template.md`), `docs/CONTRIBUTING.md`
  (branch-naming rule, target branch, issue-link format, commit and PR
  conventions, any AI-use disclosure rule), and the house rules in
  `scope.md`.
- The course's AI-use disclosure requirement: every live PR discloses,
  in the student's own words, how AI was used on the change, in the
  description's "Notes for Reviewers" section. This applies even when
  the repository states no AI policy.
- Maintainer direction: the issue thread.
- Where the PR honors the asks: `pr_draft.md` (sections, issue link,
  the AI-use disclosure under "Notes for Reviewers"), the branch name (`git branch --show-current`), and the
  branch's commits.

**What good looks like.**

- Every section the PR template asks for is present with content
  specific to this PR (or says why it does not apply); no placeholder
  text left.
- Every contribution requirement the repo states is met as stated:
  branch name matches the stated naming rule, target branch is the one
  stated, the issue is linked in the stated form, one PR per issue.
- Live mode: "Notes for Reviewers" contains an AI-use disclosure that
  says, in the student's own words, how AI was used on this change (not
  boilerplate), and it meets any further repository disclosure rule.
  Eval mode: if the bundle states a disclosure requirement, the PR's
  disclosure meets it.
- Explicit maintainer direction in the thread is followed.
- Where the repo states no requirement (no template, no branch rule, or
  in eval mode no AI policy), there is nothing to meet; the evidence
  line names the source that was silent. Repository silence about AI
  never removes the live-mode course disclosure requirement.
- calib-01 is a good example: no template and no AI policy are stated,
  and the two stated asks are met: the PR is small (one line in one
  file) and the description references the issue (`(#2211)`).

**Standards wall looks like:** template sections missing or left as
placeholder text; a required disclosure absent (in live mode, no
AI-use disclosure under "Notes for Reviewers"); a branch name, issue
link, or commit format that breaks a stated rule; a maintainer request
in the thread ignored. (Whether the description's claims match the diff
is plan fidelity, above, not standards.)
