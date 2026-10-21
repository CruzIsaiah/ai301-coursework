# Procedure: how this tool grades a PR package

## Read order

1. Decide the mode first. If you were handed a package bundle file, you are in eval mode; otherwise you are in live mode. The mode decides every source below.

   - **Live mode sources:** the files named by the command (the student's `plan.md` with its Deviations, the draft PR title and description, and any test evidence file named), the output of `git diff main...HEAD` and `git log main..HEAD` run from the student's working copy, the issue thread, the repository PR template, and `docs/CONTRIBUTING.md` from the scoped repo. A house-chain student's plan is the house plan and their repro is the house repro pack.
   - **Eval mode sources:** the frozen package bundle and nothing else. Do not fetch anything, do not run `git`, and do not read any file outside the bundle. Every "source" named in the steps below means the matching part of the bundle (its issue context, repo-facts and policy information, plan, PR title and description, commits, diff, and test evidence).

2. Live mode only: read `scope.md` and `voice-guide.md` as `SKILL.md` directs, before any package source. Stop here if `SKILL.md`'s scope refusal applies. Record the scoped repo and every house rule. In eval mode, skip both files.

3. Read the issue (live: the issue thread; eval: the bundle's issue context). Record the reported behavior, the expected behavior, maintainer guidance, and any constraint on what the fix may or may not do.

4. Read the repository requirements (live: the PR template and `docs/CONTRIBUTING.md`, plus the house rules recorded in step 2; eval: the bundle's repo-facts and policy information). Record, as separate lists: every section the PR template asks for; every stated contribution requirement (branch naming, target branch, issue-link format, commit or PR conventions, one PR per issue); the AI-use disclosure requirement (live: always the course requirement of a disclosure in the description's "Notes for Reviewers", plus any further repository rule; eval: the requirement the bundle states, if any); and the stated test, lint, or build commands, if any. Where a source says nothing about one of these, record that it is silent and name the source.

5. Read the accepted plan, including every Deviation recorded in it. Record its scope, the files it names, its approach, its test plan (each test and the observable result it expects), and each Deviation with the reason it gives.

6. Read the diff and commits next (live: `git diff main...HEAD` and `git log main..HEAD`; eval: the bundle's diff and commits). Record every changed file and, per file, what each hunk does. Record each commit's message and what it contains.

7. Read the test evidence (live: the test output the student names or pastes, and what the PR description quotes; eval: the bundle's test evidence). Record each command run, what it ran against, and the result shown.

8. Read the PR title and description last. Record every claim it makes: what changed, what was tested and how, any fidelity claim about the plan, any shortfall it discloses, the issue link, and the AI-use disclosure text. Live mode: before a PR exists, the draft description file named by the command (for example `pr_draft.md`) is authoritative; once the PR exists, the live GitHub PR description is authoritative for the PR's current state, including CI-related checklist and status text, and if the local draft differs from it, record that the local draft is stale and how it differs rather than treating the two as identical.

9. Keep the order: the plan before the diff, so the diff is read against what was promised rather than the plan being read to fit the diff; the diff and the test evidence before the description, so the description's claims are checked against facts you already recorded instead of shaping how you read them. Keep sources and claims in separate notes: a fact is established only by the diff, the test evidence, or a repository source, never because the description says so.

## Evidence gathering

Gather evidence for each rubric check by pairing the notes from the read order. Record each pairing's result as a short note that names its source, so the check's evidence line can quote it.

1. **Plan fidelity (diff against the plan and Deviations).** Make two lists. First, for every hunk in the diff, record whether it is covered by the plan's scope and approach, covered by a recorded Deviation, or covered by neither. Second, for every item the plan committed to, record whether the diff delivers it, and if not, whether a Deviation or the PR description says so and why.

2. **Description matches diff (description against the actual diff).** For every change the description claims, record the hunk that delivers it, or that no hunk does. For every material change in the diff, record whether the description mentions it. For any fidelity claim ("implements the plan as posted", "no other changes"), record whether the two lists from step 1 contradict it.

3. **Test evidence (evidence against the plan's test plan and the PR's testing claims).** First, for the primary bug-fix evidence (the plan's reproduction), record the observable output shown for it on the branch's code, whether it is the same scenario the plan's test plan names (not a substitute case), and whether that result distinguishes the fixed behavior from the reproduced bug; if it is only an assertion with no observable output, record that. Then, for every supporting test-plan item (test suite, lint, typecheck, smoke check, negative control), record the command or check named and the specific result stated, or that the claim is vague (no command, no specific result); note anything elsewhere in the package that contradicts it. Where no evidence shows a test was run, record whether the PR discloses it as not run and why. For every "tested" or "verified" claim in the description, record the evidence that backs it (shown output, or a named command with a specific result), or that none does. Live mode: a result mentioned only in `plan.md` or its Deviations may be recorded as context, but it does not replace captured command and result evidence in the test evidence file or the PR description where that evidence is required.

4. **Repo checks run (evidence against the repo's stated commands).** For each test, lint, or build command (or template checklist item) recorded in read-order step 4, record where the package names it and the specific result it states for the branch, or that it is not mentioned or only vaguely claimed; note anything in the package that contradicts it. If a run failed, record whether the failure is reported and how the PR explains it. If the repository states no required commands, record that and the source checked. Live mode: as in step 3, a result mentioned only in `plan.md` or its Deviations does not replace captured command and result evidence in the test evidence file or the PR description. If the PR has not been opened yet, CI cannot have run: an unchecked "CI is green" item does not by itself fail this check (or Template completeness in step 6), provided the draft discloses that CI is pending and will be confirmed after the PR opens; record whether it does. Once a PR exists, grade red or missing required CI by the repository's stated policy.

5. **Diff focus (hunks against the described change).** Using the per-hunk notes from read-order step 6, record every hunk that does not serve the change the plan and description describe, naming its kind: debug output, commented-out code, stray or generated file, unrelated formatting or lockfile churn, or unrelated logic.

6. **Template completeness (description against the PR template).** For every template section recorded in read-order step 4, record whether the description has it and whether its content is specific to this PR, says the section does not apply, or is still placeholder text.

7. **Contribution policy (PR against stated contribution requirements).** For every contribution requirement recorded in read-order step 4, record the PR's matching fact (live: the current branch name from `git branch --show-current`, the target branch, the issue link in the description; eval: the matching facts in the bundle) and whether it meets the requirement as stated. Grade branch naming against the stated rule only; do not assume a prefix the repository does not state.

8. **AI-use disclosure (description against the disclosure requirement).** Live mode: record the disclosure text under the description's "Notes for Reviewers" section, or that it is missing, empty, placeholder, placed elsewhere, or not specific to how AI was used on this change; also record any further repository disclosure rule and whether it is met. Repository silence about AI does not remove the live-mode requirement. Eval mode: if the bundle states a disclosure requirement, record the description's disclosure text, or that it is missing, empty, or placeholder; if the bundle states no AI policy or disclosure requirement, record that and the bundle section checked.

9. **Commit hygiene (commits).** From the commit notes, record any message that does not describe its change and any fix-up noise ("wip", "oops", reverted experiments).

10. Use only evidence that is in the package or, in live mode, in the sources named in read-order step 1. Do not invent requirements, evidence, test results, or repository facts. When a source cannot be read (a failed fetch, a failed `git` command, a part missing from the bundle), record that it is absent and which checks depend on it; do not substitute another source.

## Check execution

1. Grade every check in `rubric.md`, in rubric order: Plan fidelity, Description matches diff, Test evidence, Repo checks run, Diff focus, Template completeness, Contribution policy, AI-use disclosure, Commit hygiene. Eval mode grades every check; none is skipped.

2. For each check, apply its pass condition from `rubric.md`, word for word, to the evidence gathered for that check. Grade the outcome, not the write-up: never grade on description length, number of commits, heading count, or formatting unless a stated repository requirement asks for it.

3. Grade `pass` when the gathered evidence satisfies the pass condition. Grade `fail` when the gathered evidence shows the pass condition is not met. Grade `unclear` only when evidence needed to decide is genuinely absent, conflicting, or too incomplete to support either grade.

4. When the repository states no requirement for a check (no required commands, or in eval mode no disclosure rule), grade it as `rubric.md`'s verdict rule directs: `pass`, with an evidence line naming the source checked and found silent. Do not grade a silent requirement `unclear`, and do not invent one. Exception: in live mode the AI-use disclosure is always required by the course, so repository silence about AI never passes that check.

5. When a PR does less than the plan or than everything, grade the disclosure as the rubric directs: an honestly recorded Deviation or a test disclosed as not run, with its reason, satisfies the relevant pass condition. An undisclosed shortfall fails.

6. Do not fill missing evidence with a reasonable-sounding assumption. If the fact is needed and absent, grade `unclear`.

7. For each check, write a one-line evidence entry: the fact or quote that decided the grade, with its source (a file and hunk, a test command and result, a template section, a CONTRIBUTING.md line, a bundle section). "Looks fine" is not evidence.

8. Reuse gathered notes across checks: Description matches diff reuses the Plan fidelity lists, and Diff focus reuses the per-hunk notes. Re-read a source only when a later finding contradicts an earlier note; then re-grade every check that relied on it.

9. Where this procedure is silent on a step you need, take the narrowest reading that lets you continue and report the gap in the summary.

## Verdict assembly

1. Collect the grade and evidence line for every check in `rubric.md`.

2. Apply the rubric's verdict rule exactly: `accept` only if every required check passes.

3. If any required check is `fail`, the verdict is `reject`.

4. If any required check is `unclear`, treat it as `fail`, as the rubric directs; the verdict is `reject`.

5. Preferred checks (Commit hygiene) are graded and reported but never change the verdict.

6. Name the deciding check: on `reject`, the first required check in rubric order whose grade is `fail` or `unclear`; quote its evidence line in the summary as the reason the PR is held, then list any other failing or unclear required checks after it. On `accept`, state that every required check passed. If the problem is missing evidence, say what evidence was not provided rather than inventing it.

7. Live mode: after the check lines, report any voice-guide rule the PR title or description breaks, quoting the rule and the line. This never changes the verdict.

8. Report any procedure gaps from check execution step 9.

9. End with the fenced JSON block from `SKILL.md`: one entry per rubric check in rubric order, each with its grade and one-line evidence, and the verdict. Nothing follows the block.
