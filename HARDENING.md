<!-- markdownlint-disable -->

# Hardening Report: actions-cool--ci-notice/v1.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **actions-cool--ci-notice/v1.0.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference actions using mutable branch refs (`@main`) instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the referenced branch is compromised or force-pushed. Failing references: `actions/checkout@main` and `actions-cool/ci-notice@main` (in ci-notice.yml); `actions/checkout@main` (in test.yml).

Locations:

- `.github/workflows/ci-notice.yml:11`
- `.github/workflows/ci-notice.yml:13`
- `.github/workflows/test.yml:8`

### missing-permissions (severity: medium)

Neither workflow file defines a top-level `permissions:` block, and no job within them defines job-level permissions. Without explicit permissions, workflows run with the default (potentially broad) token permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/ci-notice.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files: (1) Pinned all @main action references to full commit SHAs — actions/checkout@main → @f548e57e544e1ff5a4c46bf1e1b8685f8e4a348a and actions-cool/ci-notice@main → @cfdbfac7f0a65d8e7a15306717b59f4bc6078bc8, with # main comments for readability. (2) Added top-level `permissions: {}` to both workflow files to enforce least privilege. In ci-notice.yml, also added job-level `permissions: issues: write` since the ci-notice action creates GitHub issues.

