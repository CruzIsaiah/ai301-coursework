# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis | The plan's stated diagnosis read against the reproduced behavior, commands, and output in the repro evidence. | Pass if the diagnosis is consistent with the reproduced evidence, explains the likely cause of the observed behavior, and does not ignore or contradict important evidence. | required |
| Scope | The plan's scope, files to change, and approach read against the issue request, thread highlights, and repo facts. | Pass if the proposed work is one bounded change that addresses the issue without adding unrelated work or expanding beyond what the issue requires. | required |
| Cause targeting | The plan's proposed approach read against its diagnosis and the reproduced evidence. | Pass if the proposed change addresses the likely cause supported by the evidence rather than only hiding or working around the visible symptom. | required |
| Executability | The plan's files and implementation approach read against the repo facts and relevant repository structure. | Pass if another developer could begin implementing the change from the plan without having to guess the main files, components, or implementation steps. | required |
| Test plan | The plan's test plan read against the original repro steps and reproduced before-state. | Pass if the tests exercise the real behavior involved in the issue and define an observable result that would distinguish the fixed behavior from the reproduced bug. | required |
| Unknowns | The plan's risks, assumptions, and unknowns read against the available repro evidence and repo facts. | Pass if the plan does not present an important uncertain claim as established fact. A plan does not need to invent risks or unknowns when the available evidence is sufficient; when a material uncertainty is present, it should be acknowledged or have a reasonable way to verify it. | required |
| Thread and conventions | The draft plan comment read against the issue thread highlights and the repo's stated conventions, contribution policies, and repo-facts block. | Pass if the proposed plan and comment respect relevant maintainer requests, issue constraints, and repository conventions, including any required contribution or AI-use disclosures. Fail when the comment omits a requirement the repository explicitly says applies to that comment or contribution. | required |

## Verdict rule

Accept only if every required check passes. Reject if any required check fails or is unclear. Preferred checks, if any are added later, do not change the final verdict.