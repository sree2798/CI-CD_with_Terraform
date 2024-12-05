# CI/CD with Terraform and Azure

This project demonstrates a CI/CD pipeline for provisioning and automating infrastructure and workflows in Azure using Terraform. The pipeline provisions Azure resources, such as a Storage Account, Data Factory, and pipelines for automated data transfers, to showcase Infrastructure as Code (IaaC) principles.

---

## Table of Contents
1. [Overview](#overview)
2. [System Architecture](#system-architecture)
3. [System Requirements](#system-requirements)
4. [Setup Instructions](#setup-instructions)
5. [Project Structure](#project-structure)
6. [Terraform Modules](#terraform-modules)
7. [Usage](#usage)
8. [Validation and Debugging](#validation-and-debugging)
9. [Destroying Resources](#destroying-resources)

---

## Overview

The project provisions the following Azure resources:
- **Resource Group**
- **Azure Storage Account** with Containers and Blobs
- **Azure Data Factory** with linked services, datasets, and pipelines

It integrates Azure Blob Storage with Azure Data Factory, enabling automated data transfers using Terraform scripts.

---

## System Architecture

The system architecture diagram below illustrates the flow of data between Azure resources, showcasing the integration of Azure Storage, Data Factory, and automated pipelines:

![System Architecture](https://github.com/user-attachments/assets/be58985a-d975-4af8-a8bf-f8a8736b7a0a)


---

## System Requirements

- **Terraform**: [Install Terraform](https://developer.hashicorp.com/terraform/install)
- **Azure CLI**: [Install Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli#install-or-update)
- **Azure Subscription**: A valid Azure account with a subscription.
- **IDE**: PyCharm or any other IDE for writing and managing Terraform scripts.

---

## Setup Instructions

1. **Install Prerequisites**:
   - Install Terraform and Azure CLI as per the links in the System Requirements section.

2. **Login to Azure**:
   - Authenticate Azure CLI to your Azure subscription using:
     ```bash
     az login --tenant <TENANT_ID>
     ```

3. **Clone the Repository**:
   - Clone this repository to your local machine.

4. **Initialize Terraform**:
   - Run the following command in the root directory:
     ```bash
     terraform init
     ```

5. **Validate Configuration**:
   - Check Terraform scripts for errors:
     ```bash
     terraform validate
     ```

6. **Plan Resources**:
   - Create an execution plan using:
     ```bash
     terraform plan -var-file="variables.tfvars"
     ```

7. **Apply Changes**:
   - Provision resources by executing:
     ```bash
     terraform apply -var-file="variables.tfvars"
     ```

---

## Project Structure

- **storage_account**: Contains Terraform configuration for Storage Account, Containers, and Blobs.
- **data_factory**: Contains Terraform configuration for Data Factory, linked services, datasets, and pipelines.
- **main.tf**: Links and orchestrates the modules.
- **variables.tf**: Defines input variables.
- **variables.tfvars**: Contains variable values for deployment.

---

## Terraform Modules

### Storage Account
- Provisions Azure Storage Account.
- Creates Containers (`source` and `destination`).
- Creates a test Blob in the source container.

### Data Factory
- Provisions Azure Data Factory with system-assigned identity.
- Links to Storage Account containers (`source` and `destination`).
- Creates datasets for Blob storage.
- Sets up a Copy Data pipeline for data transfer.

---

## Usage

1. **Running the Pipeline**:
   - Execute the pipeline manually or schedule it to run daily.
   - The `source` container file (`test.txt`) is transferred to the `destination` container with a timestamped filename.

2. **Verify Outputs**:
   - Confirm resource creation in the Azure portal.
   - Validate successful data transfer by inspecting the destination container.

---

## Validation and Debugging

1. Validate scripts:
   ```bash
   terraform validate
2. Plan execution:
   ```bash
   terraform plan -var-file="variables.tfvars"
   ```
3. Debug pipeline in Azure Data Factory:
   - Open the Data Factory in the Azure portal.
   - Run the pipeline manually for debugging.

## Destroying Resources
To clean up all provisioned azure resources
```bash
   terraform destroy -var-file="variables.tfvars"
```



