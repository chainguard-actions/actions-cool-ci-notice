<!-- markdownlint-disable -->

# Hardening Report: actions-cool--ci-notice/v1.1.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **actions-cool--ci-notice/v1.1.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference actions using mutable branch refs (`@main`) instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the referenced branch is compromised or force-pushed. Failing references: `actions/checkout@main` and `actions-cool/ci-notice@main` in ci-notice.yml; `actions/checkout@main` in test.yml.

Locations:

- `.github/workflows/ci-notice.yml:12`
- `.github/workflows/ci-notice.yml:14`
- `.github/workflows/test.yml:11`

### missing-permissions (severity: medium)

Neither workflow file defines a top-level `permissions:` block, and no job in either file defines job-level `permissions:`. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/ci-notice.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files: (1) Pinned all mutable @main action references to full 40-char commit SHAs — actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1 and actions-cool/ci-notice@cfdbfac7f0a65d8e7a15306717b59f4bc6078bc8 — with original ref preserved as inline comments. (2) Added top-level permissions blocks to both files: ci-notice.yml gets `contents: read` + `issues: write` (the ci-notice action creates issues), test.yml gets `contents: read` only (checkout + build).

