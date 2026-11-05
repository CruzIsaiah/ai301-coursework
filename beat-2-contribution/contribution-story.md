# Contribution: Implement Jest Tests for Lorem Ipsum Generator

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Isaiah Cruz
**GitHub Username:** CruzIsaiah
**Issue:** https://github.com/Bashamega/WebDevTools/issues/386
**Pull Request:** not opened yet (as of 2026-11-05)

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built and tuned an issue-scout skill to find first issues on GitHub**

I built an `issue-scout` skill that searches GitHub for recent Python
issues labeled `good first issue`. My first scan was too broad and
included assigned issues and candidates that were not very useful for
a first contribution. I tightened the ranking to drop assigned
issues, keep only issues updated in the last 60 days, put bug and
testing labels first, prefer fewer comments and more recent updates,
and allow at most two issues per repository. The final scan on
October 31 graded 5 issues against my rubric, and all 5 were accepted.

**Unit 6: Installed the voice guard, patched the scout's scope check, and claimed a real issue**

On October 31 I installed the voice guard at `~/.claude/voice-guard/`, with one voice guide
shared by repro-check, plan-check, and pr-precheck. The wiring test was stopped as expected
(`guard-log.md`: "stop: no body the guard can read | target: gh issue comment --help"). The
same day I replaced the scout's scoping check with `scope-feasible`. On November 5 I made a
mistake: I posted my claim on #386 from the browser without first running
`check_voice.py --draft`. When I ran it afterward, it stopped the claim on my own rule "Check
the thread, then name my first step and when I'll report back", because the claim gives no
report-back date. repro-check flagged the same gap. What I learned is to run the voice guard
before any GitHub comment I post, and to give a realistic report-back time in every claim I
make from now on. I have cloned my fork to `C:\Users\howdi\WebDevTools` and created
`CLAUDE.local.md` there from the Unit 6 template. It is excluded through `.git/info/exclude`,
and `git status` in WebDevTools is clean.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

My first picks did not last. On October 31 I re-graded my three Unit 5 picks with the patched
rubric, and all three were rejected: each had been closed as completed by a merged PR between
October 29 and 31. The same day I ran a fresh scan (Python, `good first issue`, open). It
graded five issues and accepted all five, but every one had been opened that day in a repo
where issues get fixed within a day, so I marked them perishable. I then found
Bashamega/WebDevTools#386 while looking through the CodePath issue-selection candidates after
my earlier choices became unavailable, and gave it to the scout directly on
November 5. The verdict was **accept**, with all five required checks passing. The owner
committed to main 54 days earlier and the latest release (2.3) is from September 12. The issue
asks for one piece of work: tests for one component. Nobody is assigned and no PR is open. The
repo says nothing about AI use. The preferred newcomer-fit check also passed: the owner opened
the issue and labeled it `good first issue` and `testing`. The scout rated it straightforward.
It fits my profile because it is automated testing with JavaScript and React on a
developer-tools site, with a clear way to check the result (`npm test`). It is frontend
testing, not the Python backend work I prefer. I hope to learn how to test React components
with React Testing Library, including mocking `localStorage` and `navigator.clipboard`.
I chose it over the five Python candidates from the October 31 scan for four reasons:
- It had a cleaner availability history: nobody else had claimed it and no PR had been
  tried, while the Python picks were in repos that fix new issues within a day.
- The scope is clear: tests for one component.
- The maintainer is active.
- It is a straightforward testing contribution that I can verify locally with `npm test`.

Claim comment (posted 2026-11-05):
https://github.com/Bashamega/WebDevTools/issues/386#issuecomment-6661084607

The scout held up on its checks, but it fell short in three ways. First, my search queries
only look for Python, so they could never have found this JavaScript issue; I had to bring it
in myself. Second, the claim check has no rule for a claim comment I wrote. I graded my own
claim a pass because `scope.md` only blocks claims by someone else, and I logged a patch:
"a claim authored by the grader never fails this check". Third, a grade in direct mode was not
saved to `scan-output.md` automatically. repro-check noticed the missing record, and I added
it by hand.

**Toolkit**

- Tool: issue-scout in live mode. I used fresh scans on October 31, then gave it #386 as a
  direct URL on November 5 and graded it against my patched rubric.
- What it produced: an **accept** for #386 with evidence for every check (owner commit on
  2026-09-12, release 2.3, no assignee or open PR, no AI policy, `good first issue` +
  `testing` labels) and a "straightforward" difficulty note. The grade is saved in
  `issue-scout/scan-output.md` under 2026-11-05.
- Difficulties: (1) my search strategy is Python-only and missed this JS issue; (2) the claim
  check has no rule for my own claim; (3) the Unit 5 picks went stale within days, so a past
  accept says nothing about today; (4) direct-mode grades were not saved to `scan-output.md`
  automatically.
- What changed: I added the #386 grade to `scan-output.md` by hand. I logged the own-claim
  patch as rubric friction. I would add a JavaScript/TypeScript `testing` query to
  `search-strategy.md` and re-grade any pick on the day I claim it.

---

## Understanding the Issue

**Problem Description**

Nothing in the Lorem Ipsum Generator is broken. What is missing is tests. The page has no Jest
tests, so a change could break generating, copying, or the theme toggle and CI would not catch
it. The issue asks for unit tests for rendering, user interactions, and props/state, and
integration tests where they make sense. It also asks that the tests pass locally and in CI,
and that the docs explain how to run them.

**Expected Behavior**

A test file under `__tests__/customizer/LoremIpsumGenerator/` should cover what the page does,
and `npm test` plus the `jest_tests.yml` CI job should pass with it included. Here is what the
page does today, read from `page.jsx` on `main`:

- It renders the "Lorem Ipsum Generator" heading, a "Number of paragraphs:" number input
  (default 1, `min={1}` `max={10}`), and Generate and Copy buttons.
- Clicking Generate shows the fixed Lorem paragraph once for each number in the input.
- Clicking Copy calls `navigator.clipboard.writeText` with the generated text, then replaces
  the shown text with "Text copied successfully".
- The theme toggle (passed to `NavBar`) flips dark mode and writes `localStorage["theme"]`. On
  mount, the page reads the stored theme and applies it.

**Current Behavior**

`__tests__/` has tests for the README generator, gh-finder, and the sitemap generator, but
nothing for the Lorem Ipsum Generator. The page has no automated checks. While reading the
source I noticed three things that tests will touch. I am recording them here, not treating
them as bugs:

- The component is named `ButtonCustomizer`.
- `min`/`max` limit only the input's spinner, not `generate()`.
- The input value is stored as a string.

I have not cloned the repo or run anything yet.

**Affected Components**

- `src/app/customizer/LoremIpsumGenerator/page.jsx`: the component under test.
- `src/components/navbar`: renders the theme toggle the page passes down.
- New: `__tests__/customizer/LoremIpsumGenerator/page.test.jsx`, following
  `__tests__/customizer/Readme-generator/page.test.jsx`.
- `jest.config.js` and `jest.setup.js`: the existing Jest + jsdom setup.
- `contributing.md`: PR #692 (2026-11-05) already added a "Run the Tests" section, so the
  issue's "update the documentation" task may already be done. I need to confirm this before
  editing docs.

**Toolkit**

- Tool: Claude Code with the `gh` CLI. It read `page.jsx`, the `__tests__/` tree,
  `contributing.md`, the PR template, `package.json`, the Husky hook, and the CI workflows
  from GitHub, without cloning.
- What it produced: the list of behaviors above, the lack of any Lorem Ipsum test, the
  Readme-generator test as a pattern to follow, and the repo's test commands (including the
  PowerShell form, `$env:NODE_OPTIONS = "--experimental-vm-modules"; npx jest`).
- Difficulties: the issue body is a generic template ("Any known issues ... can be added
  here"), so the actual behaviors had to come from the source, not the issue.
- What changed: I will base the test cases on the source and confirm them against the running
  app after cloning.

---

## Reproduction Process

**Environment Setup**

- OS and shell: Windows 11 Home (10.0.26200), Windows PowerShell 5.1.
- Versions: Node v24.14.1, npm 11.11.0, git 2.55.0, Jest 30 with jsdom (from
  `jest.config.js`).
- Project: I forked `Bashamega/WebDevTools` to `CruzIsaiah/WebDevTools` and cloned it to
  `C:\Users\howdi\WebDevTools`, outside the course repo. I added `upstream` as a remote and
  created `feature/lorem-ipsum-jest-tests` from `main` at `ce28cbe`, following
  `contributing.md`. I ran `npm install`: 1138 packages added, exit 0, no tracked files
  changed, with 35 audit warnings that I left alone.
- Repo memory: I copied the Unit 6 template to `CLAUDE.local.md` and filled it in. I added it
  to `.git/info/exclude`, and `git status` stays clean, so it cannot end up in the PR.
- Challenge: plain `npm test` fails in PowerShell with `'NODE_OPTIONS' is not recognized as an
  internal or external command`, because the npm script uses Unix shell syntax.
- How I solved it: `contributing.md` already covers this case, and I used its PowerShell form:
  `$env:NODE_OPTIONS = "--experimental-vm-modules"; npx jest`.

**Steps to Reproduce**

#386 is a missing-tests issue, not a bug, so "reproducing" it means confirming two things on
the unmodified code: the existing suite passes, and no Lorem Ipsum Generator test exists.

1. `git clone https://github.com/Bashamega/WebDevTools.git`, `cd WebDevTools`,
   `git checkout ce28cbe`
2. `npm install`
3. In PowerShell: `$env:NODE_OPTIONS = "--experimental-vm-modules"; npx jest --ci`
4. `npx jest --ci LoremIpsum` (same shell)
5. `git ls-files | Select-String lorem; git grep -il lorem -- "*.test.*" "*.spec.*"` (same
   shell)
6. Observed result:
   - Step 3: all 9 suites (36 tests) pass.
   - Step 4: no tests found.
   - Step 5: the only "lorem" path is the component itself, and no test or spec file mentions
     "lorem".

**Reproduction Evidence**

- **Commit showing reproduction:** none. This is a baseline on the unmodified upstream commit
  [`ce28cbe`](https://github.com/Bashamega/WebDevTools/commit/ce28cbee88465844869da4603d69e55063bd22aa).
  My feature branch has no commits of its own and has not been pushed.
- **Screenshots/logs:** from `beat-2-contribution/repro-report.md`.

  Step 3:
  ```text
  Test Suites: 9 passed, 9 total
  Tests:       36 passed, 36 total
  Snapshots:   0 total
  Time:        3.983 s
  Ran all test suites.
  ```

  Step 4:
  ```text
  No tests found, exiting with code 1
    139 files checked.
    testMatch: **/__tests__/**/*.?([mc])[jt]s?(x), **/?(*.)+(spec|test).?([mc])[jt]s?(x) - 9 matches
  Pattern: LoremIpsum - 0 matches
  ```

  Step 5:
  ```text
  src/app/customizer/LoremIpsumGenerator/page.jsx
  ```
  `git grep` printed nothing and exited with code 1 (no match).
- **My findings:**
  - The gap in #386 is real on `ce28cbe`. Jest finds 9 test files, some under `src/` as well as
    `__tests__/`, and none covers `LoremIpsumGenerator/page.jsx`.
  - Because the existing suite passes on Windows, any later failure will come from my new tests,
    not from the baseline.
  - `repro-report.md` is Unit 6 coursework: my reproduction evidence for this story. I am
    keeping it local on purpose and not posting it upstream.

**Toolkit**

- Tool:
  - Claude Code ran the setup and baseline commands in PowerShell and drafted
    `repro-report.md`.
  - I graded the full package (claim plus report) with repro-check in live mode, twice.
- What it produced:
  - Run 1: **reject**. Four checks passed and **steps** failed. Step 5 used
    `git ls-files | grep -i lorem` right after "(same shell)", which is Windows PowerShell 5.1,
    where `grep` does not exist. The claim "no test file mentions lorem" had no step that
    produced it.
  - Run 2: **accept**. All five required checks passed (behavior-match, steps, environment,
    honest-result, repo-rules).
- Difficulties: I had run the supporting check in Git Bash but reported the environment as
  PowerShell, so the steps did not match the shell they named. My own reading missed it, and
  repro-check caught it.
- What changed:
  - I replaced step 5 with the PowerShell form
    (`git ls-files | Select-String lorem; git grep -il lorem -- "*.test.*" "*.spec.*"`).
  - I re-ran it in the same PowerShell session and pasted the real output.
  - I now tie the "no Lorem test exists" claim directly to the `git grep` result.
  - Lesson: run every reported command in the shell the report names.

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**2026-11-05**

- Graded #386 with issue-scout: accepted.
- Posted my claim from the browser:
  https://github.com/Bashamega/WebDevTools/issues/386#issuecomment-6661084607
- Saved the exact claim text in `beat-2-contribution/claim-draft.md`.
- Read the contribution rules:
  - fork, then a `feature/<name>` branch;
  - the PR template needs `Fixes #386` and a checklist with "added tests" and "tests pass
    locally";
  - a Husky pre-commit hook runs `npm run format:check` and `npm run test`;
  - CI runs format, test, and coverage jobs;
  - auto-moderation closes PRs from new contributors that have more than 3 links;
  - there is no AI policy.
- repro-check accepted the claim for posting.
- I ran the voice guard on the claim after posting it, and it stopped the claim for having no
  report-back date (see Unit 6).
- No clone and no code yet.

Later the same day: local setup and the baseline.

- Forked to `CruzIsaiah/WebDevTools` and cloned it to `C:\Users\howdi\WebDevTools`.
- Created `feature/lorem-ipsum-jest-tests` from `main` at `ce28cbe`.
- Filled in `CLAUDE.local.md` from the Unit 6 template and excluded it through
  `.git/info/exclude` (`git status` clean).
- Ran `npm install`: exit 0, 1138 packages.
- Plain `npm test` fails in PowerShell (`'NODE_OPTIONS' is not recognized`). Decision: use the
  form from `contributing.md`, `$env:NODE_OPTIONS = "--experimental-vm-modules"; npx jest --ci`.
  Result: 9 suites and 36 tests, all passing.
- `npx jest --ci LoremIpsum` gave "No tests found… Pattern: LoremIpsum - 0 matches".
- Wrote `beat-2-contribution/repro-report.md`.
- Wrong turn: repro-check run 1 rejected it on **steps**. My step 5 used `grep`, which
  PowerShell does not have, and the "no test mentions lorem" claim had no step behind it.
- Fixed step 5 to `git ls-files | Select-String lorem; git grep -il lorem -- "*.test.*" "*.spec.*"`
  and re-ran it in the same shell. The only path match is `page.jsx`, and `git grep` printed
  nothing (exit 1).
- repro-check run 2: **accept**, with all five required checks passing.
- The report stays local as Unit 6 reproduction evidence and is intentionally not posted
  upstream. No project code or tests changed.

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [contributing.md](https://github.com/Bashamega/WebDevTools/blob/main/contributing.md):
  setup, the branch/PR flow, and the test commands, including the PowerShell form.
- [`__tests__/customizer/Readme-generator/page.test.jsx`](https://github.com/Bashamega/WebDevTools/blob/main/__tests__/customizer/Readme-generator/page.test.jsx):
  an existing page test in this repo to follow.
- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
