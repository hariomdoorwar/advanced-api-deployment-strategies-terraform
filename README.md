# Advanced API Deployment Strategies - Terraform

This repository contains only the Terraform code for the Advanced API Deployment Strategies project.

## Files

- `main.tf`
- `variables.tf`
- `outputs.tf`
- `versions.tf`
- `.terraform.lock.hcl`

## Usage

1. Initialize:
   terraform init
2. Plan:
   terraform plan
3. Apply:
   terraform apply

## Notes

- This repo intentionally excludes Terraform state files and generated artifacts.
- API testing from corporate networks may require proxy/firewall allowlisting for execute-api endpoints.
