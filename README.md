# Policy as Code

This repository contains a demonstration of GitHub policy as code using [github/safe-settings](https://github.com/github/safe-settings).

Instead of being hosted in the [Elastic organization](https://github.com/elastic) it is instead hosted in a sample organization called
[elastic-robots](https://github.com/elastic-robots) which has been specifically designated for testing and demos. 

This organization contains an imaginary set of repos whose names correspond to popular projects in the Elastic organization for the purposes
of demonstrating safe-settings.
> [!IMPORTANT]
> These repos are only named in a similar way to the actual repos in the Elastic org. They are not forks and do not contain the same code nor the same settings.

In the root of each repo is a README.md file which describes the role of the repo.

## Organization security model

In this demo, we imagine three roles for policy makers:

1. **Org Admins** are individuals and teams who have the rights to set policy for the entire organization where individuals
who are not a member of this group have no capability to override.
2. **Sub-org Admins** are individuals and teams who have rights to set policy for a given set of repoistories. Any policy they
set which contradicts a policy set at the organizational level will be ignored.
3. **Repo Admins** are individuals and teams who have rights to set policy for a given repository. Any policy they set which
contradicts a policy set by either an org or sub-org will be ignored.

In this repository, we implement the above via the following:

|Role|Via team|
|----|--------|
|1. Org Admins|[@elastic-robots/core](https://github.com/orgs/elastic-robots/teams/core)|
|2. Sub-org Admins|[@apm-agents-lead](https://github.com/orgs/elastic-robots/teams/apm-agents-lead)|
|3. Repo Admins|[@elastic-robots/apm-agent-ruby](https://github.com/orgs/elastic-robots/teams/apm-agent-ruby), [@elastic-robots/apm-agent-php](https://github.com/orgs/elastic-robots/teams/apm-agent-php)|

### Access Controls

Access control is managed via a [CODEOWNERS file](.github/CODEOWNERS) and is enforced via branch protection
rules which prohibit changes from being pushed without compliance with those controls.

The branch protection rules implemented on the `main` branch of this repo are as follows:

|Rule|Status|Details|
|----|:----:|-------|
|Require a pull request before merging |✅||
|Require approvals|✅|2 reviews required|
|Dismiss stale pull request approvals when new commits are pushed|❌||
|Require review from Code Owners|✅||
|Restrict who can dismiss pull request reviews |❌||
|Allow specified actors to bypass required pull requests |❌||
|Require approval of the most recent reviewable push|❌||
|Require status checks to pass before merging|✅|Required checks: `Safe setting validator`|
|Require branches to be up to date before merging|✅||
|Require conversation resolution before merging |❌||
|Require signed commits |❌||
|Require linear history |❌||
|Require merge queue |❌||
|Require deployments to succeed before merging |❌||
|Lock branch|❌||
|Do not allow bypassing the above settings |❌||
|Restrict who can push to matching branches |❌||
|Allow force pushes|❌||
|Allow deletions |❌||

### .github folder

#### CODEOWNERS

Implements controls described in [Access Controls](#Access-Controls)

#### .github/settings.yml

This file implements controls which apply to the entire organization which may be manipulated only by [Org Admins](#organization-design)[1].

> [!IMPORTANT]
> Settings declared in this file apply to the entire organization but individual repositories [can be excluded](https://github.com/github/safe-settings#restricting-safe-settings-to-specific-repos) through configuration present in this file.

#### .github/repos

Specific implementation for any repository, it should match the name of the repository and use the `.yml` ext

Every single repository should have a team assigned in the CODEOWNERS

#### .github/suborgs

Group of repositories that share the same configuration, it should use the `.yml` ext.

Every group should have a team assigned in the CODEOWNERS
