# Dependency automation

Dependabot proposes updates daily. The agent owns technical review and fixes; the user is not expected to review dependency PRs.

Stable compatible dependency updates may merge after meaningful CI succeeds at the exact PR head, every other check completes successfully, and the branch is current. Each run merges at most one PR. Existing deployment integration runs only after those checks.

Major versions, pre-1.0 minor changes, maintainer changes, unusual versions and workflow edits require the agent to examine upstream changes and actual application usage. The agent records compatibility evidence in the administrator-controlled `DEPENDENCY_REVIEWS` repository variable. This JSON uses schema 1 and a `reviews` array; each entry binds `pr`, `head`, `base`, `compatibility: "verified"`, a substantive `rationale`, HTTPS `evidence` links, and `allowedFiles`. A review cannot substitute for CI. Workflow exceptions apply only to named existing workflow files; application-source migrations need separate tested commits.

Missing or failing CI, unresolved migrations, custom source changes and explicit hold labels are technical blockers for the agent to resolve. They are not a human review queue. Rebased or edited commits invalidate the recorded review.

Set `DEPENDENCY_AUTOMATION_PAUSED=true` to pause merging. Manual workflow dispatch defaults to audit; schedules and completed CI can apply eligible updates. Privileged merge workflows never check out or run PR code.

This repository currently lacks meaningful required CI. Updates are proposed, but merging remains blocked until the agent establishes and verifies coverage.
