# Crossplane AWS S3 Setup

This directory contains Taskfile-based automation for setting up Crossplane with AWS S3 provider and creating S3 buckets.

## Prerequisites

- A Kubernetes cluster
- go-task CLI installed
- kubectl configured against the cluster
- Temoporary AWS credentials (access key, secret key, and session token) 
  A Less secure Alternative: AWS credentials file (access key, secret key)
- Helm 3 installed

## Configuration

The following variables are configured in the Taskfile:
if you wish to use a different version of Crossplane, you can change the `cp_controller_chart_version` variable.

```
cp_controller_name: crossplane
cp_controller_namespace: crossplane-system
cp_controller_repo: https://charts.crossplane.io/stable
cp_controller_chart_version: 1.18.2
```

## Available Tasks

### Installation Tasks

- `install-dev`: Installs Crossplane in development mode with ArgoCD context
- `install`: Standard Crossplane installation
- `full-run`: Complete setup including provider and S3 bucket creation

### Helm Chart Management

- `create-wrapper-chart`: Creates a Helm wrapper chart for Crossplane
- `create-values`: Generates the values file for the Helm chart
- `dryrun`: Performs a dry run of the Helm installation
- `apply`: Applies the Helm chart to the cluster

### AWS Provider Setup

- `create-cloud-credentials-from-envvars`: Creates AWS credentials from environment variables
  - Requires: AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_SESSION_TOKEN
- `create-credentials-secret`: Creates a Kubernetes secret with AWS credentials
- `providerconfig-provider-aws-s3`: Installs and configures the AWS S3 provider

### Resource Management

- `create-resource-aws-s3`: Creates an S3 bucket using Crossplane
- `resource-cleanup`: Cleans up all created resources in the following order:
  1. S3 bucket
  2. Provider configuration
  3. AWS S3 provider
  4. AWS credentials secret

## Full Run

This task will install Crossplane, create a Helm wrapper chart, install the AWS S3 provider, create an S3 bucket.

```
task full-run
```

## Step by Step 

```yaml
  full-run:
    cmds:
      - task: create-wrapper-chart
      - task: create-values
      - task: dryrun
      - task: apply
```

# For aws s3 demo

```bash
task aws:all
```

# For gcp s3 demo

```bash
task gcp:all
```

### AWS standard environment variables

The following environment variables are required:
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_SESSION_TOKEN`
- `AWS_REGION` defaults to "eu-west-1"

### GCP standard environment variables

The following environment variables are required:
- `GCP_CREDENTIALS_JSON`
- `GCP_PROJECT_ID`
- `GCP_REGION` defaults to "EU"

You will also need a service account with the following roles:
- `roles/storage.admin`
- `roles/iam.serviceAccountUser`

On the project level, you need to enable the following APIs:
- `storage-component.googleapis.com`
- `iam.googleapis.com`

## Notes

- In both acenarios bucket is created with a generated name prefix "crossplane-bucket-"
- All resources are created in the `crossplane-system` namespace
- The AWS provider is configured to use the AWS region `eu-west-1` or `EU`
- Provider health is verified before proceeding with resource creation
- Deletion is very strict on the naming conventions in this demo, you need to run the `gcp:resource-cleanup` or `aws:resource-cleanup` tasks to delete all resources, please verify just in case you change the naming conventions provided in this demo scenario.
