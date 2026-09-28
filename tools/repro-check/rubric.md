# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| behavior-match | The repro report's artifacts (output excerpts, logs, error text, screenshots) read against the behavior the issue context describes and against what the report's own conclusion claims. | The artifacts support the report's claim about the issue's behavior. If the report claims the bug was reproduced, the artifacts must show the same bug or behavior the issue describes; a different error, an adjacent behavior, a partial run, or an unrelated failure does not pass. If the report concludes it could not reproduce, the artifacts must show that the stated attempt was actually run and that the reported bug did not occur, or that a different result occurred exactly as the conclusion states; a different observed result may pass in that case. | required |
| steps | The reproduction steps section of the repro report, read against the setup facts in the repo-facts block. | Another person could repeat the reproduction from the setup, inputs, commands, and sequence given, from starting state through the trigger, without supplying missing information of their own. | required |
| environment | The environment record in the repro report, read against the versions, platform, and setup the issue context targets. | The record names the version, OS/platform, and repository or tool setup needed to understand and repeat the result, and those details are appropriate for the issue being tested. | required |
| honest-result | The repro report's stated conclusion read against its own artifacts and the issue context. | The conclusion matches what the artifacts actually show. An evidenced cannot-reproduce passes. Claiming reproduction when the artifacts show something different does not pass. | required |
| repo-rules | The claim comment and the repro report read against the contribution and reporting rules named in the repo-facts block and the issue context, including the repo's AI policy if it states one. | Both comments follow the repository's stated contribution and reporting rules and conventions, including any required template. Disclosure: if the repo states no AI-disclosure policy, there is no disclosure requirement to fail; if the repo requires disclosure of AI assistance, the comments must carry that disclosure in the form the repo asks for, and silence about AI is not compliance. Where the repo requires disclosure of all AI use and no disclosure appears in the comments, this check fails. | required |

## Verdict rule

Accept only if every required check passes. Any required check graded
`fail` or `unclear` means reject. All five checks are required, so
there are no preferred checks to set aside.
