# TaskBoard Infrastructure Deployment with Terraform

This repository contains Infrastructure as Code (IaC) written in **Terraform** to automate the deployment of the **SoftUni TaskBoard** web application and its database on Microsoft Azure.

## Architecture & Resources
The configuration provisions the following resources in Azure:
* **Resource Group** – A logical container holding all project assets.
* **App Service Plan** – A Linux-based hosting plan configured under the Free (`F1`) tier.
* **Linux Web App** – A secure web container configured to run a **.NET 6.0** stack.
* **Azure SQL Server & Database** – A relational database (`S0` standard SKU) with custom collation.
* **Firewall Rule** – Configured specifically to allow Azure internal services (like the Web App) to communicate with the database.
* **Source Control Integration** – Connects directly to a specified GitHub repository to fetch and deploy the application code on launch.

## File Structure
* `main.tf` – The core blueprint containing resource declarations and provider setups.
* `variables.tf` – Declarations for the 10 custom parameters used to customize the environment.
* `values.tfvars` *(or `terraform.tfvars`)* – The actual configuration values and secrets for the deployment variables.
* `outputs.tf` – Post-deployment indicators that dynamically expose the Web App's URL and outbound IP addresses.

## 🚀 How to Run the Project

### 1. Initialize the Directory
Download and configure the required HashiCorp Azure RM providers:
```bash
terraform init
```

### 2. Format and Validate Code
Ensure that your syntax is accurate and adheres to canonical style practices:
```bash
terraform fmt
terraform validate
```

### 3. Review the Deployment Plan
Preview what changes Terraform will execute in your cloud environment without actually applying them yet:
```bash
terraform plan -var-file="values.tfvars"
```
*(Note: If you have renamed your variable file to `terraform.tfvars`, you can omit the `-var-file="values.tfvars"` flag from all commands).*

### 4. Deploy Infrastructure
Apply the configuration to provision the entire stack in Azure:
```bash
terraform apply -var-file="values.tfvars"
```
Type `yes` when prompted. Upon completion, the console will print out the final application URL and IP addresses under the `Outputs` block.

## Clean Up & Resource Destruction
To remove all created resources permanently and prevent unexpected Azure billing, execute the destruction sequence:
```bash
terraform destroy -var-file="values.tfvars"
```
