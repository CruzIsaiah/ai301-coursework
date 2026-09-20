# Issue Selection Rubric

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer activity | Last 5 default-branch commits, commit authors, maintainer first-response sample, and Owner/Member/Collaborator comments in the issue thread | PASS if there is at least one human-authored default-branch commit within 90 days of the eval capture date/live date, OR an Owner/Member/Collaborator comment within 90 days. Bot-only activity does not count. | Required |
| Repository is active | Archived status, latest release, default-branch activity, and last push | PASS if the repository is not archived AND either: (a) it has a release within the last 6 months, OR (b) it has a human-authored default-branch commit within the last 90 days. An archived repository always fails. | Required |
| Issue is appropriately scoped for a newcomer | Issue body and comment thread | PASS if the issue names a settled, specific change and none of these hold: (a) it is an umbrella or tracking issue whose sub-items are meant to be split into separate work; multiple sub-steps serving one deliverable are not an umbrella; (b) it is a pure usage or support question; (c) a maintainer warns that the fix requires reworking core internals; a maintainer diagnosing the cause or naming files/components is scoping help and does not fail by itself; (d) the specific change is left for the contributor to choose rather than stated; (e) the required behavior is still unsettled, such as an unanswered design question in the body/thread or repeated closed-unmerged attempts with no maintainer resolution; (f) it depends on an unresolved product decision or missing required artifact. A terse description or missing reproduction steps does not fail by itself, especially when the opener is a maintainer or the issue carries a good-first-issue label. | Required |
| Issue is not already actively claimed | Assignees, linked PRs, PRs mentioned in comments, and claim comments in the thread | PASS if there is no current assignee, no open PR for the issue, and no active recent claim within 30 days. A closed/unmerged PR or clearly stale abandoned claim does not automatically fail. In Path Review live mode, apply the house rule in scope.md so ordinary classmate claim comments do not block the issue. | Required |
| AI-assisted contributions are permitted | CONTRIBUTING.md, linked contribution docs, AI policy files, PR templates, and issue templates | PASS if AI use is allowed, allowed with conditions, or the repository is silent about AI use. FAIL only when the repository explicitly prohibits AI-generated/AI-assisted contributions. | Required |
| Newcomer-fit signals | Good-first-issue labels, maintainer scoping comments, clear acceptance criteria, project adoption/activity | PASS if at least one positive newcomer-fit signal is present. FAIL if none are present. This check is Preferred and never changes the accept/reject verdict; it is used only to rank accepted issues. | Preferred |

## Verdict rule

- ACCEPT only when every Required check passes.
- REJECT when any Required check fails.
- Treat genuinely missing or unavailable evidence as UNCLEAR.
- For Required checks, UNCLEAR counts as REJECT unless the check explicitly defines missing evidence as acceptable.
- For the AI-policy check, absence of an AI policy counts as PASS rather than UNCLEAR.
- Preferred checks do not determine accept/reject. Use them only to rank accepted issues by fit.
- In live mode, apply any repository-specific house rules in scope.md when interpreting evidence.
