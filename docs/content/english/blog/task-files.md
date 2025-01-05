---
title: "Doing literally anything with go-task and why should ya?"
meta_title:
description:
date: 2024-01-02T05:00:00Z
image: "https://external-preview.redd.it/YDjOdYp0-Kecn8nQUIu6brlJR5aI3URdikvQljcIBzo.jpg?width=640&crop=smart&auto=webp&s=ba6397b95542e1026912e6679717b728de550869"
categories: ["Developer Experience (DevEx)"]
author: "Haggai Philip Zagury (hagzag)"
tags: ["dotfiles", "config", "DevEx", "Tools"]
draft: false
---


This is a common approach I adopted to manage tasks

I have a private one meintaine in house at my company Tikal and a public one in github - here is the link to the public one: [hagzag/dotfiles](https://github.com/hagzag/just-do-it)

{{< notice "info" >}}
So a good place to start is the code which is available at [hagzag/just-do-it](https://github.com/hagzag/just-do-it)
{{< /notice >}}

The following is basically the repo's README.md file which I maintain as I improove it.

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
* argo-workflows:                                                    Run the argo-workflows project
* argocd:                                                            Deploy argocd project
* chartmeusem:                                                       Run the chartmeusem project
* config-managment:                                                  Run all config-managment tasks
* coredns:                                                           Run the codedns project
* default:                                                           Debug the environment
* goldilocks-minimal:                                                Run the goldilocks project
* help:                                                              Show help
* ingress-nginx:                                                     Deploy nginx project
* opa-gatekeeper:                                                    Run the opa-gatekeeper project
* opa-gatekeeper-demo:                                               Run the opa-gatekeeper project
* opa-gatekeeper-demo-cleanup:                                       Cleanup the opa-gatekeeper project
* run-tests:                                                         Run tests
* sealed-secrets:                                                    Run all sealed-secrets tasks
* app:argo-workflows:apply:                                          
* app:argo-workflows:create-values:                                  
* app:argo-workflows:create-wrapper-chart:                           
* app:argo-workflows:delete-argocd-app:                              
* app:argo-workflows:dryrun:                                         
* app:argo-workflows:full-run:                                       
* app:argo-workflows:helm:create-wrapper-chart:                      
* app:argo-workflows:helm:dependency_build:                          Run Helm dependency build for 
* app:argo-workflows:helm:install:                                   Install Helm chart for  in monitoring namespace
* app:argo-workflows:helm:repo_add:                                  Add and update Helm repo: $1 -> 
* app:argo-workflows:helm:template:                                  Apply Helm template for  in $1 namespace
* app:argo-workflows:helm:template_apply:                            Apply Helm template for  in  namespace
* app:argo-workflows:helm:template_apply_dry_run:                    Apply Helm template for  in  namespace
* app:argo-workflows:helm:template_delete:                           Apply Helm template for  in  namespace
* app:argo-workflows:install:                                        
* app:argo-workflows:install-argocd-app:                             Installs nginx as argocCD application
* app:argo-workflows:install-dev:                                    
* app:argocd:bridge:                                                 
* app:argocd:create-argo-helm-app:                                   Create argo app for reloader
* app:argocd:install:                                                Installs ArgoCD resources manually on the local cluster
* app:argocd:password:                                               
* app:argocd:repo:                                                   
* app:argocd:rm:                                                     
* app:argocd:secret:                                                 
* app:chartmeusem:install-argo-app:                                  Installs nginx resources manually on the local cluster
* app:chartmeusem:rm:                                                
* app:chartmeusem:tweak-chartmeusem-test:                            Tear down the chartmeusem chart
* app:descheduler:apply:                                             
* app:descheduler:create-values:                                     
* app:descheduler:create-wrapper-chart:                              
* app:descheduler:dryrun:                                            
* app:descheduler:full-run:                                          
* app:descheduler:helm:create-wrapper-chart:                         
* app:descheduler:helm:dependency_build:                             Run Helm dependency build for 
* app:descheduler:helm:install:                                      Install Helm chart for  in monitoring namespace
* app:descheduler:helm:repo_add:                                     Add and update Helm repo: $1 -> 
* app:descheduler:helm:template:                                     Apply Helm template for  in $1 namespace
* app:descheduler:helm:template_apply:                               Apply Helm template for  in  namespace
* app:descheduler:helm:template_apply_dry_run:                       Apply Helm template for  in  namespace
* app:descheduler:helm:template_delete:                              Apply Helm template for  in  namespace
* app:descheduler:install:                                           
* app:descheduler:install-dev:                                       
* app:descheduler:test-controller:                                   
* app:ingress-nginx:apply:                                           
* app:ingress-nginx:create-values:                                   
* app:ingress-nginx:create-wrapper-chart:                            
* app:ingress-nginx:delete-argocd-app:                               
* app:ingress-nginx:dryrun:                                          
* app:ingress-nginx:full-run:                                        
* app:ingress-nginx:helm:create-wrapper-chart:                       
* app:ingress-nginx:helm:dependency_build:                           Run Helm dependency build for 
* app:ingress-nginx:helm:install:                                    Install Helm chart for  in monitoring namespace
* app:ingress-nginx:helm:repo_add:                                   Add and update Helm repo: $1 -> 
* app:ingress-nginx:helm:template:                                   Apply Helm template for  in $1 namespace
* app:ingress-nginx:helm:template_apply:                             Apply Helm template for  in  namespace
* app:ingress-nginx:helm:template_apply_dry_run:                     Apply Helm template for  in  namespace
* app:ingress-nginx:helm:template_delete:                            Apply Helm template for  in  namespace
* app:ingress-nginx:install:                                         
* app:ingress-nginx:install-argocd-app:                              Installs nginx as argocCD application
* app:ingress-nginx:install-dev:                                     
* app:minio:add_additional_templates:                                Add additional templates for ./config/apps/minio in minio namespace
* app:minio:apply:                                                   
* app:minio:argocd-app:                                              Create argo app for reloader
* app:minio:argocd:bridge:                                           
* app:minio:argocd:create-argo-helm-app:                             Create argo app for reloader
* app:minio:argocd:install:                                          Installs ArgoCD resources manually on the local cluster
* app:minio:argocd:password:                                         
* app:minio:argocd:repo:                                             
* app:minio:argocd:rm:                                               
* app:minio:argocd:secret:                                           
* app:minio:create-argo-helm-app:                                    Create argo app for reloader
* app:minio:create-values:                                           
* app:minio:create-wrapper-chart:                                    
* app:minio:delete-argocd-app:                                       
* app:minio:dryrun:                                                  
* app:minio:full-run:                                                
* app:minio:helm:create-wrapper-chart:                               
* app:minio:helm:dependency_build:                                   Run Helm dependency build for 
* app:minio:helm:install:                                            Install Helm chart for  in monitoring namespace
* app:minio:helm:repo_add:                                           Add and update Helm repo: $1 -> 
* app:minio:helm:template:                                           Apply Helm template for  in $1 namespace
* app:minio:helm:template_apply:                                     Apply Helm template for  in  namespace
* app:minio:helm:template_apply_dry_run:                             Apply Helm template for  in  namespace
* app:minio:helm:template_delete:                                    Apply Helm template for  in  namespace
* app:minio:install:                                                 
* app:minio:install-argocd-app:                                      Installs nginx as argocCD application
* app:minio:install-dev:                                             
* app:reflector:apply:                                               
* app:reflector:create-values:                                       
* app:reflector:create-wrapper-chart:                                
* app:reflector:dryrun:                                              
* app:reflector:full-run:                                            
* app:reflector:helm:create-wrapper-chart:                           
* app:reflector:helm:dependency_build:                               Run Helm dependency build for 
* app:reflector:helm:install:                                        Install Helm chart for  in monitoring namespace
* app:reflector:helm:repo_add:                                       Add and update Helm repo: $1 -> 
* app:reflector:helm:template:                                       Apply Helm template for  in $1 namespace
* app:reflector:helm:template_apply:                                 Apply Helm template for  in  namespace
* app:reflector:helm:template_apply_dry_run:                         Apply Helm template for  in  namespace
* app:reflector:helm:template_delete:                                Apply Helm template for  in  namespace
* app:reflector:install:                                             
* app:reflector:install-dev:                                         
* app:reflector:test-controller:                                     
* app:reloader:apply:                                                
* app:reloader:create-values:                                        
* app:reloader:create-wrapper-chart:                                 
* app:reloader:dryrun:                                               
* app:reloader:full-run:                                             
* app:reloader:helm:create-wrapper-chart:                            
* app:reloader:helm:dependency_build:                                Run Helm dependency build for 
* app:reloader:helm:install:                                         Install Helm chart for  in monitoring namespace
* app:reloader:helm:repo_add:                                        Add and update Helm repo: $1 -> 
* app:reloader:helm:template:                                        Apply Helm template for  in $1 namespace
* app:reloader:helm:template_apply:                                  Apply Helm template for  in  namespace
* app:reloader:helm:template_apply_dry_run:                          Apply Helm template for  in  namespace
* app:reloader:helm:template_delete:                                 Apply Helm template for  in  namespace
* app:reloader:install:                                              
* app:reloader:install-dev:                                          
* app:reloader:test-controller:                                      
* app:sealed-secrets:create-private-key:                             Create a private key
* app:sealed-secrets:helm:create-wrapper-chart:                      
* app:sealed-secrets:helm:dependency_build:                          Run Helm dependency build for 
* app:sealed-secrets:helm:install:                                   Install Helm chart for  in monitoring namespace
* app:sealed-secrets:helm:repo_add:                                  Add and update Helm repo: $1 -> 
* app:sealed-secrets:helm:template:                                  Apply Helm template for  in $1 namespace
* app:sealed-secrets:helm:template_apply:                            Apply Helm template for  in  namespace
* app:sealed-secrets:helm:template_apply_dry_run:                    Apply Helm template for  in  namespace
* app:sealed-secrets:helm:template_delete:                           Apply Helm template for  in  namespace
* app:sealed-secrets:install-kubeseal:                               Install kubeseal
* app:sealed-secrets:local-apply:                                    
* app:sealed-secrets:local-dryrun:                                   
* app:sealed-secrets:test-sealed-secret:                             Create a sealed secret
* app:whoami:apply:                                                  
* app:whoami:create-values:                                          
* app:whoami:create-wrapper-chart:                                   
* app:whoami:delete-argocd-app:                                      
* app:whoami:dryrun:                                                 
* app:whoami:full-run:                                               
* app:whoami:helm:create-wrapper-chart:                              
* app:whoami:helm:dependency_build:                                  Run Helm dependency build for 
* app:whoami:helm:install:                                           Install Helm chart for  in monitoring namespace
* app:whoami:helm:repo_add:                                          Add and update Helm repo: $1 -> 
* app:whoami:helm:template:                                          Apply Helm template for  in $1 namespace
* app:whoami:helm:template_apply:                                    Apply Helm template for  in  namespace
* app:whoami:helm:template_apply_dry_run:                            Apply Helm template for  in  namespace
* app:whoami:helm:template_delete:                                   Apply Helm template for  in  namespace
* app:whoami:install:                                                
* app:whoami:install-argocd-app:                                     Installs nginx as argocCD application
* app:whoami:install-dev:                                            
* chartmeusem:cleanup:                                               Run the chartmeusem project
* external-dns:eks:demo:                                             Run the external-dns project
* external-dns:eks:demo:cleanup:                                     Cleanup the external-dns project
* k3d:cluster:create:                                                Start the k3d cluster
* k3d:cluster:delete:                                                Destroy the k3d cluster
* suite:aws-sso:create-profile:                                      Create an AWS SSO profile
* suite:aws-sso:relogin:                                             Validate the session
* suite:aws-sso:status:                                              Get the STS status
* suite:awx:awx-cli-login:                                           
* suite:awx:create-argo-apps:                                        
* suite:awx:get-awx-admin-password:                                  
* suite:awx:install:                                                 
* suite:awx:run-ansible-k8s-exmaple:                                 Run the ansible k8s example
* suite:awx:run-awx-playbook:                                        
* suite:awx:secret:                                                  
* suite:awx:uninstall:                                               
* suite:coredns:dns-test:                                            
* suite:gatekeeper-pm:apply:                                         
* suite:gatekeeper-pm:create-values:                                 
* suite:gatekeeper-pm:create-wrapper-chart:                          
* suite:gatekeeper-pm:dryrun:                                        
* suite:gatekeeper-pm:full-run:                                      
* suite:gatekeeper-pm:helm:create-wrapper-chart:                     
* suite:gatekeeper-pm:helm:dependency_build:                         Run Helm dependency build for 
* suite:gatekeeper-pm:helm:install:                                  Install Helm chart for  in monitoring namespace
* suite:gatekeeper-pm:helm:repo_add:                                 Add and update Helm repo: $1 -> 
* suite:gatekeeper-pm:helm:template:                                 Apply Helm template for  in $1 namespace
* suite:gatekeeper-pm:helm:template_apply:                           Apply Helm template for  in  namespace
* suite:gatekeeper-pm:helm:template_apply_dry_run:                   Apply Helm template for  in  namespace
* suite:gatekeeper-pm:helm:template_delete:                          Apply Helm template for  in  namespace
* suite:gatekeeper-pm:install:                                       
* suite:gatekeeper-pm:install-dev:                                   
* suite:gatekeeper:apply:                                            
* suite:gatekeeper:create-constraint:                                
* suite:gatekeeper:create-constraint-teample:                        
* suite:gatekeeper:create-values:                                    
* suite:gatekeeper:create-wrapper-chart:                             
* suite:gatekeeper:delete-constraint:                                
* suite:gatekeeper:delete-constraint-template:                       
* suite:gatekeeper:dryrun:                                           
* suite:gatekeeper:full-run:                                         
* suite:gatekeeper:helm:create-wrapper-chart:                        
* suite:gatekeeper:helm:dependency_build:                            Run Helm dependency build for 
* suite:gatekeeper:helm:install:                                     Install Helm chart for  in monitoring namespace
* suite:gatekeeper:helm:repo_add:                                    Add and update Helm repo: $1 -> 
* suite:gatekeeper:helm:template:                                    Apply Helm template for  in $1 namespace
* suite:gatekeeper:helm:template_apply:                              Apply Helm template for  in  namespace
* suite:gatekeeper:helm:template_apply_dry_run:                      Apply Helm template for  in  namespace
* suite:gatekeeper:helm:template_delete:                             Apply Helm template for  in  namespace
* suite:gatekeeper:install:                                          
* suite:gatekeeper:install-dev:                                      
* suite:gatekeeper:test-constraint-expect-failure:                   
* suite:gatekeeper:test-constraint-expect-success:                   
* suite:git-workflow:add-changes-to-pr-brnach:                       Open a PR with the name as input
* suite:git-workflow:commit-changes-to-local-feature-brnach:         Commit changes to pr branch
* suite:git-workflow:merge-feature-branch-into-default-branch:       Merge PR
* suite:git-workflow:open-pr-with-name-as-input:                     Open a PR with the name as input
* suite:git-workflow:push-pr-branch-changes-to-default-remote:       Push changes to pr branch
* suite:git-workflow:reset:soft:                                     Reset the workflow
* suite:git-workflow:workflow:close:                                 Continue the workflow
* suite:git-workflow:workflow:continue:                              Continue the workflow
* suite:git-workflow:workflow:init:                                  Run the workflow
* suite:git-workflow:workflow:publish:                               Continue the workflow
* suite:git-workflow:workflow:reset:                                 Reset the workflow
* suite:git:commit:am:                                               Run the workflow
* suite:goldilocks:apply:                                            
* suite:goldilocks:create-values:                                    
* suite:goldilocks:create-wrapper-chart:                             
* suite:goldilocks:dryrun:                                           
* suite:goldilocks:full-run:                                         
* suite:goldilocks:helm:create-wrapper-chart:                        
* suite:goldilocks:helm:dependency_build:                            Run Helm dependency build for 
* suite:goldilocks:helm:install:                                     Install Helm chart for  in monitoring namespace
* suite:goldilocks:helm:repo_add:                                    Add and update Helm repo: $1 -> 
* suite:goldilocks:helm:template:                                    Apply Helm template for  in $1 namespace
* suite:goldilocks:helm:template_apply:                              Apply Helm template for  in  namespace
* suite:goldilocks:helm:template_apply_dry_run:                      Apply Helm template for  in  namespace
* suite:goldilocks:helm:template_delete:                             Apply Helm template for  in  namespace
* suite:goldilocks:install:                                          
* suite:goldilocks:install-dev:                                      
* suite:iac:tf-aws-example:                                          Run the AWS example
* suite:iac:tf-aws-example-destroy:                                  Run the AWS example
* suite:iac:tg-aws-example:                                          Run the AWS example
* suite:iac:tg-aws-example-destroy:                                  Run the AWS example
* suite:k3d:certs:                                                   Creates and uploads local certificates to the cluster as tls secrets
* suite:k3d:cluster-create:                                          Starts a local k3d cluster.
* suite:k3d:cluster-template:                                        Create a k3d cluster template
* suite:k3d:delete-cluster:                                          
* suite:k3d:dns:                                                     Creates the DNS entry required for the local domain to work.
* suite:k3d:hosts-file:                                              Adds a line to the hosts file if it doesn't already exist.
* suite:k3d:ns:system:                                               
* suite:pre-commit:1st-run:                                          reset-precommit configration to bare minimal
* suite:pre-commit:gen-default-pre-commit-config:                    create-the-base
* suite:pre-commit:get:                                              internal | exec - install pre-commit via homebrew
* suite:pre-commit:install:                                          internal | configure | pre-commit to local repo
* suite:pre-commit:run:                                              internal | execute | run-all pre-commit run on the staged files (files which are going to be commited)
* suite:pre-commit:run-all-files:                                    internal | execute | run-all pre-commit against all files
* suite:vault:cleanup:all:                                           Installs vault + eso resources manually on the local cluster
* suite:vault:demo:vault-eso:install:                                Installs vault + eso resources manually on the local cluster
* suite:vault:demo:vault-eso:uninstall:                              Uninstalls vault + eso resources from the local cluster
* suite:vault:deploy:all:                                            Installs vault + eso resources manually on the local cluster
* suite:vault:install:                                               Installs vault + eso resources manually on the local cluster
* suite:vault:install:eso:                                           Installs vault + eso resources manually on the local cluster
* suite:vault:test-result:                                           
* suite:vault:uninstall:                                             Uninstalls vault + eso resources from the local cluster
* suite:vault:uninstall:eso:                                         Uninstalls eso resources from the local cluster
* utils:helm:create-wrapper-chart:                                   
* utils:helm:dependency_build:                                       Run Helm dependency build for 
* utils:helm:install:                                                Install Helm chart for  in monitoring namespace
* utils:helm:repo_add:                                               Add and update Helm repo: $1 -> 
* utils:helm:template:                                               Apply Helm template for  in $1 namespace
* utils:helm:template_apply:                                         Apply Helm template for  in  namespace
* utils:helm:template_apply_dry_run:                                 Apply Helm template for  in  namespace
* utils:helm:template_delete:                                        Apply Helm template for  in  namespace
* utils:hugo:dependency_build:                                       Install Hugo dependencies
* utils:hugo:run-dev:                                                Run Hugo in development mode
* utils:templates:argocd:                                            
* utils:templates:certificate:                                       
* utils:templates:chartmeusem:                                       
* utils:templates:example:                                           
* utils:templates:gen:                                               
* utils:test:helm-wrapper:                                           
* utils:test:helm:create-wrapper-chart:                              
* utils:test:helm:dependency_build:                                  Run Helm dependency build for 
* utils:test:helm:install:                                           Install Helm chart for  in monitoring namespace
* utils:test:helm:repo_add:                                          Add and update Helm repo: $1 -> 
* utils:test:helm:template:                                          Apply Helm template for  in $1 namespace
* utils:test:helm:template_apply:                                    Apply Helm template for  in  namespace
* utils:test:helm:template_apply_dry_run:                            Apply Helm template for  in  namespace
* utils:test:helm:template_delete:                                   Apply Helm template for  in  namespace
* utils:tools:asdf:                                                  
* utils:tools:asdf:nodejs:                                           
* utils:tools:asdf:nodejs:latest:                                    
* utils:tools:aws-cli:                                               
* utils:tools:aws-vault:                                             
* utils:tools:google-cloud-sdk:                                      
* utils:tools:hostctl:                                               
* utils:tools:install:                                               
* utils:tools:jq:                                                    
* utils:tools:k3d:                                                   
* utils:tools:kubectl:                                               
* utils:tools:kustomize:                                             
* utils:tools:mkcert:                                                
* utils:tools:python3.11:                                            
* utils:tools:python3.12:                                            
* utils:tools:python3.13:                                            
* utils:tools:set:aws:                                               
* utils:tools:set:gcp:                                               
* utils:tools:set:k8s:                                               
* utils:tools:set:nodejs:                                            
* utils:tools:set:python:                                            
* utils:tools:set:system:                                            
* utils:tools:vault:                                                 
* utils:utils:create-vscode-config:                                  creates a .vscode/settings.json
* utils:utils:docker-pull-images:                                    
* utils:utils:images-list:                                           
* utils:utils:k3d-import-images:                                     
* utils:utils:super-linter:                                          

```

</details>

## 🔍 pre-commit config

- see [pre-commit config](./config/tasks/suites/pre-commit/README.md)


## Using Vscode and go-task extention

![vscode-go-task](https://i.imgur.com/ZJn0EO5.png)
