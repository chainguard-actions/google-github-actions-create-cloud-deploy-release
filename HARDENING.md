<!-- markdownlint-disable -->

# Hardening Report: google-github-actions--create-cloud-deploy-release/v1.1.7

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google-github-actions--create-cloud-deploy-release/v1.1.7** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference external actions or reusable workflows using mutable version tags instead of full 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the tag is moved or the referenced repository is compromised.

- `.github/workflows/draft-release.yml` line 17: `uses: 'google-github-actions/.github/.github/workflows/draft-release.yml@v3'` (tag `v3`)
- `.github/workflows/integration.yml` line 49: `uses: 'google-github-actions/auth@v2'` (tag `v2`)
- `.github/workflows/integration.yml` line 55: `uses: 'google-github-actions/setup-gcloud@v2'` (tag `v2`)
- `.github/workflows/release.yml` line 10: `uses: 'google-github-actions/.github/.github/workflows/release.yml@v3'` (tag `v3`)

Note: These are all marked `# ratchet:exclude`, indicating they are intentionally excluded from SHA-pinning, but they remain unpinned and therefore a security risk.

Locations:

- `.github/workflows/draft-release.yml:17`
- `.github/workflows/integration.yml:49`
- `.github/workflows/integration.yml:55`
- `.github/workflows/release.yml:10`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all four unpinned action references to full commit SHAs:
1. `.github/workflows/draft-release.yml` line 17: `google-github-actions/.github/.github/workflows/draft-release.yml@v3` → `@29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3`
2. `.github/workflows/integration.yml` line 49: `google-github-actions/auth@v2` → `@c200f3691d83b41bf9bbd8638997a462592937ed # v2`
3. `.github/workflows/integration.yml` line 55: `google-github-actions/setup-gcloud@v2` → `@e427ad8a34f8676edf47cf7d7925499adf3eb74f # v2`
4. `.github/workflows/release.yml` line 10: `google-github-actions/.github/.github/workflows/release.yml@v3` → `@29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3`

All SHAs were resolved using lookup_action_sha. The original version tags are preserved as inline comments for readability.

