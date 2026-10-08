# Working on WURK documentation

Read `README.md` for the checkout, source and publication workflow.

- This is the public `STATIKHEADZ/docs` repository. Keep commits and Git operations
  scoped to this checkout. In the shared workspace the implementation checkout is
  `../workspace`; it is a separate repository, not part of this one.
- Use the implementation's public skill and its `skill-documents.json` manifest to
  find current user guides. Verify specific contracts against the relevant code and
  tests when implementation access is available. If it is unavailable, use public
  released documentation and identify facts that still need verification.
- Check deployed API and published client availability separately. Do not describe
  an unreleased improvement as part of an existing npm release just because the
  local package version matches it.
- Write for users completing tasks: explain the operation, required inputs, expected
  result and recovery action. Keep the commissioning path prominent and make earning,
  service listing and worker flows easy to find. Match examples to the stated client.
- Publish only relevant user-facing information. Do not copy internal preparation
  files, database/operator instructions, secrets, real payment proofs or private
  customer data into pages or public review notes. Retired features do not need
  historical exclusion lists in onboarding guides.
- `docs.json` owns current navigation. Inspect the existing `mint.json` and deployed
  configuration before any migration. Preserve this checkout's `.replit` unless a
  task explicitly requires changing its runtime configuration.
- Keep shared API facts consistent with the maintained public guides and specs.
  Update related examples and links together. A full automatic cross-repository
  documentation sync is not installed by this workflow.
- Use a work branch for documentation changes. Check diffs and affected links;
  preview and validate site changes using Mintlify. A production-branch merge can
  publish the site; repository setup alone does not include that publication.
