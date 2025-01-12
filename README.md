# Prerequisites
######
- JDK 11
- Maven 3
- MySQL 8 

# Technologies 
- Spring MVC
- Spring Security
- Spring Data JPA
- Maven
- JSP
- MySQL
# Database
Here,we used Mysql DB 
MSQL DB Installation Steps for Linux ubuntu 14.04:
- $ sudo apt-get update
- $ sudo apt-get install mysql-server

Then look for the file :
- /src/main/resources/db_backup.sql
- db_backup.sql file is a mysql dump file.we have to import this dump to mysql db server
# GitOps Project (Deployment Branch)

## End to End GitOps Project

This repository contains the Terraform code to maintain VPC and EKS for the vProfile project. This `deployment` branch is used for the deployment configurations and steps necessary for deploying the project.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Prerequisites](#prerequisites)
3. [Technologies Used](#technologies-used)
4. [Database Setup](#database-setup)
5. [Installation](#installation)
6. [Usage](#usage)
7. [Contributing](#contributing)
8. [License](#license)
9. [Contact](#contact)

## Project Overview

The purpose of this project is to demonstrate an end-to-end GitOps workflow using Terraform to manage infrastructure for the vProfile project. GitOps enables continuous deployment for cloud infrastructure by using Git as the single source of truth for declarative infrastructure and applications.

## Prerequisites

- JDK 11
- Maven 3
- MySQL 8

## Technologies Used

- Spring MVC
- Spring Security
- Spring Data JPA
- Maven
- JSP
- MySQL

## Database Setup

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
        ```bash
        mysql -u <user_name> -p accounts < /src/main/resources/db_backup.sql
        ```

## Installation

To set up the project, ensure you have the required tools listed above installed, then follow these steps:

1. Clone the repository:
    ```bash
    git clone https://github.com/Ammar-Abdelhady-ai/GitOps.git
    cd GitOps
    git checkout deployment
    ```

## Usage

To apply the Terraform configurations, execute the following steps:

1. Initialize the Terraform working directory:
    ```bash
    terraform init
    ```

2. Check the formatting of the Terraform code:
    ```bash
    terraform fmt -check
    ```

3. Validate the configuration:
    ```bash
    terraform validate
    ```

4. Create an execution plan:
    ```bash
    terraform plan -out planfile
    ```

5. Apply the changes required to reach the desired state of the configuration:
    ```bash
    terraform apply -auto-approve -input=false -parallelism=1 planfile
    ```

## Contributing

Contributions are welcome! Please read the [contributing guidelines](CONTRIBUTING.md) before submitting a pull request. Note that deployment-specific changes should be tested in the `deployment` branch before being merged into the `main` branch.
## Contact

For any questions or support, please open an issue in the repository or contact the repository owner.