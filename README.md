# GitOps Project

## End to End GitOps Project

This repository contains the Terraform code to maintain VPC and EKS for the vProfile project. The project follows a GitOps workflow to enable continuous deployment for cloud infrastructure by using Git as the single source of truth for declarative infrastructure and applications.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Tools Required](#tools-required)
3. [Installation](#installation)
4. [Branch Workflows](#branch-workflows)
    - [Main Branch](#main-branch)
    - [Stage Branch](#stage-branch)
    - [Deployment Branch](#deployment-branch)
5. [Terraform State Management](#terraform-state-management)
6. [Usage](#usage)
7. [Destroying Infrastructure](#destroying-infrastructure)
8. [Contributing](#contributing)
9. [License](#license)
10. [Contact](#contact)

## Project Overview

The purpose of this project is to demonstrate an end-to-end GitOps workflow using Terraform to manage infrastructure for the vProfile project. GitOps enables continuous deployment for cloud infrastructure by using Git as the single source of truth for declarative infrastructure and applications.

## Tools Required

- Terraform version ~> 1.10.3
- AWS CLI (for managing AWS resources)
- JDK 11 (for deployment branch)
- Maven 3 (for deployment branch)
- MySQL 8 (for deployment branch)

## Installation

To set up the project, ensure you have the required tools listed above installed, then follow these steps:

1. Clone the repository:
    ```bash
    git clone https://github.com/Ammar-Abdelhady-ai/GitOps.git
    cd GitOps
    ```

## Branch Workflows

### Main Branch

The `main` branch contains the production-ready code and configurations. It follows the standard GitOps workflow to manage VPC and EKS using Terraform.

### Stage Branch

The `stage` branch is used for testing and staging changes before they are merged into the `main` branch. It ensures that all changes are validated and tested before deployment to production.

### Deployment Branch

The `deployment` branch contains deployment-specific configurations and steps necessary for deploying the project. It includes additional prerequisites and technologies required for deployment.

#### Prerequisites for Deployment Branch

- JDK 11
- Maven 3
- MySQL 8

#### Technologies Used in Deployment Branch

- Spring MVC
- Spring Security
- Spring Data JPA
- Maven
- JSP
- MySQL

#### Database Setup for Deployment Branch

We use MySQL as the database for this project. Below are the steps to install and set up MySQL on Linux Ubuntu 14.04:

1. Update your package list:
    ```bash
    sudo apt-get update
    ```

2. Install MySQL server:
    ```bash
    sudo apt-get install mysql-server
    ```

3. Import the database schema:
    - Locate the `db_backup.sql` file in the `/src/main/resources/` directory.
    - Import the dump file to the MySQL server:
   

## Terraform State Management

This project uses an S3 bucket to store Terraform state files to enable remote state management and collaboration. Make sure you have an S3 bucket and DynamoDB table set up for state locking.

# AWS Resource Cleanup Guide

This guide provides step-by-step instructions for removing all infrastructure and associated resources created by this project. These commands will delete Kubernetes configurations, ingress controllers, Helm deployments, and Terraform-managed resources.

## Steps to Remove Resources

### 1. Delete Kubernetes Configuration

```bash
rm -rf ~/.kube/config
```
- **Purpose**: Removes the local Kubernetes configuration file.
- **Why Needed**: Clears cached or outdated Kubernetes cluster configurations from your local machine.

### 2. Update Kubernetes Configuration for EKS

```bash
aws eks update-kubeconfig --region <region-name> --name <eks-cluster-name>  
```
- **Purpose**: Reconnects your local system to the EKS cluster.
- **Why Needed**: Ensures `kubectl` can communicate with the cluster to delete resources.

### 3. Delete the Ingress Controller

```bash
kubectl delete -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.7.0/deploy/static/provider/aws/deploy.yaml
```
- **Purpose**: Deletes the NGINX ingress controller from the EKS cluster.
- **Why Needed**: Removes the ingress controller used for routing traffic to applications.

### 4. Uninstall the Helm Deployment

```bash
helm uninstall vprofile-stack
```
- **Purpose**: Uninstalls the Helm release named `vprofile-stack`.
- **Why Needed**: Deletes all resources associated with the Helm chart used for deploying the application.

### 5. Navigate to the Terraform Directory

```bash
cd terraform/
```
- **Purpose**: Changes the directory to the Terraform configuration folder.
- **Why Needed**: Ensures Terraform commands are executed in the correct directory.

### 6. Reinitialize Terraform

```bash
terraform init -backend-config="bucket=<s3-bucket-name>" -backend-config="region=<region-name>" -backend-config="key=terraform.tfstate"
```
- **Purpose**: Reinitializes Terraform with the backend configuration.
- **Why Needed**: Ensures Terraform can communicate with the S3 bucket storing the state file.

### 7. Destroy All Terraform-Managed Resources

```bash
terraform destroy -auto-approve
```
- **Purpose**: Deletes all infrastructure resources defined in the Terraform configuration.
- **Why Needed**: Cleans up AWS resources (e.g., VPCs, EKS clusters, S3 buckets) to avoid incurring unnecessary costs.

## Important Notes

- **Backup State Files**: Before running `terraform destroy`, back up your state file if you need to restore the infrastructure later.
- **Deletion Confirmation**: Review the resources managed by Terraform to confirm no unintended resources will be destroyed.
- **Costs**: Removing resources ensures you don't incur costs for unused infrastructure.

By following these steps, you can safely and completely remove all resources related to this project.


## Repository Secrets Setup for GitHub Actions

This repository uses GitHub Actions to automate tasks like testing, building, and deploying the application. To ensure the workflow runs successfully, you must configure the following repository secrets. These secrets store sensitive information and are used during the workflow execution.

### Required Secrets

| Secret Name           | Purpose                                                                                 | Example Value                                    |
|-----------------------|-----------------------------------------------------------------------------------------|------------------------------------------------|
| `AWS_ACCESS_KEY_ID`   | Used to authenticate with AWS services (e.g., ECR, EKS).                                | `AKIAEXAMPLEID`                                |
| `AWS_SECRET_ACCESS_KEY` | Used alongside the `AWS_ACCESS_KEY_ID` for secure AWS authentication.                 | `wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY`     |
| `BUCKET_TF_STATE`     | The name of the AWS S3 bucket used to store Terraform state files.                      | `my-terraform-bucket`                          |
| `REGISTRY`            | The AWS ECR registry URL where Docker images are stored.                               | `123456789012.dkr.ecr.us-east-1.amazonaws.com` |
| `SONAR_ORGANIZATION`  | Identifies the organization in SonarCloud where the project is hosted.                  | `my-sonar-org`                                 |
| `SONAR_PROJECT_KEY`   | The unique key of your SonarCloud project.                                              | `vproapp0100`                                  |
| `SONAR_TOKEN`         | Authentication token for accessing SonarCloud services.                                 | `a12b34c56d78e9f01g2h34i567j89k01`            |
| `SONAR_URL`           | The base URL for SonarCloud.                                                           | `https://sonarcloud.io`                        |

### How to Add Secrets to Your Repository

Follow these steps to configure the secrets:

1. Go to your GitHub repository.
2. Navigate to **Settings** > **Secrets and variables** > **Actions**.
3. Click **New repository secret** for each secret listed above.
4. Enter the **Name** (e.g., `AWS_ACCESS_KEY_ID`) and its corresponding **Value**.
5. Save the secret.

### Note for Collaborators

If you fork or clone this repository, ensure that you add the above secrets to your forked repository to successfully run the workflows. Without these secrets, the workflow will fail during execution. Each secret must be set up with valid credentials or tokens specific to your environment.

For more details about setting up secrets in GitHub Actions, refer to the [official GitHub documentation](https://docs.github.com/en/actions/security-guides/encrypted-secrets).




