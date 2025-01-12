# GitOps Project (Stage Branch)

## End to End GitOps Project

This repository contains the Terraform code to maintain VPC and EKS for the vProfile project. The `stage` branch is used for testing and staging changes before they are merged into the `main` branch.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Tools Required](#tools-required)
3. [Installation](#installation)
4. [Branch Workflow](#branch-workflow)
5. [Terraform State Management](#terraform-state-management)
6. [Usage](#usage)
7. [Destroying Infrastructure](#destroying-infrastructure)
8. [Contributing](#contributing)
9. [License](#license)
10. [Contact](#contact)

## Project Overview

The purpose of this project is to demonstrate an end-to-end GitOps workflow using Terraform to manage infrastructure for the vProfile project. GitOps enables continuous deployment for cloud infrastructure by using Git as the single source of truth for declarative infrastructure and applications.

The `stage` branch is specifically used for:
- Testing new features and updates.
- Staging changes before they are merged into the `main` branch.
- Validating infrastructure changes in an environment similar to production.

## Tools Required

- Terraform version 1.6.3
- AWS CLI (for managing AWS resources)

## Installation

To set up the project, ensure you have the required tools listed above installed, then follow these steps:

1. Clone the repository and checkout the `stage` branch:
    ```bash
    git clone https://github.com/Ammar-Abdelhady-ai/GitOps.git
    cd GitOps
    git checkout stage
    ```

2. Configure AWS CLI with your credentials:
    ```bash
    aws configure
    ```

## Branch Workflow

The `stage` branch follows a workflow that ensures all changes are thoroughly tested before being merged into the `main` branch. This includes:
- Code reviews and approvals.
- Automated testing and validation.
- Manual testing in a staging environment.

## Terraform State Management

This project uses an S3 bucket to store Terraform state files to enable remote state management and collaboration. Make sure you have an S3 bucket and DynamoDB table set up for state locking.
