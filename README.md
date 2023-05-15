# Policy as Code

GitHub policy as code using [github/safe-settings](https://github.com/github/safe-settings)

### .github folder

#### CODEOWNERS

This is one of the core features so we can warranty who has the ultimate voice to merge any Pull Requests

#### .github/settings.yml

Unused

#### .github/repos

Specific implementation for any repository, it should match the name of the repository and use the `.yml` ext

Every single repository should have a team assigned in the CODEOWNERS

#### .github/suborgs

Group of repositories that share the same configuration, it should use the `.yml` ext.

Every group should have a team assigned in the CODEOWNERS
