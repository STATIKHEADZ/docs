# WURK documentation

Source for [docs.wurk.fun](https://docs.wurk.fun/introduction), built with Mintlify.
This repository owns the documentation pages and site navigation. The WURK
application, API and client packages live in a separate implementation repository.

## Work with both repositories

Keep independent checkouts next to each other. In the shared development workspace:

```text
/home/runner/workspace/  # WURK implementation
/home/runner/wurk-docs/  # This documentation repository
```

For a new checkout:

```bash
gh repo clone STATIKHEADZ/docs /home/runner/wurk-docs
cd /home/runner/wurk-docs
git switch -c update-agent-docs
```

When the checkout already exists, inspect its branch and changes first:

```bash
git -C /home/runner/wurk-docs status --short --branch
git -C /home/runner/wurk-docs remote get-url origin
```

Continue unfinished work on its existing branch. To start a new update from a clean
checkout after previous work is committed:

```bash
cd /home/runner/wurk-docs
git fetch origin
git switch main
git pull --ff-only origin main
git switch -c docs/describe-the-update
```

Run documentation Git commands in this checkout. Do not change the implementation
repository's remote, pull this repository into it, or copy either repository's
`.git` or `.replit` into the other. Each checkout retains its own configuration.
An editor can open both folders in one workspace without combining their Git history.

## Check the source before writing

When implementation access is available, start with these paths relative to that
checkout:

| Subject | Source |
| --- | --- |
| Agent overview and current guide inventory | `services/x402/public/skill.md`, `services/x402/shared/skill-documents.json` |
| Public workflow guidance | `services/x402/public/references/`, `services/x402/public/best-practices.md` |
| API behavior and response contracts | Relevant handlers and tests in `services/x402/server/` and `server/` |
| API specification generation | `services/x402/server/openapi_aggregate.ts`, `services/x402/server/x402_openapi.ts` |
| SDK and CLI commands and examples | `packages/wurk-sdk/`, `packages/wurk-cli/` |

Use the guide manifest to discover current references instead of maintaining a
second fixed inventory here. Consult the relevant implementation and tests when a
guide and code disagree; verify release status before changing public instructions.

Source changes, deployed API behavior, published npm packages and documentation
versions can differ. A local package version alone does not prove its current code
has been published. Check release evidence and the installed package's README/help;
exclude explicitly unreleased behavior from instructions for released clients.

Without implementation access, use the [public skill](https://wurkapi.fun/skill.md),
its linked guides and released package documentation. Mark unresolved behavior for
verification instead of guessing. Keep internal plans, credentials, production
diagnostics and private customer data out of this public repository.

## Preview and review

Navigation and site settings are in `docs.json`; page content is in `.mdx` files.
The repository also contains an older `mint.json`; check the actual deployment
configuration before changing or removing it.

Install the official `mint` CLI and run a preview from this repository:

```bash
npm install -g mint
cd /home/runner/wurk-docs
mint dev
```

Preview at `http://localhost:3000`. Run `mint validate` after editing site pages or
configuration, check the affected links, and verify examples against the intended
API/client release. See the [Mintlify CLI documentation](https://www.mintlify.com/docs/cli/install).
Documentation examples involving payments are not commands to execute during a docs review.

## Save and publish

Review the diff, commit only the intended documentation files, then push the work
branch to this repository:

```bash
cd /home/runner/wurk-docs
git diff --check
git diff
# Stage the reviewed files and commit them before pushing.
git push -u origin HEAD
```

Open a pull request for review. Describe the changed user flows, release versions
checked, and validation performed. Keep private implementation audit details in the
private project. Confirm the Mintlify GitHub integration and publishing branch before
merging: updates to its configured production branch can publish the site automatically.
Pushing a work branch is separate from publishing production documentation.

Docs publication does not redeploy WURK services or publish SDK/CLI packages.
