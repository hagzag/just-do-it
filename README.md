# 🛠️ Tasks & The code behind the posts

[![Lint Code Base](https://github.com/hagzag/just-do-it/actions/workflows/super-linter.yml/badge.svg)](https://github.com/hagzag/just-do-it/actions/workflows/super-linter.yml)

This repository was setup to centralize code examples I mention in different blog posts,  
this is part of my attempt to manage all these snippets / samples in once place.

- 🌐 The 1st contribution to this repository was for the post involving `external-dns` - some finishes in the making ;)
- 🚀 The 2nd was the [k3d-intro](./config/tasks/suites/k3d-playground/README.md) is still WIP, it's code was quite useful to me for quite a while ...
  
I hope to to continue maintaining this and making this a table of features.

## 📖 Using these tasks / `Taskfile.yml` Documentation

### 🎯 Overview

This `Taskfile.yml` configures task automation for various components related to Kubernetes, DNS configurations, and deployment of several applications and services. It integrates environment settings and modular task files from different repository paths.

### ⚙️ Environment Configuration

- **Dotenv**: Loads environment variables from `.env` see `.env-example` which if frequently updated

### 📁 Included Task Files

The project is organized into three main categories:

1. **🔧 Utils** (`./config/tasks/utils.yaml`):
   - Helm operations
   - Templates
   - Testing utilities
   - Common tools

2. **📱 Apps** (`./config/tasks/apps.yml`):
   - 🔐 Configuration management (sealed-secrets)
   - 🔄 Cluster utilities (reloader, descheduler, reflector)
   - 🌐 Ingress (ingress-nginx)
   - 🚢 GitOps tools (argocd)
   - 🔄 CI/CD tools
   - 📦 Package management (chartmeusem)
   - 🎮 Demo applications (whoami)
   - ⚡ Workflow engines (argo-workflows)
   - 💾 Storage solutions (minio)

3. **🎁 Suites** (`./config/tasks/suites.yml`):
   - 🔑 AWS SSO integration
   - 🏗️ Infrastructure as Code
   - 🎮 K3d playground
   - ✅ Production readiness tools
   - 🔄 Git workflows
   - 🌐 CoreDNS configuration
   - 🔍 Pre-commit hooks
   - 🔒 Vault and External Secrets
   - 🎯 AWX deployment
   - ⚖️ Scaling (Goldilocks)
   - 🛡️ Policy management (Gatekeeper)

## 📋 All commands

<details>
<summary>🔍 Click to expand task list</summary>

```sh
# task --list-all
task: Available tasks for this project:
[... original task list content ...]
```

</details>

## 🔍 pre-commit config

- see [pre-commit config](./config/tasks/suites/pre-commit/README.md)


## Using Vscode and go-tak extention

![vscode-go-task](https://i.imgur.com/ZJn0EO5.png)

## Also built on gitlab.tikalk.dev before release here
> this icon may be broken for those with no access to this server ...
[![pipeline status](https://gitlab.tikalk.dev/tikalk/users/hagzag/code-samples/badges/main/pipeline.svg)](https://gitlab.tikalk.dev/tikalk/users/hagzag/code-samples/-/commits/main)
