# GitOps Project

## End to End GitOps Project

This repository contains the Terraform code to maintain VPC and EKS for the vProfile project.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Tools Required](#tools-required)
3. [Installation](#installation)
4. [Usage](#usage)
5. [Contributing](#contributing)
6. [License](#license)
7. [Contact](#contact)

## Project Overview

The purpose of this project is to demonstrate an end-to-end GitOps workflow using Terraform to manage infrastructure for the vProfile project. GitOps enables continuous deployment for cloud infrastructure by using Git as the single source of truth for declarative infrastructure and applications.

## Tools Required

- Terraform version ~> 1.10.3

## Installation

To set up the project, ensure you have the required tools listed above installed, then follow these steps:

1. Clone the repository:
    ```bash
    git clone https://github.com/Ammar-Abdelhady-ai/GitOps.git
    cd GitOps
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

Contributions are welcome! Please read the [contributing guidelines](CONTRIBUTING.md) before submitting a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact

For any questions or support, please open an issue in the repository or contact the repository owner.