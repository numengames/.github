<!--
SPDX-FileCopyrightText: 2026 Numen Games S.L.
SPDX-License-Identifier: CC0-1.0
-->

# numengames/.github

The one home of what every Numen Games repository shares on GitHub. **Change it here; never copy it into a repository.** The rule and its reasons are in the archive's decision on how the house's repositories are organised, at [numinia.org](https://numinia.org).

## What lives here

| File | What it is | How a repository uses it |
|---|---|---|
| `PULL_REQUEST_TEMPLATE.md` | The house pull request template | GitHub applies it to every repository of the organisation that has no template of its own. Repositories do not keep a copy. |
| `.github/workflows/secrets.yml` | Full-history secret scan (gitleaks) | Called by a short workflow in each repository |
| `.github/workflows/workflow-lint.yml` | actionlint + zizmor over the repository's workflows | Called |
| `.github/workflows/audit.yml` | Production dependency audit, npm or pnpm | Called, with the lockfile's directory |
| `.github/workflows/monitor.yml` | The night watch of a live site | Called on a schedule, with the site and its probes |
| `.github/workflows/dependabot-auto-merge.yml` | Dependabot PRs merge themselves when CI is green | Called on `pull_request` |

Each file says, at its top, exactly how to call it. A repository keeps a workflow of its own only when the job belongs to it: its build, its deploy.

## How a change reaches the repositories

1. Change the shared workflow here, in a pull request. `self-check.yml` runs the secret scan and the workflow lint on this repository first.
2. After the merge, each calling repository moves its pin (`@<commit-sha>`) to the new commit, in its own pull request. Pins are by commit, never by branch, so no repository changes behaviour without a reviewed change of its own.

## Licence

Workflows: MIT (see `LICENSE`). This README and the pull request template: CC0-1.0, as the SPDX line in each file says.
