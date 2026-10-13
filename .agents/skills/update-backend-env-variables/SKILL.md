---
name: update-backend-env-variables
description: "Update Blockscout backend environment-variable docs from a PR. Use when adding, changing, removing, or deprecating backend environment variables."
argument-hint: "<pr-number> [release; default: master]"
user-invocable: true
---

# Update Backend Environment Variables

Use this skill to update the Blockscout backend environment-variable references from a Blockscout PR.

## Arguments

Read the invocation arguments from the user's message:

- Required: a positive PR number from `blockscout/blockscout`.
- Optional: the release to pin the variable to. Use `master` if omitted.

Examples: `/update-backend-env-variables 14936` uses `master`; `/update-backend-env-variables 14936 v12.0.0` pins variables to `v12.0.0`.

If the PR number is missing or invalid, ask the user for it before proceeding. If the release is supplied, accept `master` or a release number such as `v12.0.0`.

## Procedure

1. Use `gh` to inspect the PR's title, description, changed files, and diff in `blockscout/blockscout`.
2. Identify added, changed, removed, or renamed backend environment variables from implementation and config changes, not just mentions in prose. Verify descriptions, defaults, and applicable applications against the code and changelog.
3. Update only the relevant reference:
   - General variables: [backend-env-variables.mdx](../../../setup/env-variables/backend-env-variables.mdx)
   - Chain-specific variables: [backend-envs-chain-specific.mdx](../../../setup/env-variables/backend-envs-chain-specific.mdx)
   - Integration variables: [backend-envs-integrations.mdx](../../../setup/env-variables/backend-envs-integrations.mdx)
   - Removed or replaced variables: [deprecated-env-variables.mdx](../../../setup/env-variables/deprecated-env-variables.mdx)
4. For added variables, include the PR link, version (`master` or the supplied release with the existing `+` convention), default, and applications. Follow the destination table's existing grouping and formatting. Update a documented row if the PR changes its default or behavior; avoid duplicates.
5. For removed or replaced variables, remove them from their active list and add their existing description, default, introduced version, and supplied deprecated-in version to the deprecated list. Do not deprecate variables that were only moved or reformatted.
6. Do not guess missing metadata or category. If the PR does not provide enough evidence to determine a value or destination, ask the user one focused clarification before editing.
7. Preserve unrelated work. Inspect the final diff to confirm only relevant environment-variable rows changed, then report the files updated.
