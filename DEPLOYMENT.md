# Deployment

## Release Please

When you push changes to any action to the `main` branch the release please action will add your commit to the changelog. Once you merge the release PR it will do a deployment. There is no real deployment for the actions, rather the release please action will tag the commit with a semantic version string. You can then use this to lock the version of the action you're using. For example, a project might use the link PR action like:

```yml
jobs:
  lint-pr:
    uses: PlaidypusDev/github-actions/.github/workflows/conventional-commit-lint-pr.yml@v1.0.0 # Note the version string from the tagged commit
    with:
      jira_key: WGC
```
