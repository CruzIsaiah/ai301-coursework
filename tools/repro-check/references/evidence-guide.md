# Evidence guide: where proof lives in a reproduction package

## Environment

**Where it lives.** Eval mode: the environment record in the repro
report section of the bundle, compared against the versions, platform,
and setup named in the issue context and the repo-facts block. Live
mode: the environment lines in the student's draft repro comment,
compared against the issue body's stated target and the repo's README
or contributing docs for the supported versions.

**What good looks like.** The record names the version of the tool or
package under test, the OS/platform it ran on, and how the repo or tool
was set up (install method, branch or commit, relevant configuration).
The versions and platform named either match what the issue targets, or
the difference is called out in the report rather than left for the
reader to notice.

## Steps

**Where it lives.** Eval mode: the reproduction steps in the repro
report, read together with the setup facts in the repo-facts block.
Live mode: the numbered steps in the draft repro comment, read against
the repo's documented install and run instructions.

**What good looks like.** A stranger starting from the stated starting
state could reach the trigger using only the setup, inputs, commands,
and ordering given, without inventing a missing step or guessing a
value. Commands appear as commands and inputs appear as literal values,
so nothing important hides behind a phrase like "set up the project" or
"run it with the usual config."

## Behavior shown

**Where it lives.** Eval mode: the artifacts in the repro report —
output excerpts, logs, error text, stack traces, screenshots — read
directly against the behavior the issue context describes. Live mode:
the same artifacts in the draft repro comment, read against the issue
body and any later comments that restate the symptom.

**What good looks like.** Read the artifacts against what the report
concludes; the two shapes of valid evidence differ.

- **Successful reproduction.** The artifact shows the specific behavior
  the issue describes: the same error or message, on the same
  operation, with the same observable outcome. A related but different
  failure — a different exception, a failure at an earlier step, a
  partial run, a symptom that merely resembles the reported one — does
  not count as showing the issue's bug, even when it is a real problem,
  and does not become acceptable because the report sounds confident.
- **Honest cannot-reproduce.** The artifact shows that the stated
  attempt actually ran and that the reported bug did not appear: the
  command or trigger executed, with its real output, and that output is
  the normal or differing result the conclusion describes. A different
  observed result is valid evidence here, provided the steps were
  genuinely attempted and the conclusion describes that result
  accurately. What fails is a cannot-reproduce with no artifact of the
  attempt, or one whose output does not match what the conclusion says
  happened.

The question in both cases is whether the artifacts support the
report's claim about the issue's behavior, not whether the bug itself
appears.

## Honesty

**Where it lives.** Eval mode: the conclusion or summary line of the
repro report, read against that same report's own artifacts and the
issue context. Live mode: the conclusion in the draft repro comment,
read against the artifacts pasted in the same comment.

**What good looks like.** The conclusion states no more than the
artifacts support. A cannot-reproduce backed by the environment,
the steps attempted, and the actual output is a valid, complete result.
A report that says "reproduced" while its artifacts show a different
failure, a partial run, or no trigger at all is claiming more than it
shows.

## Comms

**Where it lives.** Eval mode: the claim comment and the repro report,
read against the contribution and reporting rules named in the
repo-facts block and against the conventions visible in the issue
context. Live mode: the draft claim and repro comments, read against
the repo's CONTRIBUTING file, issue and comment templates, any
AI-use disclosure policy, and how the issue thread itself is written.

**What good looks like.** The comments follow the repository's stated
requirements — the required template is used where one is required, and
the words are specific to this issue, naming its actual symptom, files,
or versions, rather than boilerplate that would fit any issue in any
repo.

**Reading the AI policy.** First locate the policy: the repo-facts
block's contribution-policy line in eval mode, the repo's CONTRIBUTING
or AI policy file in live mode. Then apply it in one of two ways.

- The repo states no AI-disclosure policy: there is no disclosure
  requirement here, so disclosure cannot fail this check. Judge the
  comments on template and conventions alone.
- The repo requires disclosure of AI assistance: look for the
  disclosure in the claim comment and the repro report themselves, in
  the form the policy asks for (typically naming the tool used and the
  extent of the assistance). A comment that says nothing about AI has
  not disclosed. Silence is not compliance, and the absence of an
  explicit AI claim is not evidence that no assistance occurred. Where
  the policy covers all AI use and no disclosure appears anywhere in
  the comments, the requirement is unmet.
