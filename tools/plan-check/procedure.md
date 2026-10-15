# Procedure: how this skill grades a plan package

## Read order

1. Read the issue summary and thread highlights first. Record the behavior being reported, any requested constraints, maintainer guidance, and anything the proposed change is expected or not expected to do.

2. Read the repro evidence next. Record the commands or steps that reproduced the issue, the observed behavior, the expected behavior, and any evidence that points to a likely cause.

3. Read the repo facts and stated repository conventions. Record relevant files, components, architecture, testing commands, contribution rules, and implementation constraints.

4. Read the proposed plan only after the source evidence above. Record its diagnosis, scope, files to change, implementation approach, test plan, risks, assumptions, and unknowns.

5. Read the draft plan comment last. Record what it tells maintainers about the proposed cause, scope, implementation, and verification.

6. Keep the source evidence separate from claims made by the plan. Do not treat something as established fact only because the plan says it is true.

## Evidence gathering

1. For the Diagnosis check, compare the plan's stated diagnosis with the reproduced behavior, commands, output, and other observations in the repro evidence. Record any supporting evidence, contradictions, or missing links.

2. For the Scope check, compare the plan's scope, files to change, and implementation approach with the issue request, thread highlights, and repo facts. Record whether each proposed change is necessary for the issue and whether unrelated work has been added.

3. For the Cause targeting check, compare the proposed implementation approach with both the diagnosis and the repro evidence. Record whether the change acts on the likely source of the reproduced behavior or only hides the visible symptom.

4. For the Executability check, use the plan's named files, components, and implementation steps together with the repo facts. Record whether another developer could identify where to begin and what main changes to make without inventing missing implementation details.

5. For the Test plan check, compare the proposed tests with the original repro steps and before-state. Record what real behavior the test exercises, what result is observable, and how the result would distinguish the fixed behavior from the bug.

6. For the Unknowns check, inspect the plan's risks, assumptions, and unknowns and compare them with actual uncertainty shown by the repro evidence and repo facts. Do not require the plan to invent an unknown when the available evidence is sufficient. Record any materially uncertain claim that the plan presents as settled, and whether the plan acknowledges or provides a way to verify uncertainty that could change the implementation.

7. For the Thread and conventions check, compare the draft plan comment and proposed work with the issue thread highlights, maintainer requests, repo facts, and stated repository conventions. Record any conflict, ignored instruction, or convention the plan fails to follow.

8. Use only evidence present in the package or available through the locations defined in the evidence guide. Do not invent missing repository facts or assume an unsupported cause.

## Check execution

1. Grade the checks in this order: Diagnosis, Scope, Cause targeting, Executability, Test plan, Unknowns, then Thread and conventions.

2. For each check, apply the pass condition from `rubric.md` to the evidence gathered for that check.

3. Grade a check `pass` when the available evidence satisfies the pass condition without an important contradiction.

4. Grade a check `fail` when the available evidence shows that the pass condition is not satisfied.

5. Grade a check `unclear` when evidence needed to decide the check is genuinely missing, conflicting, or too incomplete to support either pass or fail.

6. Do not convert missing evidence into a pass by making a reasonable-sounding assumption. If the missing information is necessary to decide the check, use `unclear`.

7. For the Thread and conventions check, compare the draft plan comment and proposed work with the issue thread highlights, maintainer requests, repo facts, and stated repository conventions. Check explicit contribution-policy requirements, including required AI-use disclosures when the repository says they apply. Record any conflict, ignored instruction, missing required disclosure, or convention the plan or comment fails to follow.

8. Once evidence has been gathered for a check, reuse those notes for related checks. Re-read the full package only if later evidence creates a contradiction or changes the meaning of an earlier fact.

9. Judge the proposed outcome and whether the plan can safely be built from. Do not grade based on writing length, number of headings, formatting style, or other presentation details unless a repository rule specifically requires them.

## Verdict assembly

1. Collect the final grade for every check in `rubric.md`.

2. Apply the rubric verdict rule exactly: accept only if every required check passes.

3. If any required check is `fail`, the final verdict is `reject`.

4. If any required check is `unclear`, treat it as a failure and make the final verdict `reject`.

5. Preferred checks, if any are added later, may be reported but never change the final accept or reject verdict.

6. For each failed or unclear required check, quote or identify the smallest piece of package evidence that explains the grade. If the problem is missing evidence, state what necessary evidence was not provided instead of inventing it.

7. End with the final binary verdict required by the skill: `accept` for a ready plan or `reject` for a plan that should be held.