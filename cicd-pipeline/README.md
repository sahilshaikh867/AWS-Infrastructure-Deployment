# ⚙️ CI/CD Pipeline Automation

An end‑to‑end **CI/CD pipeline** that takes code from commit → tested → container image → deployed to a server environment.

---

## 🎯 Goal

- No manual SSH & “git pull on server” deployments.  
- Every change to `main` should:
  1. Run tests & linting  
  2. Build a Docker image  
  3. Push image to a registry  
  4. Deploy / restart the app container on a target host  

---

## 🧩 Tech Stack (Example)

- **CI**: GitHub Actions (ya Jenkins)
- **Containerization**: Docker
- **Registry**: Docker Hub / GHCR
- **App Host**: Linux VM (Nginx reverse proxy + Docker)
- **Code**: Any web app (Node/Python/…); focus is on pipeline

---

## 🧱 High‑Level Pipeline
Developer → Git push → CI (tests) → Docker build+push → Deploy → Live server

text

Trigger:  
- `on: [push, pull_request]` to `main`  
- optional: manual `workflow_dispatch`

---

## 🔁 Stages (Step‑by‑Step)

1. **Trigger**
   - Event: push or PR targeting `main`
   - Optional manual run to redeploy

2. **Checkout & Setup**
   - CI runner checks out code
   - Sets up language runtime (Node/Python/etc.)
   - Restores dependency cache if configured

3. **Install & Test**
   - Install dependencies (`npm ci`, `pip install -r requirements.txt`, etc.)
   - Run unit tests
   - Run linters / format checks
   - **If tests fail → pipeline stops here**

4. **Docker Build**
   - Build image using `Dockerfile`
   - Tag with:
     - `latest`
     - commit SHA (e.g. `app:sha-abcdef`)

5. **Push to Registry**
   - Login to Docker Hub / GHCR using CI secrets
   - Push image tags to registry

6. **Deploy to Server**
   - Option A: **SSH** into server
     - Pull new image
     - Restart container (plain Docker or docker‑compose)
   - Option B: **Self‑hosted runner** on the server
     - CI job directly runs `docker-compose up -d` with new image

---

## 📄 Sample GitHub Actions Workflow (Simplified)

name: CI/CD

on:
push:
branches: [ main ]
pull_request:
branches: [ main ]
workflow_dispatch:

jobs:
build-and-deploy:
runs-on: ubuntu-latest

text
steps:
  - name: Checkout
    uses: actions/checkout@v4

  - name: Setup Node
    uses: actions/setup-node@v4
    with:
      node-version: 20

  - name: Install dependencies
    run: npm ci

  - name: Run tests
    run: npm test

  - name: Build Docker image
    run: |
      docker build -t youruser/yourapp:latest .
      docker tag youruser/yourapp:latest youruser/yourapp:${{ github.sha }}

  - name: Login to Docker Hub
    run: |
      echo "${{ secrets.DOCKERHUB_TOKEN }}" | docker login -u "${{ secrets.DOCKERHUB_USER }}" --password-stdin

  - name: Push image
    run: |
      docker push youruser/yourapp:latest
      docker push youruser/yourapp:${{ github.sha }}

  # Example deploy via SSH
  - name: Deploy to server
    uses: appleboy/ssh-action@v1.0.0
    with:
      host: ${{ secrets.SERVER_HOST }}
      username: ${{ secrets.SERVER_USER }}
      key: ${{ secrets.SERVER_SSH_KEY }}
      script: |
        docker pull youruser/yourapp:latest
        docker stop app || true
        docker rm app || true
        docker run -d --name app -p 80:3000 youruser/yourapp:latest
text

*(IDs, secrets, and app port adjust according to your project.)*

---

## 📊 What Was Learned

- Designing a **pipeline** with clear stages instead of manual steps.  
- Managing **secrets** (registry, server SSH) safely within CI.  
- Making deployments **repeatable** and versioned via Docker tags.  
- Understanding the difference between **CI** (tests/build) and **CD** (deploy).  

---

## 🔮 Next Improvements

- Add **staging environment** and a manual approval before production.  
- Run post‑deploy **smoke tests**.  
- Extend deployment to **Kubernetes** (EKS/AKS) instead of a single VM.
