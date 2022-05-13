# Reusable GitHub actions

This repository contains GitHub actions that can be reused across projects

## Workflows available:

- [Deploy to Cloud Run](#deploy-to-cloud-run)
- [Remove old container images](#remove-old-containers-images)
- [Conventional commit lint PR](#conventional-commit-lint-pr)

## Deploy to Cloud Run

`.github/workflows/deploy-to-cloud-run.yml` <br>
This workflow will deploy a given container to Cloud Run and clean out the old images from the container registry after successfully deploying.

### Setting up the Google Cloud project

Download the keys as JSON for the compute engine service account that gets created when you create a cloud run service.

Inputs:
| Name | Description | Required |
| ---- | ----------- | -------- |
| container_name | The tag of the built container to deploy | ✅ |
| service_name | The name of the Cloud Run instance | ✅ |
| gcp_project_id | The project ID for the Google Cloud project containing the Cloud Run instance | ✅ |

Secrets:
| Name | Description | Required |
| ---- | ----------- | -------- |
| GCP_SA_KEY | The JSON service account key | ✅ |

## Remove old containers images

`.github/workflows/remove-old-images.yml`
This workflow removes images from the Google Cloud container registry when they meet a specified age criteria.

Inputs:
| Name | Description | Required |
| ---- | ----------- | -------- |
| gcp_project_id | The project ID for the Google Cloud project containing the Cloud Run instance | ✅ |
| image_repo | The name of the image repository to remove images from | ✅ |
| remove_images_keep | How many images should be in the repository at a time | ❌ Defaults to `"10"` |
| remove_images_grace | Don't remove containers that are younger than this time. The format is `<hours>h` | ❌ Defaults to `"336h"` |

Secrets:
| Name | Description | Required |
| ---- | ----------- | -------- |
| GCP_SA_KEY | The JSON service account key | ✅ |

## Conventional commit lint PR

`.github/workflows/conventional-commit-lint-pr.yml`
This workflow lints PRs created with a conventional commit title.

Inputs:
| Name | Description | Required |
| ---- | ----------- | -------- |
| jira_key | The JIRA key to check for when checking the ticket number. Example, `PLAN`. | ✅ |
| require_scope | Require the conventional commit scope to be in the PR title | ❌ Defaults to `false` |
| validate_single_commit | See [https://github.com/amannn/action-semantic-pull-request#configuration](https://github.com/amannn/action-semantic-pull-request#configuration) | ❌ Defaults to `true` |

## Publish to container registry

`.github/workflows/publish-to-container-registry.yml`
This workflow publishes a Docker container to a Google Cloud container registry.

Inputs:
| Name | Description | Required |
| ---- | ----------- | -------- |
| gcp_project_id | The project ID for the Google Cloud project containing the Cloud Run instance | ✅ |
| container_tag | The tag of the built Docker container to publish | ✅ |
| repository_name | The nam eof the container registry repository to publish to | ✅ |
