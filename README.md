<img src="./assets/Vault_VerticalLogo_Black_RGB.svg" alt="Vault HashiCorp logo" style="width: 450px;" align="right">

# vault-quickstarts
Vault by HashiCorp Quickstarts.

## Best Practices for Using HashiCorp Terraform with HashiCorp Vault
### Source
- The video: https://www.youtube.com/watch?v=fOybhcbuxJ0
- The source code: https://github.com/hashicorp/vault-guides

### Notes
1. It is important to find a **secure** place to store the `terraform.tfstate` file because it might contain sensitive information (e.g.: S3 AWS (encrypted)).
    ```hcl
    terraform {
     backend "S3" {
      bucket = "remote-terraform-state-best-practices-demo"
      encrypted = true
      key = "terraform.tfstate"
      region = "us-east-1"
     }
    }
    ```
2. It is a good idea that the AWS keys have a TTL.
3. `terraform init` it's pulling what is needed to execute. It also figures what it will need to do to setup the env.
4. `terraform apply` 
