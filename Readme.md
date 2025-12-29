# 🚀 DevOps & Cloud Projects – Sahil Shaikh

Collection of hands‑on **DevOps, Cloud, Security & Monitoring** projects built to practice real‑world workflows.

> Each project has: architecture, step‑by‑step flow, and what was learned.

---

## 📂 Projects

### 1️⃣ AWS Infrastructure Deployment

Design and deployment of a **3‑tier web application architecture** on AWS with secure networking, auto scaling and managed database.

- VPC with public & private subnets
- Application Load Balancer + Auto Scaling Group
- RDS MySQL in private subnets
- S3 for static assets & backups
- CloudWatch for metrics & logs

👉 [`AWS Infrastructure Deployment`](aws-infrastructure/README.md)

---

### 2️⃣ CI/CD Pipeline Automation

End‑to‑end **CI/CD pipeline** that runs tests, builds a Docker image, pushes it to a registry and deploys to a server on every commit.

- Git‑based workflow (feature branches → PR → main)
- Tests + linting on every push
- Docker build & push to registry
- Deployment to Linux host using script / Actions runner
- Environment variables & secrets

👉 [`CI/CD Pipeline Automation`](cicd-pipeline/README.md)

---

### 3️⃣ Student Project Tracking System

Full‑stack style **tracking system** for managing student projects, teams, milestones and submissions.

- Roles: Student, Mentor, Admin
- Project & team registration
- Milestones with deadlines
- File uploads (reports, PPTs, etc.)
- Dashboards for mentors & admin

👉 [`Student Project Tracking System`](student-project-tracking/README.md)

---

### 4️⃣ Evil Twin Wi‑Fi Attack Lab

Controlled **security lab** simulating an Evil Twin Wi‑Fi attack to understand how attackers clone SSIDs and how to defend.

- Kali Linux attacker lab
- Fake access point with same SSID
- Captive portal phishing page
- Credential capture (lab only, no real users)
- Learnings + mitigations

👉 [`Evil Twin Wi‑Fi Attack Lab`](evil-twin-lab/README.md)

---

### 5️⃣ Monitoring & Dashboards

Observability setup for **metrics + logs + dashboards** to monitor application and infrastructure health.

- System & application metrics
- Log forwarding & retention
- Dashboards for latency, errors, traffic
- Alert rules on key signals
- Basic incident investigation loop

👉 [`Monitoring & Dashboards`](monitoring-dashboards/README.md)

---

### 6️⃣ Cloud Cost & Security Review

Structured **cloud cost + security review** for a small environment, focusing on quick wins and safe optimizations.

- Resource inventory & tagging
- Idle / over‑sized resource detection
- Storage, snapshots, backups review
- Security groups, encryption, IAM basics
- Action plan: keep, right‑size, stop, secure

👉 [`Cloud Cost & Security Review`](cloud-cost-security/README.md)

---

## 🧭 How to Explore

- Each folder contains:
  - `README.md` → project description, steps, learnings  
  - (optional) IaC / scripts / screenshots (to be added)

You can jump into any project based on what you want to see first:
- **Cloud & networking?** Start with AWS Infrastructure.  
- **Automation?** Go to CI/CD Pipeline.  
- **Security?** Check the Evil Twin lab & Cloud Cost/Security projects.
