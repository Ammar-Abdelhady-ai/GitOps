# GitOps Project (Deployment Branch)

## End to End GitOps Project

This repository contains the Terraform code to maintain VPC and EKS for the vProfile project. The `deployment` branch is used for deployment-specific configurations and steps necessary for deploying the project.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Tools and Prerequisites](#tools-and-prerequisites)
3. [Installation](#installation)
4. [Branch Workflow](#branch-workflow)
5. [Terraform State Management](#terraform-state-management)
6. [Deployment Overview](#deployment-overview)
7. [Why Use Helm in Kubernetes](#why-use-helm-in-kubernetes)
8. [Usage](#usage)
9. [Destroying Infrastructure](#destroying-infrastructure)
10. [Contributing](#contributing)
11. [License](#license)
12. [Contact](#contact)

## Project Overview

The purpose of this project is to demonstrate an end-to-end GitOps workflow using Terraform to manage infrastructure for the vProfile project. GitOps enables continuous deployment for cloud infrastructure by using Git as the single source of truth for declarative infrastructure and applications.

The `deployment` branch is specifically used for:
- Deploying the application to production environments.
- Managing deployment-specific configurations and scripts.
- Ensuring a smooth and efficient deployment process.

## Tools and Prerequisites

- Terraform version 1.6.3
- AWS CLI (for managing AWS resources)
- Helm (for Kubernetes package management)
- Kubernetes CLI (kubectl)
- JDK 11 (for application deployment)
- Maven 3 (for application deployment)
- MySQL 8 (for application deployment)

## Installation

To set up the project, ensure you have the required tools listed above installed, then follow these steps:

1. Clone the repository and checkout the `deployment` branch:
    ```bash
    git clone https://github.com/Ammar-Abdelhady-ai/GitOps.git
    cd GitOps
    git checkout deployment
    ```

2. Configure AWS CLI with your credentials:
    ```bash
    aws configure
    ```

## Branch Workflow

The `deployment` branch follows a workflow that ensures all deployment configurations and scripts are properly managed and tested. This includes:
- Code reviews and approvals.
- Automated testing and validation.
- Manual testing in a deployment environment.

## Terraform State Management

This project uses an S3 bucket to store Terraform state files to enable remote state management and collaboration. Make sure you have an S3 bucket and DynamoDB table set up for state locking.
