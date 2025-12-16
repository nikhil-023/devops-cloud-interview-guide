# Terraform State File

Terraform must store the state of your managed infrastructure and configuration. Terraform uses this state to map real-world resources to your configuration, track information, and boost efficiency for huge infrastructures. This state is stored by default in a local file named "terraform.tfstate".
Terraform uses the state to decide which infrastructure changes to make. Terraform does a refresh before any operation to update the state with the actual infrastructure. Bindings between resources declared in your configuration and objects in a remote system are mostly stored in the Terraform state. When Terraform generates a remote object in reaction to a configuration change, it records the identification of that remote object against a specific resource instance. Later, in response to subsequent configuration changes, Terraform may update or delete that object.

# Terraform State File Structure
Terraform state files contain each and every detail of any resources along with their current status whether it is "ACTIVE", "DELETED" or "PROVISIONING" etc.

here is a sample example of a compartment resources state file

"module": "module.compartments",
      "mode": "managed",
      "type": "oci_identity_compartment",
      "name": "test_compartment",
      "provider": "provider[\"registry.terraform.io/hashicorp/oci\"]",
      "instances": [
        {
          "schema_version": 0,
          "attributes": {
            "compartment_id": "compartment_id",
            "defined_tags": {
              "Oracle-Tags.CreatedBy": "user_id",
              "Oracle-Tags.CreatedOn": "2023-05-24T10:25:53.737Z"
            },
            "description": "Compartment for testing ",
            "enable_delete": null,
            "freeform_tags": {},
            "id": "compartment_id",
            "inactive_state": null,
            "is_accessible": true,
            "name": "test",
            "state": "ACTIVE",
            "time_created": "2023-05-24 10:25:53.87 +0000 UTC",
            "timeouts": null
          },
          "sensitive_attributes": [],
          "private": " ",
          "dependencies": [
            "module.compartments.data.oci_identity_tenancy.tenancy",
          ]
        }
      ]


# Storing Terraform State Files
By default, Terraform saves state files locally in the directory where you run it. This is fine for personal projects or testing, but when working in teams or using automation tools (like CI/CD pipelines), storing state locally becomes a problem. In team environments, multiple people need to access the state file, and automation needs to read and write it as well.

To solve this, it's better to store the state file remotely instead of on your local machine. Services like Azure Storage Accounts or Amazon S3 buckets work well for this purpose. Remote storage ensures that the state file is accessible to everyone who needs it, while allowing you to control permissions.

Here’s an example of how to configure a remote backend using Azure:

terraform {
  backend "azurerm" {
    resource_group_name  = "terraform-rg"
    storage_account_name = "terraformsa"
    container_name       = "terraformstate"
    key                  = "terraform.tfstate"
  }
}

It’s important not to store state files in source control because they might contain sensitive data, like secrets. You can use services like Azure Key Vault to keep secrets secure. Version control systems don’t allow locking files, which means people might overwrite each other’s work when accessing the state file. Using a remote backend resolves this by supporting file locks, automatic loading, encryption, and versioning. Plus, it's typically inexpensive.

# Organizing and Isolating State Files
To reduce risk and make it easier to manage your infrastructure, it’s best to isolate your state files. If everything is in a single state file, a change to one resource could unintentionally affect others.

A better approach is to use separate state files for different parts of your infrastructure, or different environments. For example, you might want separate state files for development, testing, and production. Here’s how you could organize state files in Azure Storage:

terraformstate
  --development
    --webapp.tfstate
    --sqldb.tfstate
    --vnet.tfstate
  --UAT
    --webapp.tfstate
    --sqldb.tfstate
    --vnet.tfstate
  --production
    --webapp.tfstate
    --sqldb.tfstate
    --vnet.tfstate

Each environment and resource has its own state file, so changes to one environment won’t affect another. For example, the backend configuration for a web app in the development environment would look like this:

terraform {
  backend "azurerm" {
    resource_group_name  = "terraform-rg"
    storage_account_name = "terraformsa"
    container_name       = "terraformstate"
    key                  = "development/webapp.tfstate"
  }
}

# Using Workspaces for Isolation
Another way to manage state files is through Terraform workspaces. Workspaces allow you to quickly isolate environments, though they’re not meant for use in production. Each workspace has its own state file. When you create a new workspace, Terraform sets up a directory to store the state file for that workspace.

Here’s how to use workspaces:

Create a new workspace:

$ terraform workspace new development
Created and switched to workspace "development"!
Switch between workspaces:

$ terraform workspace new stage
Created and switched to workspace "stage"!

$ terraform workspace new prod
Created and switched to workspace "prod"!

Define variables based on the selected workspace

locals {
  cidr_block = terraform.workspace == "dev" ? "10.0.0.0/16" : terraform.workspace == "stage" ? "11.0.0.0/16" : "12.0.0.0/16"
}

output "cidr_block" {
  value = local.cidr_block
}
Switch to a workspace and apply changes:

$ terraform workspace select dev
Switched to workspace "dev".

$ terraform apply
By using workspaces, Terraform will keep separate state files for each environment. You can list your workspaces with:

$ terraform workspace list
* dev
  stage
  prod
This makes it easy to manage separate environments without accidentally changing something you didn’t mean to. You can isolate your work and keep environments clean.