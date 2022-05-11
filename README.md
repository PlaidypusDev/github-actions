# Reusable GitHub actions

This repository contains GitHub actions that can be reused across projects

## Workflows available:

- [Deploy to Cloud Run](#deploy-to-cloud-run)

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
