<!-- markdownlint-disable -->

# Hardening Report: actions-cool--ci-notice/v1.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **actions-cool--ci-notice/v1.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow files reference actions using mutable branch refs (`@main`) instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks where a compromised or updated action could execute arbitrary code. Failing references: `actions/checkout@main` and `actions-cool/ci-notice@main` in ci-notice.yml; `actions/checkout@main` in test.yml.

Locations:

- `.github/workflows/ci-notice.yml:12`
- `.github/workflows/ci-notice.yml:14`
- `.github/workflows/test.yml:9`

### missing-permissions (severity: medium)

Neither workflow file defines a top-level `permissions:` block, and no job within them defines job-level permissions. Without explicit permissions, workflows run with the default (often broad) token permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/ci-notice.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files:

1. **unpinned-uses**: Pinned all three mutable `@main` references to full 40-character commit SHAs:
   - `actions/checkout@main` → `actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1 # main` (ci-notice.yml and test.yml)
   - `actions-cool/ci-notice@main` → `actions-cool/ci-notice@cfdbfac7f0a65d8e7a15306717b59f4bc6078bc8 # main` (ci-notice.yml)

2. **missing-permissions**: Added `permissions: {}` at the top level of both workflow files to deny all permissions by default. In ci-notice.yml, also added `permissions: issues: write` at the job level since the ci-notice action creates GitHub issues (notice-types: 'issue').

