<!-- markdownlint-disable -->

# Hardening Report: actions-cool--ci-notice/v1.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **actions-cool--ci-notice/v1.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference GitHub Actions using mutable branch refs (`@main`) instead of immutable 40-character SHA commit digests. This exposes the workflow to supply-chain attacks where a compromised upstream action could execute arbitrary code. Affected references: `actions/checkout@main` (both files) and `actions-cool/ci-notice@main` (ci-notice.yml).

Locations:

- `.github/workflows/ci-notice.yml:11`
- `.github/workflows/ci-notice.yml:13`
- `.github/workflows/test.yml:9`

### missing-permissions (severity: medium)

Neither workflow file defines a top-level `permissions:` block, and no job within either file defines job-level permissions. Without explicit permissions, workflows run with the default (often broad) token permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/ci-notice.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files (.github/workflows/ci-notice.yml and .github/workflows/test.yml):
1. unpinned-uses: Replaced all three mutable @main action references with pinned full SHA digests — actions/checkout@f548e57e544e1ff5a4c46bf1e1b8685f8e4a348a (both files) and actions-cool/ci-notice@cfdbfac7f0a65d8e7a15306717b59f4bc6078bc8 (ci-notice.yml). Original ref preserved as inline comment.
2. missing-permissions: Added top-level `permissions: {}` block to both workflow files to enforce least privilege, since neither workflow requires any specific GitHub token permissions.

