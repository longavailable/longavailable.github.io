---
layout: post
title:  Github actions jobs/workflows/repository depend on each other
author: Bruce Liu
#last update date
date:   2023-05-26 20:00:00 +0800
#first published date
published:   2023-05-21 20:40:00 +0800
categories: [post]
tags: [Github, workflow, Github Action]
description: 
header-image: 
permalink: /workflow-depends
---

If you are using GitHub Actions to automate your workflows, you might want to trigger a workflow based on another workflow's completion or status. For example, you might want to run some tests after a build workflow finishes, or deploy your application only if the tests pass. In this blog post, I will show you three methods to achieve this functionality.

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

There are different ways to trigger a workflow based on the completion or status of another workflow in GitHub Actions. One method is to use the keyword [`needs`] in the same YAML file to specify the dependencies between jobs. Another method is to use the [`workflow_run`] event to run a workflow after another workflow has been completed or requested. A third method is to use the [`repository_dispatch`] event to send a custom webhook event to a repository and trigger a workflow.

## [`needs`] method

All-in-one YAML file:

```yaml
name: test of needs method

on: push

jobs:
  job1:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    
    - name: Do something
      run: ...

  job2:
    needs: job1	        # keyword
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Do something
        run: ...
```

## [`workflow_run`] method

YAML file for job1:

```yaml
name: job1's name

on: push

jobs:
  job1:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    
    - name: Do something
      run: ...
```

YAML file for job2:

```yaml
name: job2's name

on: 
  workflow_run:
    workflows: ['job1's name']
    types:
      - completed
	  
jobs:
  job2:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    
    - name: Do something
      run: ...
```

## [`repository_dispatch`] method

YAML file for job1:

```yaml
name: job1's name

on: push

jobs:
  job1:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    
    - name: Do something
      run: ...

    - name: send a POST request to the GitHub API
      run: |
        curl -X POST \
        -H "Accept: application/vnd.github.v3+json" \
        -H "Authorization: token <your token>" \	# ${{ secrets.GITHUB_API_TOKEN }}
        --data '{"event_type": "job1-event"}' \
        https://api.github.com/repos/<owner>/<repo>/dispatches		# repository which job2 file is located
```

YAML file for job2:

```yaml
name: job2's name

on: 
  repository_dispatch:
    types:['job1-event']
	  
jobs:
  job2:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    
    - name: Do something
      run: ...
```

Of course, you can trigger the job2 from the terminal:

```
curl -X POST \
-H "Accept: application/vnd.github.v3+json" \
-H "Authorization: token <your token>" \
--data '{"event_type": "job1-event"}' \
https://api.github.com/repos/<owner>/<repo>/dispatches
```

Or python [requests] ...

## References

- [Trigger GitHub actions if push in another repo](https://stackoverflow.com/a/68407424/12371819)

- [Permanently authenticating with Git repositories](https://confluence.atlassian.com/bitbucketserver080/permanently-authenticating-with-git-repositories-1115142281.html)

<!--links-->
[`needs`]:https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idneeds
[`workflow_run`]:https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#workflow_run
[`repository_dispatch`]:https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#repository_dispatch
[requests]:https://requests.readthedocs.io/en/latest/
