# This organization shared workflow

## publish-docker-image-by-tag.yaml
To build a Dockerfile and publish docker image. Workflow is triggered by tag.

Tag format [0-9].[0-9].[0-9] is recognized as Release tag and creates "latest" docker image tag too.

It uses: 
- Docker Hub target repo from the GitHub repo DOCKERHUB_REPO variable
- Docker build args from the inputs
- DockerHub secrets from explicitly defined secrets (for external usage)

Usage example:

```yaml
name: Publish Docker Image

on:
  push:
    tags:
      - '**'

jobs:

  call-publish-docker-image-by-tag:
    uses: dshakalo/shared-workflows/.github/workflows/publish-docker-image-by-tag.yaml@main
    with:
      build-args: | 
        "MASTODON_VERSION=${{ vars.MASTODON_VERSION }}"
    secrets:
      DOCKER_USERNAME: ${{ secrets.DOCKER_USERNAME }}
      DOCKER_PASSWORD: ${{ secrets.DOCKER_PASSWORD }}
```

