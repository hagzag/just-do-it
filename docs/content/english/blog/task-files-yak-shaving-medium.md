---
title: "From yak shaving to mastering tasks"
meta_title:
description:
date: 2024-01-02T05:00:00Z
image: "https://cdn-images-1.medium.com/max/2000/1*BAYflQ9Zt9D_CXWXEXfEJw.png"
categories: ["Medium Publication"]
author: "Haggai Philip Zagury (hagzag)"
tags: ["dotfiles", "config", "DevEx"]
draft: false
---

[Israeli Tech Radar](https://medium.com/israeli-tech-radar/from-yak-shaving-to-mastering-tasks-982b669e05e8) on *medium*.

**TLDR;** This is a quick share of a neat tool which found it’s way into my toolset, it did it in such a significant way which enabled me to combine tools in a common way — something I’ve been missing for quite a while. This is also a thank you to the author’s and contributors of go-task which is such an awesome tool.

## The term **Yak Shaving …

{{< image src="https://cdn-images-1.medium.com/max/2000/1*t3FxgVN-EWq9EB4xEQ3LFQ.png" caption="YakShaving and Procrastination **| DALL.E**" alt="15 f" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}

Do you remember that time ?, That time, when you were trying to do a simple project, but end up doing a bunch of weird, seemingly unrelated tasks first ?

Imagine you wanna do your assignment, but first you gotta ***clean your desk***, but to clean your desk, you gotta find a place for your old project, which lead you to organizing your workspace… and it just keeps going….

In one of the conferences the best analogy was I had to go to buy a hose in order to wash the car ;) … It’s like you set out to ***shave a yak*** instead of just **doing your assignment,** total rabbit hole situation, you know? it’s a phrase for those moments when you’re like, “how did i even end up here?”
> Don’t misplace YakShaving and Procrastination — although yak shaving could help Procrastinators to have another excuse ;) ☯️

## Jar of Life Philosophy

In the realm of DevOps, the complexity of tasks can often seem overwhelming, akin to fitting rocks, pebbles, and sand into a jar, this analogy, known as the **Jar of Life concept**, teaches us the importance of prioritizing larger tasks (the rocks) and fitting smaller ones (pebbles and sand) around them.

However, the real challenge lies in efficiently managing these tasks to maximize productivity. These efficiencies are also known as the Best Practices … something you may want to store centrally let’s say in your platform (something to discuss in a broader context).

For software developers like Chef’s, Carpenters and Other crafts the set or sequence of execution is the “secrets of success” — why not share that with your team ?

{{< image src="https://cdn-images-1.medium.com/max/2000/1*7t2uyTF8MorRQwL-hJSqUA.png" caption="Jar of Life Philosophy in our day2day DevOps **| DALL.E**" alt="15 f" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}

Since the days I was an IT professional (before I could call myself a developer / devops) I was always stumbled upon ***patterns*** like readme.txt which matured into readme.md and of course Makefile as I matured in the configuration management world I learned a thing or two about makefiles and build-systems …

### A “One file to rule them all” approach

{{< image src="https://cdn-images-1.medium.com/max/2000/1*wRwW0rYU-Ok3No3J1ofH7A.png" caption="A “One file to rule them all” approach …" alt="15 f" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}

I had this Makefile which should literally build anything, an example usecase -> setting up an aws profile:

```python
    #!/usr/bin/make -f
    
    # .env
    # AWS_DEFEULT_REGION
    # AWS_REGION
    
    AWS_ACCOUNT_ID  := $(shell aws sts get-caller-identity --profile ${AWS_PROFILE} | jq -r .Account)
    AWS_CURRENT_USER_ARN  := $(shell aws sts get-caller-identity --profile ${AWS_PROFILE} | jq -r .Arn)
    
    aws-req-env: guard-AWS_ACCOUNT_ID \
           guard-AWS_CURRENT_USER_ARN
    
    aws-profile-setup-prompt:
     @aws configure --profile $(AWS_PROFILE)
    
    aws-profile-show:
     @echo "AWS_ACCOUNT_ID is $(AWS_ACCOUNT_ID)"
     @echo "AWS_CURRENT_USER_ARN is $(AWS_CURRENT_USER_ARN)"
     @aws sts get-caller-identity --profile $(AWS_PROFILE)
    
    aws-profile-check: aws-req-env 
     @cat $(HOME)/.aws/credentials | grep "^\[$(AWS_PROFILE)" && \
      echo "$(GREEN)Yore all set$(RESET)" || \
      echo "$(RED) please set your AWS profile - run make _aws_profile-prompt"
     @make aws-profile-show
```

Considering we had many accounts and tools to configure and switch between, this example has a dynamic_variable via shell execution …

```sh
    AWS_ACCOUNT_ID  := $(shell aws sts get-caller-identity --profile ${AWS_PROFILE} | jq -r .Account)
```

I even implemented some utility targets such as the following:
usage example is the guard-AWS_USER_ARN which is really a common task from common.mk which looks like the following (cleaned up for simplicity):

```sh
#!/usr/bin/make -f

BOLD = $(shell tput bold)
RED = $(shell tput setaf 1)
GREEN = $(shell tput setaf 2)
YELLOW = $(shell tput setaf 3)
RESET = $(shell tput sgr0)

DOCKER_COMPOSE     := /usr/local/bin/docker-compose
DOCKER_IMAGE_VERSION := $(shell cat ${CURRENT_FOLDER}/VERSION)

HELM_BIN       := /usr/local/bin/helm

.PHONY        := docker-check guard-%

env-check: ## env-check: common environment checks
  @echo "CURRENT_FOLDER --> $(CURRENT_FOLDER)"
  @echo "VERSION_FILE -----> $(CURRENT_FOLDER)/VERSION"
  @test -f $(HELM_BIN)  || echo "$(RED)$(HELM_BIN) not found$(RESET)" && \
  @echo "Helm Version -----> $(GREEN) `$(HELM_BIN) version --short` $(RESET)"
  @echo "Helm Chart Name --> $(GREEN)$(CHART_NAME)$(GREEN)$(RESET)"
  @echo "Docker Image Name --> $(GREEN)$(DOCKER_IMAGE_NAME)$(GREEN)$(RESET)"
  @echo "Docker Image Version --> $(GREEN)$(DOCKER_IMAGE_VERSION)$(GREEN)$(RESET)"

# https://dev.to/daniel13rady/guarding-makefile-targets-1nb8
guard-%:
  @ if [ "${${*}}" = "" ]; then \
    echo "$(RED)Environment variable $* not set$(CHART_REPO_STABLE)"; \
    exit 1; \
  fi
```

After Makelicious and working with kubectl, terraform and other go based tools and running commands like kubectl apply -k https://some-arbitrary.com/file.yaml … I would like the same “cloud native experience “ in my *task definition* and my ***task execution tools !***

Side-note — Makelicious attempted to serve me in a central Makefile to all my tasks, which worked for 1 customer with 1 cloud-provider with a set of specific requirements … this was before cloud was a thing ;)

[ and we had a well-defined / internal platform — topic for my next post in the series ].

## So, I’m slowly Transitioning to go-task 🤔

**Why**❓**Well**❗

So with this in mind **notwithstanding to our laziness by nature …* I’ve always been looking for a tool I could use for “all my projects” — may the truth be said i’m not there yet …

{{< image src="https://cdn-images-1.medium.com/max/2000/1*EmYaT5vKnlyySV6KilsKJw.png" caption="**go-task**, is a modern task runner / simpler Make alternative written in Go." alt="15 f" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}

DevOps, in A multi-provider reality … especially in my day2day as a DevOps consultant switching providers (/ platforms), I need a consistent way of working if it’s authenticating with my cloud provider or my git provider or my iac provider … if I take authN and authZ related tasks alone — think on how that could execrate my productivity ❗

{{< image src="https://cdn-images-1.medium.com/max/2000/1*nZ8xTnW09i-Tl1xIQzA9LQ.png" caption="Our Taskfile(s) needs to be “cloud-native” **| DALL.E**" alt="15 f" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}

> Lets get the obvious out of the way, why not continue using make ⁉️ well, as mentioned above -> no solid good reason except it’s scalability and the promise of the **ones below -> which were enough for me ;)**

> If you haven’t pivoted yet to the go-task doc / repository … I urge you to brew install go-task / sudu snap install task — classic / choco install go-task -> is really all you need to get hacking ;).

Side note: in one of the projects I’ll mention below I saw a brilliant Makefile in the root of the repo with the following task:

```sh
    all: install-taskfile
    
    install-taskfile:
     @command -v task > /dev/null 2>&1 && echo "Task is already installed, ignoring." || (echo "Installing Task..." && curl --location https://taskfile.dev/install.sh -o install_task.sh && (if [ -w /usr/local/bin ]; then sh install_task.sh -d -b /usr/local/bin; else sudo sh install_task.sh -d -b /usr/local/bin; fi) && rm install_task.sh)
```

What can you do with it … in a nutshell, go-task is designed to handle today’s multifaceted development workflows with greater ease, due to a few facts

1. It is declared as you guest it, in yaml - just like anything else devops 😃

2. It is **written in go** a single executable — which makes it fast & portable

3. It has many built-in standards which I will share a few examples from variable handling, env files dependencies and more

4. It has a very cool **experimental flag **or **feature toggle **which I am now working with for experimental features -> especially the **Remote tasks** (— BTY so far it “just works” which is surprising)
> if I don’t break and attempt to build my own ring — I’ll write a sequel on how Im using this **experiment feature** named **“remote tasks”**

1. I wasn’t sure if its **#1** or **#5** … global ~/.taskfile.yaml an extremely cool feature which could be a substitute / complimentary to the remote taskfile feature — i’m not sure yet

Where will I be using this ? In one word — everywhere ;)
from **DevEnv** to **AnyEnv …**

{{< image src="https://cdn-images-1.medium.com/max/2000/1*hNGUauzHrxNBYOPoeUfB6g.png" caption="From **DevEnv **to **“AnyEnv” | DALL.E**" alt="15 f" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}

When I say from **DevEnv** to **AnyEnv **I really mean to say, that in many cases my CI workflow and my development workflow, could be executed from the same Taskfile — the one I use on my local machine, the one stored in git … (the same file in the root of my home folder ?!)

```yaml
    version: '3'
    
    dotenv: # global scope .envfile 
      - .env
    
    vars: # global scope env vars
      HELM_VERSION: v3.13.0
    
    tasks:
      build:
        desc: Build the Go application
        cmds:
          - go build -o '{{.PROJECT_NAME}}'
    
      test:
        desc: Run Go tests
        cmds:
          - go test
    
      docker-build:
        desc: Build a Docker container
        cmds:
          - docker build -t '{{.VENDOR_NAME}}/{{.PROJECT_NAME}}:{{.VERSION}}' .
    
    tasks:
      install:helm:
        desc: install helm from sources
        cmds:
        # vars without '.' (e.g. {{.HELM_VERSION}} at beginning are build-in
        - wget -qO- https://get.helm.sh/helm-{{.HELM_VERSION}}-{{OS}}-{{ARCH}}.tar.gz | tar xvz -C ./ 
```

if we take a look at the .env we will find:

```sh
    VENDOR_NAME=tikal
    PROJECT_NAME=keda-poc
```

And although you could say the exact same things on Makefiles … Task comes with a set of features that in other tools we had to have a contrib or a plugin in order to get features such as .env files … (I remember a script I wrote back in the days…).

So let’s take the theory and let’s examine some practical examples

{{< image src="https://cdn-images-1.medium.com/max/2000/1*BAYflQ9Zt9D_CXWXEXfEJw.png" caption="From theory to practice" alt="15 f" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}

**(1) Gruberdev’s Local-GitOps [Taskfile](https://github.com/gruberdev/local-gitops/blob/main/Taskfile.yml) — **This Taskfile stands out as one of the most advanced implementations, showcasing how go-task can manage intricate workflows in local GitOps setups.

Note the usage of `includes` — a very cool feature the classification will also be apparent in the task’s completion …

```yaml
    includes:
      argocd: ./tasks/argocd.yaml
      templates: ./tasks/templates.yaml
      tools: ./tasks/tools.yaml
```

The built-in osand arch support:

```yaml
    # ./tasks/tools.yaml
      
    mkcert:
      cmds:
      - |
        echo -e "Installing mkcert" && \
        {{if eq OS "windows"}}choco install mkcert{{end}} \
        {{if eq OS "darwin"}}brew install mkcert && brew install nss{{end}} \
        {{if eq OS "linux"}}brew install mkcert{{end}}
      ignore_error: true
```

**(2) Go-Task’s Own [Taskfile](https://github.com/go-task/task/blob/main/Taskfile.yml) **: ) as the task project itself, this Taskfile serves as an excellent reference for understanding the standard practices and potential of go-task.

Note-worthy example like the example I agave above with dynamic-variables GO_PACKAGES = sh: go list ./...

```yaml
      test:all:
        desc: Runs test suite with signals and watch tests included
        deps: [install, sleepit:build]
        cmds:
          - go test {{catLines .GO_PACKAGES}} -tags 'signals watch'
        vars:
          GO_PACKAGES:
            sh: go list ./...
```

Also note the usage of deps keyword which defines dependencies between tasks …

These examples demonstrate go-task’s versatility in handling diverse tasks, from simple to complex, in a more organized and efficient manner than traditional Makefiles.

{{< image src="https://cdn-images-1.medium.com/max/2000/1*f28eLWybQgIFEhOCFXqZTQ.png" caption="A Modern approach to Task Management **| DALL.E**" alt="15 f" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}

My exploration continues with** Remote Task Execution …**

From Makealicious to Taskiosk (temp name) — options in mind. My needs are to configure and operate all the tools in the following diagram, in my wildest dream I have a “taskfile per provider” — and one index to include them all ;)

{{< image src="https://cdn-images-1.medium.com/max/2000/1*jCbmoF_FeKkSQFf_8gvP9A.png" caption="On Tool to Manage" alt="15 f" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="image title"  webp="false" >}}

Go-task feels like my custom shell on steroids — and in a much more **cloud-native way ! **It enables a centralized management of tasks, even when they are spread across different environments, versions , in a container / in CI.

It’s as close as it gets to a tool I’d love to use in every project (a sentence I used to say about Make ) … 🫡 hope this post motivates you to give it a try.

<hr />

{{< notice "info" >}}
Originally posted on [medium.com](https://medium.com/israeli-tech-radar/from-yak-shaving-to-mastering-tasks-982b669e05e8)
{{< /notice >}}
