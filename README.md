# Reusable GitHub actions

This repository contains [reusable GitHub actions](https://docs.github.com/en/actions/using-workflows/reusing-workflows) that can be reused across projects

## Links

- Reusable workflow documentation: https://docs.github.com/en/actions/using-workflows/reusing-workflows
- Inputs and secrets in reusable workflow: https://docs.github.com/en/actions/using-workflows/reusing-workflows#using-inputs-and-secrets-in-a-reusable-workflow
- Outputs for reusable workflows: https://docs.github.com/en/actions/using-workflows/reusing-workflows#using-outputs-from-a-reusable-workflow

## Workflows available:

- [Conventional commit lint PR](#conventional-commit-lint-pr)
- [Deploy to Cloud Run](#deploy-to-cloud-run)
- [Remove old container images](#remove-old-containers-images)
- [Publish to container registry](#publish-to-container-registry)

## Conventional commit lint PR

[`conventional-commit-lint-pr.yml`](.github/workflows/conventional-commit-lint-pr.yml)

This workflow lints PRs created with a conventional commit title. When using the "squash and merge" strategy, make sure to configure the repository to use the setting: [Default to PR title for squash merge commits](https://github.blog/changelog/2022-05-11-default-to-pr-titles-for-squash-merge-commit-messages/). For context, please read [this section](https://github.com/marketplace/actions/semantic-pull-request#legacy-configuration) of the `semantic-pull-request` action documentation.

Inputs:
| Name | Description | Required | Default |
| ---- | ----------- | :------: | ------- |
| jira_key | The JIRA key to check for when checking the ticket number. Example, `PLAN`. | ✅ | `N/A` |
| require_scope | Require the conventional commit scope to be in the PR title | ❌ | `false` |

## Deploy to Cloud Run

[`deploy-to-cloud-run.yml`](.github/workflows/deploy-to-cloud-run.yml)

This workflow will deploy a given container to Cloud Run and clean out the old images from the container registry after successfully deploying.

### Setting up the Google Cloud project

Download the keys as JSON for the compute engine service account that gets created when you create a cloud run service.

Inputs:
| Name | Description | Required |
| ---- | ----------- | :------: |
| container_name | The tag of the built container to deploy | ✅ |
| service_name | The name of the Cloud Run instance | ✅ |
| gcp_project_id | The project ID for the Google Cloud project containing the Cloud Run instance | ✅ |

Secrets:
| Name | Description | Required |
| ---- | ----------- | :------: |
| GCP_SA_KEY | The JSON service account key | ✅ |

## Remove old container images

[`remove-old-images.yml`](.github/workflows/remove-old-images.yml)

This workflow removes images from the Google Cloud container registry when they meet a specified age criteria.

Inputs:
| Name | Description | Required | Default |
| ---- | ----------- | :------: | ------- |
| gcp_project_id | The project ID for the Google Cloud project containing the Cloud Run instance | ✅ | `N/A` |
| image_repo | The name of the image repository to remove images from | ✅ | `N/A` |
| tag_filter_regex | Only images with at least one tag that matches this given regular expression will be deleted | ❌ | `".*"` |
| remove_images_keep | How many images should be in the repository at a time | ❌ | `"10"` |
| remove_images_grace | Don't remove containers that are younger than this time. The format is `<hours>h` | ❌ | `"336h"` |

Secrets:
| Name | Description | Required |
| ---- | ----------- | :------: |
| GCP_SA_KEY | The JSON service account key | ✅ |

## Publish to container registry

[`publish-to-container-registry.yml`](.github/workflows/publish-to-container-registry.yml)

This workflow publishes a Docker container to a Google Cloud container registry.

Inputs:
| Name | Description | Required |
| ---- | ----------- | :------: |
| gcp_project_id | The project ID for the Google Cloud project containing the Cloud Run instance | ✅ |
| container_tag | The tag of the built Docker container to publish | ✅ |
| repository_name | The nam eof the container registry repository to publish to | ✅ |
