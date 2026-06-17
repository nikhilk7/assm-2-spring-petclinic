# Reusable Docker Build Pipeline

Author: Nikhil Kumbhare

GitHub: https://github.com/nikhilk7

---

This repository contains a reusable GitHub Actions workflow that can be used by multiple application repositories to build applications, create Docker images, and push them to Docker Hub.

## Features

- Reusable GitHub Actions workflow
- Configurable build command
- Configurable Dockerfile path
- Configurable Docker image repository
- Docker image tagging using GitHub Run Number and Commit ID
- Pushes image to Docker Hub

---

## Required Inputs

| Input | Description | Example |
|---------|-------------|---------|
| image_repository | Docker Hub repository name | assm2-spring-petclinic |
| build_command | Application build command | ./mvnw clean package |
| dockerfile_path | Path to Dockerfile | Dockerfile |

---

## Required Secrets

| Secret | Description |
|----------|-------------|
| DOCKER_USERNAME | Docker Hub Username |
| DOCKER_TOKEN | Docker Hub Access Token |

---

## Example Usage

```yaml
name: Spring Petclinic CI

on:
  push:
    branches:
      - main

jobs:
  call-reusable-workflow:
    uses: nikhilk7/github-actions-template/.github/workflows/reusable-docker-build.yaml@main

    with:
      image_repository: assm2-spring-petclinic
      build_command: ./mvnw clean package
      dockerfile_path: Dockerfile

    secrets:
      DOCKER_USERNAME: ${{ secrets.DOCKER_USERNAME }}
      DOCKER_TOKEN: ${{ secrets.DOCKER_TOKEN }}
```

## Generated Docker Image

Example:

```
nikhilkumbhare/assm2-spring-petclinic:7-a1b2c3d
```

Where:

- 7 = GitHub Run Number
- a1b2c3d = Short Commit ID

Latest tag:

```
nikhilkumbhare/assm2-spring-petclinic:latest
```
