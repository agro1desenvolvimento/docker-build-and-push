# Docker Build and Push Action

A GitHub Action that builds a Docker image and pushes it to Docker Hub.

## Inputs

| Input | Description | Required | Default |
|-------|-------------|:--------:|---------|
| `name-and-tag` | Docker image name with tag (e.g., `username/image:tag`) | ✅ | - |
| `dockerhub-username` | Docker Hub username | ✅ | - |
| `dockerhub-password` | Docker Hub password or access token | ✅ | - |
| `context` | Docker build context directory | ❌ | `.` |
| `dockerfile` | Path to Dockerfile | ❌ | `./Dockerfile` |
| `args` | Build arguments as key-value pairs | ❌ | - |

## Usage

Add your Docker Hub username to GitHub secrets as `DOCKER_USERNAME` and create a token in Docker Hub and add it to GitHub secrets as `DOCKER_PASSWORD`.

```yaml
name: Docker Build and Push

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      
      - name: Build and push Docker image
        uses: agro1desenvolvimento/docker-build-and-push@v2
        with:
          name-and-tag: username/my-image:tag
          dockerhub-username: ${{ secrets.DOCKER_USERNAME }}
          dockerhub-password: ${{ secrets.DOCKER_PASSWORD }}
          context: .
          dockerfile: ./Dockerfile
          args: VERSION=1.0.0 DEBUG=false
```
