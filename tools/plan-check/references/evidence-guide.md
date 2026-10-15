# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

**Where it lives**

In an eval package, read the candidate plan's diagnosis or stated cause together with the issue context and the repro-evidence block. Use the reproduced commands, observed output, expected behavior, and any notes that narrow the likely cause.

In live mode, read the student's diagnosis in `plan.md` against the GitHub issue, the student's posted repro comment from Unit 2, and any repository evidence that was used during reproduction.

**What good looks like**

The stated cause should explain behavior that the repro evidence actually shows. It should not contradict the observed output, ignore important evidence, or claim a cause that the available evidence does not support.

## Scope

**Where it lives**

In an eval package, read the candidate plan's scope statement, files or areas to change, implementation approach, issue context, thread highlights, and repo-facts block.

In live mode, read the scope, in-scope and out-of-scope statements, and named files in `plan.md` against the GitHub issue and relevant repository structure.

**What good looks like**

The work should be limited to one bounded change needed to address the issue. Proposed files and changes should connect directly to the reproduced problem, without unrelated cleanup, redesigns, or drive-by changes.

## Executability

**Where it lives**

In an eval package, read the candidate plan's files-to-change section, implementation approach, ordered work steps, and relevant repo facts.

In live mode, use the files, components, and approach named in `plan.md` together with the actual repository layout and relevant documentation.

**What good looks like**

Another developer should be able to identify where to start, what main files or components are involved, and what change is intended without asking the author to invent the missing implementation strategy.

## Test plan

**Where it lives**

In an eval package, read the candidate plan's test plan together with the repro-evidence block, especially the original reproduction steps, commands, inputs, observed behavior, and expected behavior.

In live mode, compare the test plan in `plan.md` with the Unit 2 repro steps and the before-state evidence from the posted repro.

**What good looks like**

The test plan should exercise the real behavior involved in the issue and describe an observable result. It should be possible to tell from the test output whether the original bug is still present or the intended fix worked.

## Honesty

**Where it lives**

In an eval package, read the plan's risks, assumptions, unknowns, and any deviation information, then compare those claims with the repro evidence and repo facts.

In live mode, read the risks and unknowns in `plan.md`. After implementation, read the `## Deviations` section and compare it with what was actually built.

**What good looks like**

The plan should not present a materially uncertain claim as established fact. It does not need to invent risks or unknowns when the available evidence is already sufficient. When an important uncertainty really exists and could affect the implementation, the plan should acknowledge it or identify a reasonable way to verify it. If the build changes from the original plan, the deviation should be stated clearly rather than hidden.

## Comms

**Where it lives**

In an eval package, read the draft plan comment against the issue context, thread highlights, repo-facts block, contribution instructions, templates, and any stated AI-use or disclosure rules.

In live mode, compare `comment.md` with the actual GitHub issue thread, maintainer comments, repository contribution documentation, and any required templates or policies.

**What good looks like**

The comment should respond to the actual issue and respect relevant maintainer requests and repository conventions. Any explicit contribution-policy requirement that applies to the comment or contribution, including required AI-use disclosure, should be satisfied. The comment should not ignore constraints from the thread, contradict the proposed plan, omit a required disclosure, or use generic boilerplate that misses issue-specific requirements.