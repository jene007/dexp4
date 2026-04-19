# dexp4
Create a CI pipeline using GitHub Actions to build and push a Docker image of a Python app to Docker Hub.
GitHub Actions
Docker
Python
Step 1 – Add secrets to GitHub repo
🔐
Repo → Settings → Secrets and variables → Actions → New repository secret:
DOCKER_USERNAME — your Docker Hub username
DOCKER_PASSWORD — your Docker Hub access token
.github/workflows/docker-publish.yml
yaml
copy
name: Build and Push Docker Image

on:
  push:
    branches: [ main ]

jobs:
  build-push:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Log in to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build Docker image
        run: docker build -t ${{ secrets.DOCKER_USERNAME }}/python-app:latest .

      - name: Push to Docker Hub
        run: docker push ${{ secrets.DOCKER_USERNAME }}/python-app:latest
Expected Output
✅
Every push to main triggers a green workflow run in the Actions tab and the image appears on Docker Hub.
