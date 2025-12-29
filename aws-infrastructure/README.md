# 🏗️ AWS Infrastructure Deployment

Design and deployment of a **3‑tier web application architecture** on AWS, focusing on high availability, security and clarity of design.

---

## 🎯 Goal

Build a production‑style environment where:

- Users access the app over **HTTPS**  
- Traffic goes through an **Application Load Balancer (ALB)**  
- Application servers run in private subnets with **Auto Scaling**  
- The database is **isolated** in private subnets (no public access)  
- Static assets and backups live in **S3**  
- Everything is observed via **CloudWatch**

---

## 🧱 Architecture Summary

**Main components:**

- **VPC** – `10.0.0.0/16`
- **Subnets**
  - 2× public subnets (for ALB, NAT)
  - 2× private app subnets (for EC2 ASG)
  - 2× private DB subnets (for RDS)
- **Networking**
  - Internet Gateway for public subnets
  - NAT Gateway for private subnets
- **Compute**
  - Launch Template + Auto Scaling Group
  - EC2 instances in private subnets
- **Load Balancing**
  - Application Load Balancer in public subnets
  - Listeners on HTTP/HTTPS (redirect HTTP → HTTPS)
- **Database**
  - RDS MySQL, Multi‑AZ
  - Only reachable from app SG
- **Storage**
  - S3 for static assets & backups
- **Observability**
  - CloudWatch metrics, dashboards & alarms
  - ALB access logs

---

## 🔁 Request Flow

1. User enters application URL (e.g. via **Route 53** DNS record).  
2. Traffic goes to the **ALB** in public subnets.  
3. ALB terminates **HTTPS** and forwards to the EC2 **Auto Scaling Group**.  
4. EC2 instances read/write data from **RDS** in private DB subnets.  
5. Static assets are served through **S3** (optionally behind CloudFront).  
6. Metrics and logs are pushed to **CloudWatch** for monitoring & alerts.

---

## 🛠️ Step‑by‑Step Setup (Manual)

1. **Create VPC & Subnets**
   - VPC CIDR: `10.0.0.0/16`
   - Create:
     - Public Subnet A (e.g. `10.0.1.0/24`)
     - Public Subnet B (e.g. `10.0.2.0/24`)
     - Private App Subnet A/B
     - Private DB Subnet A/B

2. **Internet & NAT**
   - Attach an **Internet Gateway** to the VPC.
   - Create:
     - Public route table → route `0.0.0.0/0` → Internet Gateway.
     - Private route table → route `0.0.0.0/0` → NAT Gateway (in a public subnet).

3. **Security Groups**
   - **ALB SG**
     - Inbound: `80/443` from internet
     - Outbound: to App SG
   - **App SG**
     - Inbound: HTTP/port from ALB SG only
     - Outbound: to DB SG
   - **DB SG**
     - Inbound: DB port (e.g. 3306) from App SG only

4. **RDS MySQL**
   - Create RDS instance in **private DB subnets**.
   - Enable Multi‑AZ and automated backups.
   - Attach **DB SG**.
   - Set a strong master password and parameter group as needed.

5. **EC2 + Auto Scaling Group**
   - Create a **Launch Template**:
     - Base AMI (with app or use user‑data to deploy)
     - Attach App SG
   - Create **Auto Scaling Group**:
     - Use private app subnets
     - Configure min/max/desired capacities
     - Add CPU‑based scaling policies if needed

6. **Application Load Balancer**
   - Create ALB in **public subnets**.
   - Target group → EC2 instances (ASG).
   - Listener:
     - 80 → redirect to 443
     - 443 → forward to target group (using ACM certificate).

7. **S3 & Backups**
   - Create S3 bucket(s) for:
     - Static assets
     - DB snapshots / exports (optional)
   - Enable versioning and lifecycle rules if required.

8. **CloudWatch & Logs**
   - Enable:
     - EC2 detailed monitoring
     - ALB access logs (to S3)
     - RDS performance insights / metrics
   - Create CloudWatch dashboards:
     - CPU, latency, requests, errors
   - Set alarms (e.g. high CPU, 5xx error rate, low DB connections).

---

## 📊 What Was Learned

- Designing **public vs private** subnets and routing.  
- Using **security groups** to strictly control traffic flow.  
- Building **stateless** app layer with an **Auto Scaling Group** behind an ALB.  
- Configuring RDS in private subnets with least‑privilege access.  
- Basic observability using **CloudWatch** dashboards and alarms.

---

## 🔮 Next Improvements

- Automate the stack using **Terraform / CloudFormation**.  
- Add **CI/CD** to deploy app updates into the ASG.  
- Introduce **WAF** and more advanced logging / central log aggregation.
