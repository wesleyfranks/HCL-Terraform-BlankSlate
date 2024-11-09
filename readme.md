
# Terraform Infrastructure Project

This project uses Terraform to provision and manage infrastructure in a modular, scalable, and environment-specific structure. The setup is adaptable across various cloud providers, supporting multi-environment configurations like Development and Production.

## Review Folders and Files Prior to cloning

## Project Structure

```
├── main.tf                    # Root configuration file for the infrastructure
├── provider.tf                # Provider configurations (e.g., AWS, Azure, GCP)
├── variables.tf               # Input variables for the root module
├── outputs.tf                 # Output values for the root module
├── terraform.tfvars           # Root-level values for input variables
├── modules/                   # Modular components of the infrastructure
│   ├── network/               # Network resources (e.g., VPC, subnets)
│   │   ├── main.tf            # Networking module resources
│   │   ├── variables.tf       # Module variables for networking
│   │   └── outputs.tf         # Module outputs
│   ├── compute/               # Compute resources (e.g., VM instances)
│   │   ├── main.tf            # Compute module resources
│   │   ├── variables.tf       # Module variables for compute resources
│   │   └── outputs.tf         # Module outputs
│   └── storage/               # Storage resources (e.g., S3, Blob storage)
│       ├── main.tf            # Storage module resources
│       ├── variables.tf       # Module variables for storage
│       └── outputs.tf         # Module outputs
└── env/                       # Environment-specific configurations
    ├── dev/                   # Development environment
    │   ├── main.tf            # Dev environment resources
    │   ├── variables.tf       # Variables specific to the dev environment
    │   └── terraform.tfvars   # Values for dev environment variables
    └── prod/                  # Production environment
        ├── main.tf            # Prod environment resources
        ├── variables.tf       # Variables specific to the prod environment
        └── terraform.tfvars   # Values for prod environment variables
```

## Requirements

- **Terraform**: Version 0.14 or newer.
- **CLI for the Cloud Provider**: Ensure the CLI for the chosen provider (e.g., AWS CLI, Azure CLI, gcloud) is installed and configured with the necessary permissions.

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/wesleyfranks/HCL-Terraform-BlankSlate.git
cd HCL-Terraform-BlankSlate
```

### 2. Initialize Terraform

Run the following command to install the required provider plugins:

```bash
terraform init
```

### 3. Configure Variables

Set values for the input variables by updating `terraform.tfvars` in each environment folder (`env/dev/terraform.tfvars` for development, `env/prod/terraform.tfvars` for production), or set environment variables as needed. You can find a list of variables in `variables.tf`.

### 4. Plan the Deployment

To preview the resources that will be created, modified, or destroyed, run:

```bash
terraform plan -var-file="env/dev/terraform.tfvars"   # For Development
terraform plan -var-file="env/prod/terraform.tfvars"  # For Production
```

### 5. Apply the Configuration

To deploy the infrastructure, use:

```bash
terraform apply -var-file="env/dev/terraform.tfvars"   # For Development
terraform apply -var-file="env/prod/terraform.tfvars"  # For Production
```

## File Exclusions

Sensitive and unnecessary files are excluded from version control by default in the `.gitignore` file:

- **Local state files**: `terraform.tfstate`, `*.tfstate.*`
- **Sensitive variable files**: `terraform.tfvars`
- **Provider configurations**: `.terraformrc`, `.terraform.d`
- **Temporary and backup files**: `*.backup`
- **Lock files**: `.terraform.lock.hcl`

## Notes

- **State Management**: Terraform state files are critical and contain metadata about your infrastructure. Consider using remote backends for collaborative projects, such as AWS S3 with DynamoDB for state locking, or Azure Blob Storage.
- **Modular Structure**: Each module (e.g., `network`, `compute`, `storage`) encapsulates a specific part of the infrastructure, keeping configurations organized and reusable.
- **Environment Separation**: The environment-specific folders (`env/dev`, `env/prod`) allow you to manage configurations specific to each environment, making it easy to isolate resources.

## License

This project is licensed under the MIT License. See `LICENSE` for more details.
