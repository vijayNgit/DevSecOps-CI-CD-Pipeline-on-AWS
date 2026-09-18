# DevSecOps CI/CD Pipeline on AWS

A hands-on implementation of a **DevSecOps CI/CD Pipeline** on **AWS** using **Jenkins, Docker, Hadolint, Trivy, and Amazon SNS**. This project demonstrates **Shift-Left Security** by automatically linting Dockerfiles, scanning container images for vulnerabilities, and sending security reports before deployment.

> **Tech Stack:** AWS (EC2, IAM, VPC, Security Groups, SNS) • Jenkins • Docker • Docker Compose • Hadolint • Trivy • Linux

---

## Architecture

> *(Add your architecture diagram or screenshot here.)*

---

# Implementation Steps

## 1. IAM Role Assignment

Created an **IAM Role** for the Jenkins EC2 instance to securely interact with AWS services without using access keys.

### Purpose

- Allow Jenkins running on EC2 to publish notifications to **Amazon SNS**
- Follow AWS best practices using **Instance Profiles**

**Screenshot**

> `screenshots/01-iam-role.png`

---

## 2. VPC Network

Created an **isolated VPC** dedicated to the Jenkins CI/CD environment.

### Configuration

- Custom VPC
- Public subnet for Jenkins
- Internet Gateway for external access
- Route table configured for internet connectivity

### Purpose

- Isolate CI/CD infrastructure
- Provide secure networking for Jenkins

**Screenshot**

> `screenshots/02-vpc.png`

---

## 3. Security Groups

Configured Security Groups to control inbound and outbound traffic for Jenkins.

### Inbound Rules

| Port | Purpose |
|------|---------|
| 80 | Jenkins HTTP Access |
| 22 | SSH Administration |

### Purpose

- Allow browser access to Jenkins
- Allow secure SSH management

**Screenshot**

> `screenshots/03-security-group.png`

---

## 4. EC2 Jenkins Server

Launched an **Amazon EC2** instance to host Jenkins and the required DevSecOps tools.

### Configuration

- Ubuntu EC2 Instance
- IAM Role attached
- Security Group attached
- Public IP enabled

### Purpose

- Host Jenkins
- Run Docker
- Execute security scans

**Screenshot**

> `screenshots/04-ec2.png`

---

## 5. SNS Alert Topic

Created an **Amazon SNS Topic** used by Jenkins to publish security scan reports.

### Purpose

- Send combined **Hadolint** and **Trivy** reports
- Notify when pipeline execution completes

**Screenshot**

> `screenshots/05-sns-topic.png`

---

## 6. Deploy Jenkins

Connected to the EC2 instance and prepared the environment before deploying Jenkins.

### Setup Steps

- Connected through SSH
- Increased system memory (Swap)
- Installed Docker
- Installed Docker Compose
- Deployed Jenkins using a Docker Compose stack

### Deployment

```bash
docker compose up -d
```

### Result

Jenkins became accessible through the browser.

**Screenshot**

> `screenshots/06-jenkins-running.png`

---

## 7. Create Jenkins Pipeline

Built a Jenkins Pipeline that performs automated DevSecOps checks.

### Pipeline Workflow

1. Generate sample application
2. Lint Dockerfile using **Hadolint**
3. Build Docker image
4. Scan image using **Trivy**
5. Generate combined security report
6. Publish report through **Amazon SNS**

### Security Checks

| Tool | Purpose |
|------|---------|
| Hadolint | Dockerfile Best Practices |
| Trivy | Container Vulnerability Scan |

**Screenshot**

> `screenshots/07-pipeline.png`

---

## 8. Execute and Verify

Executed the complete pipeline and verified every stage successfully completed.

### Verification Checklist

- Jenkins pipeline executed successfully
- Docker image built
- Hadolint completed linting
- Trivy generated vulnerability report
- SNS notification delivered
- Security report successfully published

**Final Result**

The pipeline demonstrates **Shift-Left Security**, ensuring vulnerable container images are identified during CI before reaching deployment.

**Screenshot**

> `screenshots/08-success.png`

---

# Pipeline Flow

```text
Developer
    │
    ▼
Jenkins Pipeline
    │
    ├── Hadolint
    │
    ├── Docker Build
    │
    ├── Trivy Scan
    │
    ├── Combined Report
    │
    ▼
Amazon SNS Notification
```

---

# Project Structure

```text
DevSecOps-CI-CD-AWS/
│
├── Jenkinsfile
├── docker-compose.yml
├── Dockerfile
├── screenshots/
│   ├── 01-iam-role.png
│   ├── 02-vpc.png
│   ├── 03-security-group.png
│   ├── 04-ec2.png
│   ├── 05-sns-topic.png
│   ├── 06-jenkins-running.png
│   ├── 07-pipeline.png
│   └── 08-success.png
└── README.md
```

---

# Skills Demonstrated

- AWS IAM
- Amazon EC2
- Amazon VPC
- Security Groups
- Amazon SNS
- Jenkins
- Docker
- Docker Compose
- Hadolint
- Trivy
- CI/CD
- DevSecOps
- Shift-Left Security
- Linux Administration

---

# Acknowledgment

This project was implemented as a **hands-on DevSecOps on AWS lab** from **KodeKloud**, where I independently provisioned AWS resources, configured Jenkins, integrated security scanning, and validated the complete CI/CD security workflow.
