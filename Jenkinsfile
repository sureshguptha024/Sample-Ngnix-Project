name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Build Docker Image
        run: docker build -t nginx-devops .

      - name: Push Docker Image
        run: |
          echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin
          docker tag nginx-devops mydockerhub/nginx-devops
          docker push mydockerhub/nginx-devops

      - name: Deploy to Kubernetes
        run: kubectl apply -f k8s-deployment.yml
