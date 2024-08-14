# Service (Backend) API: Nodes

This service is part of backend APIs of BLOCKCHAIN LABS.

## BASICS

Technologies:
1. Kotlin
1. Spring boot

### Prerequisites

Before you begin, ensure you have met the following requirements:

* You have installed the `GIT`
* You have installed the `JDK` version of `11`
* You have installed the `Gradle` version of `7.x`
  
Extra tool to deployment development 
* You have installed the `docker` or `docker desktop`

#### You may install components by [Chocolately](https://chocolatey.org/)
GIT
```bash
choco install git
```

Gradle
```bash
choco install gradle
```

JDK 11
```bash
choco install jdk11
```

### Installing service

To install the service, follow these steps:

Download project:
```bash
git clone --recurse-submodules <rep>
```

Install dependencies
```shell
./gradlew build
```

## Startup service API
```shell
./gradlew bootRun
```

It'll be on port `8080`.

## Project structure

```
.dev/                           Developer assist folder
|- commands/                    Folder to put in usual commands in order of use
|  |- 01-docker/                Docker commands to build images
|  |- 02-kubernetes/            Kubernetes commands to deploy locally docker images
|  |- 03-curl/                  Curl commands to check docker image was deployed correctly in the local kubernetes cluster
deploy/                         Kubernetes deployment config folder
|- local/deployment.yaml        Deployment config to the local kubernetes environment
doc/                            Git submodule with Swagger/OpenApi project
gradle/                         Embedded gradle folder
src/                            Service API source code folder
|- main/                        Service API app code
|  |- kotlin/                   Source code
|  |  |- config/                Configuration folder e.g. Spring Security, CORS and others configs
|  |  |- domain/                Business code folder
|  |  |- support/               Support folder e.g. Converters, Exceptions, ExceptionHandler and others
|  |  |- Application.kt         Application main class
|  |- resources/                Resource folder
|  |  |- application.yml        Application configuration file
|- test/                        Unit tests folder
|  |- kotlin/                   Test source code
|  |- resources/                Resource test folder
|- testIntegration/             System/integration tests folder
.dockerignore                   Docker ignore
.gitignore                      Git ignore
.gitmodules                     Git sub modules: swagger project
azure-pipelines.yaml            Pipeline trigger configuration for git repository
build.gradle.kts                Gradle definitions
settings.gradle.kts             Gradle variables
Dockerfile                      Dockerfile to build image for kubernetes
```

## DEVELOPMENT GUIDELINE

### Tools

* GIT GUI: Sourcetree
* GIT
* IDE: Intellij IDEA

#### IDE SETTINGS

* Intellij IDEA


### Coding guideline

#### Kotlin
* [Kotlin Coding Conventions](https://kotlinlang.org/docs/coding-conventions.html)


## Project libs
* Spring boot
    * https://spring.io/projects/spring-boot
* OpenAPI Specification - API
    * https://swagger.io/specification/

## DEPLOY

Deploy settings are performed by:
1. Azure Pipeline trigger `azure-pipeline.yaml`
1. Ansible config `environment/` and `utils/`
1. Kubernetes deployment settings `deploy/`

### DEV Local
The developer may be to deploy the service locally:

#### Prerequisites:
1. Docker desktop
1. Enable kubernetes in docker desktop
    1. `docker desktop > settings > kubernetes > enable kubernetes`

#### To create deploy, follow these steps:
1. Build docker image
    1. command: `.dev/commands/01-docker/01-docker-build.sh`
1. Create kubernetes namespace
    1. command: `.dev/commands/02-kubernetes/01-kubernetes-create-namespace.sh`
1. Deploy docker image to kubernetes
    1. command: `.dev/commands/02-kubernetes/02-kubernetes-deploy-local.sh`

#### Do check deploy was successful:
1. Do CURL to service API in kubernetes
    1. command: `.dev/commands/03-curl/01-curl-check-health.sh`

### DEV
Deploy info in:
```
deploy/dev
```
### PROD
Deploy info in:
```
deploy/prod
```