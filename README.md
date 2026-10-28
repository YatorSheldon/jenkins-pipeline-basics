# Jenkins pipeline basics

My first declarative Jenkins pipelines, written in August 2024 while learning CI/CD. This repo brings
together a set of earlier practice repos (`easy-Bank`, `pipeline`, `pi`, and others) that contained
versions of the same pipeline, so the work lives in one documented place.

## What the pipeline models

[`Jenkinsfile`](Jenkinsfile) defines the stages of a typical delivery pipeline:

| Stage | Purpose |
| --- | --- |
| Build | Fetch the source from the workspace and compile it into artifacts |
| Test | Run unit and integration tests |
| Code Quality Check | Static analysis / quality gate |
| Deploy | Deploy to a staging environment |
| Approval | Pause for a manual sign-off before production |
| Deploy to Production | Release to the production environment |

It also uses pipeline-level `environment` variables for the workspace path and target environments,
and a `post { always { … } }` block that runs whatever the outcome.

Each stage only `echo`s what it would do: the goal was to learn the structure of a declarative
pipeline, stage ordering, environment variables and approval gates in Jenkins before wiring in real
tools.

## Running it

1. In Jenkins, create a new **Pipeline** job.
2. Under *Pipeline*, choose **Pipeline script from SCM**, point it at this repository and leave the
   script path as `Jenkinsfile`.
3. Click **Build Now** and watch each stage in the Stage View.

## Where this went next

The same stage structure, with every step made real (linting, pytest, model training, a model quality
gate, a Docker build, manual approval and a health-checked deploy), is used in
[**transaction-fraud-detection**](https://github.com/YatorSheldon/transaction-fraud-detection/blob/main/Jenkinsfile).
