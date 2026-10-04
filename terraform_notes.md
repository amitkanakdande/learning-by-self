### Terraform command auto-complete installation

```terraform-bash
terraform install-autocomplete
```

### Terraform command auto-complete uninstall

```terraform-bash
terraform uninstall-autocomplete
```

### Terraform version

```terraform-bash
terraform version
```

## Terraform Workflow Notes

## 1. terraform init

From the existing directory, run:

```terraform-bash
terraform init
```
This command looks for any provider blocks and decides which provider binaries need to be downloaded.

Example:

```terraform-bash
# providers.tf
provider "aws" {
  region = "eu-west-1"
}
```

In this case, Terraform understands it must download the AWS provider binary.

AWS provider configuration/binaries are hosted on GitHub: hashicorp/terraform-provider-aws

Terraform downloads those binaries into the `.terraform` directory.

Resulting structure:

```terraform-bash
terraform_workspace
   └── .terraform/providers/registry.terraform.io/hashicorp/aws/6.67.0/windows_amd64
```

To upgrade to the latest provider or module versions:

```terraform-bash
terraform init -upgrade
```

## 2. terraform plan

After initialization, if you’ve written resource blocks, run:

```terraform-bash
terraform plan
```
Shows what resources will be affected:

1. `+` create
2. `~` update
3. `-` destroy

Important: `terraform plan` is a dry run. It never actually creates, updates, or deletes resources.

It compares the current state (from the state file) with the desired state (from configuration).

It refreshes the state file during the plan phase.

### 3. terraform apply

```terraform-bash
terraform apply
```
Deploys the configuration to the cloud provider.

Refreshes the state file and then takes action (create/update/destroy).

### 4. terraform destroy
```terraform-bash
terraform destroy
```
Removes all resources defined in the configuration.

## Terraform Blocks Overview

1. provider  
Connects Terraform to a cloud platform (AWS, Azure, GCP).

2. resource  
Defines infrastructure to create, update, or delete (e.g., EC2, VPC).

3. data  
Retrieves information about existing resources (e.g., AMI IDs, subnets).

4. variable  
Makes code reusable by allowing customization of values.

5. output  
Displays or shares essential information after deployment.

6. terraform  
Defines settings like required Terraform version or backend configuration.

7. module  
Groups related resources into reusable units.

8. import  
Brings existing resources under Terraform management (e.g., import an EC2 created manually).
