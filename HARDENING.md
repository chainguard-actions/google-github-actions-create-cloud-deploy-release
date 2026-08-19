<!-- markdownlint-disable -->

# Hardening Report: google-github-actions--create-cloud-deploy-release/v2.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google-github-actions--create-cloud-deploy-release/v2.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Three workflow files contain `uses:` references pinned to mutable tags instead of full 40-character commit SHAs, making them vulnerable to supply-chain attacks if the referenced tag is moved or overwritten.

Failing references:
- `.github/workflows/draft-release.yml`: `uses: 'google-github-actions/.github/.github/workflows/draft-release.yml@v3'` (tag `v3`)
- `.github/workflows/integration.yml`: `uses: 'google-github-actions/auth@v3'` (tag `v3`)
- `.github/workflows/integration.yml`: `uses: 'google-github-actions/setup-gcloud@v2'` (tag `v2`)
- `.github/workflows/release.yml`: `uses: 'google-github-actions/.github/.github/workflows/release.yml@v3'` (tag `v3`)

These should each be pinned to a full SHA digest, e.g. `uses: 'google-github-actions/auth@<40-hex-sha>' # v3`.

Locations:

- `.github/workflows/draft-release.yml:14`
- `.github/workflows/integration.yml:44`
- `.github/workflows/integration.yml:50`
- `.github/workflows/release.yml:8`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all four mutable tag references to full commit SHAs:
1. `.github/workflows/draft-release.yml`: `google-github-actions/.github/.github/workflows/draft-release.yml@v3` → `@29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3`
2. `.github/workflows/integration.yml`: `google-github-actions/auth@v3` → `@7c6bc770dae815cd3e89ee6cdf493a5fab2cc093 # v3`
3. `.github/workflows/integration.yml`: `google-github-actions/setup-gcloud@v2` → `@e427ad8a34f8676edf47cf7d7925499adf3eb74f # v2`
4. `.github/workflows/release.yml`: `google-github-actions/.github/.github/workflows/release.yml@v3` → `@29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3`

All SHAs were resolved using lookup_action_sha against the live GitHub API. Original tags preserved in comments for readability.

