# Assignment 2 - Design Note

Author: Nikhil Kumbhare

Date: June 2026

## Objective

Create a reusable GitHub Actions pipeline that can be shared across multiple application repositories.

---

## Design Approach

A dedicated repository named:

github-actions-template

was created to store the reusable workflow.

The reusable workflow accepts configurable parameters:

- image_repository
- build_command
- dockerfile_path

This allows different repositories to use the same pipeline without duplicating workflow code.

---

## Reusability

Any application repository can consume this workflow by:

1. Creating a workflow file
2. Referencing the reusable workflow repository
3. Passing application-specific inputs

Example:

```yaml
uses: nikhilk7/github-actions-template/.github/workflows/reusable-docker-build.yaml@main
```

---

## Onboarding a New Application

To onboard a new application:

1. Create a Docker Hub repository
2. Add Docker credentials as GitHub Secrets
3. Create a workflow file
4. Call the reusable workflow
5. Pass:
   - image_repository
   - build_command
   - dockerfile_path

No changes are required in the shared pipeline.

---

## Benefits

- Single source of pipeline logic
- Easy maintenance
- Consistent CI/CD process
- Reusable across multiple projects
- Reduced duplication
- Faster onboarding of new repositories

