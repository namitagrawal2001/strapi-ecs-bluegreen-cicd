🚀 Strapi Deployment on AWS ECS (Fargate) with Blue-Green CI/CD
📌 Overview

This project demonstrates a production-ready deployment of a Strapi application on AWS ECS Fargate, fully managed using Terraform and automated with GitHub Actions.

It implements a Blue-Green deployment strategy using AWS CodeDeploy, ensuring zero downtime during updates.

🏗 Architecture

Client
⬇
Application Load Balancer (ALB)
⬇
Amazon ECS (Fargate) – Strapi Container
⬇
Amazon RDS (PostgreSQL)

🧰 Tech Stack

AWS ECS (Fargate)

Amazon RDS (PostgreSQL)

Application Load Balancer

AWS CodeDeploy (Blue-Green Deployment)

Amazon ECR

Terraform (Infrastructure as Code)

Docker

GitHub Actions (CI/CD)

📂 Project Structure
.
├── app/                        # Strapi application
├── terraform/                  # Infrastructure as Code
│   ├── modules/
│   ├── main.tf
│   ├── variables.tf
│   └── outputs.tf
├── .github/workflows/          # CI/CD pipelines
├── appspec.json                # CodeDeploy configuration
└── README.md
⚙ Infrastructure Provisioning
Initialize Terraform
cd terraform
terraform init
Review Execution Plan
terraform plan
Deploy Infrastructure
terraform apply

This provisions:

VPC and Subnets

Security Groups

Application Load Balancer

Blue & Green Target Groups

ECS Cluster and Service

Amazon RDS PostgreSQL instance

CodeDeploy Application and Deployment Group

🔄 Blue-Green Deployment Strategy

Deployment workflow:

Code is pushed to GitHub.

GitHub Actions builds Docker image.

Image is pushed to Amazon ECR.

New ECS task definition revision is created.

CodeDeploy launches a replacement task set.

Traffic is shifted gradually (Canary strategy).

On success → full traffic shift.

On failure → automatic rollback.

This ensures zero downtime and safer releases.

🗄 Database Configuration

The application uses Amazon RDS PostgreSQL for persistent storage.

ECS task definition includes environment variables:

DATABASE_HOST

DATABASE_PORT

DATABASE_NAME

DATABASE_CLIENT

DATABASE_USERNAME

DATABASE_PASSWORD

This ensures secure and production-ready data management.

🩺 Health Check Configuration

ALB Target Group Health Check:

Path: /

Matcher: 200-399

Port: 1337

This allows redirect responses (302) to be treated as healthy, ensuring stable service routing.

🔐 Security Design

RDS is not publicly accessible.

Database access restricted via Security Groups.

ECS tasks communicate with RDS inside private network.

No direct internet exposure to database.

🚀 CI/CD Pipeline

GitHub Actions automates:

AWS authentication

Docker image build

Push to ECR

ECS task definition update

CodeDeploy deployment trigger

Deployment monitoring

This creates a fully automated release workflow.

🧹 Destroy Infrastructure

To remove all provisioned resources:

terraform destroy -auto-approve
📈 Key Highlights

Infrastructure fully managed with Terraform

Blue-Green zero-downtime deployment

Production-ready database setup

Secure networking configuration

Fully automated CI/CD pipeline

Scalable containerized architecture

🎯 What This Project Demonstrates

Cloud architecture design

Infrastructure as Code best practices

Containerized deployment strategies

Production-grade AWS setup

Automated DevOps workflow