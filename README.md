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

graph TB
    subgraph "Client Layer"
        CLIENTS[API Clients]
    end
    
    subgraph "DNS & Load Balancing"
        ROUTE53[Route 53]
        DOMAIN[Custom Domain]
    end
    
    subgraph "API Gateway - Blue Environment"
        APIGW_BLUE[API Gateway Blue]
        STAGE_BLUE[Production Stage]
        DEPLOY_BLUE[Blue Deployment]
    end
    
    subgraph "API Gateway - Green Environment"
        APIGW_GREEN[API Gateway Green]
        STAGE_GREEN[Staging Stage]
        DEPLOY_GREEN[Green Deployment]
        CANARY[Canary Deployment]
    end
    
    subgraph "Backend Services"
        LAMBDA_BLUE[Lambda Blue]
        LAMBDA_GREEN[Lambda Green]
    end
    
    subgraph "Monitoring & Control"
        CW[CloudWatch]
        ALARMS[CloudWatch Alarms]
        METRICS[Custom Metrics]
    end
    
    CLIENTS --> ROUTE53
    ROUTE53 --> DOMAIN
    DOMAIN --> APIGW_BLUE
    DOMAIN --> APIGW_GREEN
    
    APIGW_BLUE --> STAGE_BLUE
    STAGE_BLUE --> DEPLOY_BLUE
    DEPLOY_BLUE --> LAMBDA_BLUE
    
    APIGW_GREEN --> STAGE_GREEN
    STAGE_GREEN --> DEPLOY_GREEN
    STAGE_GREEN --> CANARY
    DEPLOY_GREEN --> LAMBDA_GREEN
    CANARY --> LAMBDA_GREEN
    
    APIGW_BLUE --> CW
    APIGW_GREEN --> CW
    CW --> ALARMS
    CW --> METRICS
    
    style APIGW_BLUE fill:#4A90E2
    style APIGW_GREEN fill:#7ED321
    style CANARY fill:#F5A623
    style ALARMS fill:#D0021B




