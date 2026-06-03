---
name: aws-iac-generator
description: AWS Infrastructure-as-Code generation patterns. Terraform modules, CDK stacks, CloudFormation templates. Docker-compose to AWS mapping, security hardening, cost-optimized defaults. Use when generating IaC from project architecture.
origin: ECC
---

# AWS Infrastructure-as-Code Generator

Read your project. Write your infrastructure.

## When to Activate

- Generating Terraform, CDK, or CloudFormation from an existing project
- Migrating docker-compose services to AWS
- Setting up modular IaC for a new AWS deployment
- Creating environment-specific configs (dev/staging/prod)
- Adding CI/CD pipelines for infrastructure deployment

## Docker-Compose to AWS Mapping

| docker-compose | AWS Resource | Terraform Resource |
|----------------|-------------|-------------------|
| `postgres:16-alpine` | RDS PostgreSQL 16 | `aws_db_instance` |
| `redis:7-alpine` | ElastiCache Redis 7 | `aws_elasticache_cluster` |
| `minio/minio` | S3 (native) | `aws_s3_bucket` |
| `pgbouncer` | RDS Proxy | `aws_db_proxy` |
| `nginx` | ALB + CloudFront | `aws_lb` + `aws_cloudfront_distribution` |
| Service with `ports` | ECS Service + ALB TG | `aws_ecs_service` + `aws_lb_target_group` |
| Service without ports | ECS Task (worker) | `aws_ecs_service` (no LB) |
| `volumes:` (data) | EBS / S3 / EFS | `aws_ebs_volume` / `aws_s3_bucket` / `aws_efs_file_system` |
| `depends_on:` | Security groups + service discovery | `aws_security_group_rule` + `aws_service_discovery_service` |
| `healthcheck:` | ALB/ECS health check | `health_check {}` block |
| `environment:` | Secrets Manager + task def env | `aws_secretsmanager_secret` + `environment {}` |

## Terraform Module Structure

Standard modular layout for any project:

```
infra/
├── main.tf              # Provider, backend, data sources
├── variables.tf         # All input variables
├── outputs.tf           # Key outputs
├── versions.tf          # Provider version pins
├── terraform.tfvars     # Default dev values
├── environments/
│   ├── dev.tfvars
│   ├── staging.tfvars
│   └── prod.tfvars
└── modules/
    ├── networking/      # VPC, subnets, NAT, SGs, VPC endpoints
    ├── compute/         # ECS/EC2/EKS + ALB + auto-scaling
    ├── database/        # RDS + parameter groups + backups
    ├── cache/           # ElastiCache Redis
    ├── storage/         # S3 + lifecycle + CORS
    ├── cdn/             # CloudFront + Route 53 + ACM
    └── monitoring/      # CloudWatch + SNS + alarms
```

Each module contains `main.tf`, `variables.tf`, `outputs.tf`.

## CDK Stack Structure (TypeScript)

```
infra/
├── bin/app.ts
├── lib/
│   ├── network-stack.ts
│   ├── compute-stack.ts
│   ├── data-stack.ts
│   ├── cdn-stack.ts
│   └── monitoring-stack.ts
├── cdk.json
├── tsconfig.json
└── package.json
```

## Security Standards

Every generated IaC file MUST follow:

1. **No hardcoded secrets** — use `aws_secretsmanager_secret` for all credentials
2. **Private subnets** for compute and databases — only ALB in public subnets
3. **Least-privilege IAM** — no `*` actions, scope to specific resources
4. **Encryption at rest** — RDS, ElastiCache, S3, EBS all encrypted
5. **SSL/TLS everywhere** — ACM certs, RDS SSL, Redis TLS
6. **Security groups** — specific CIDR blocks, only `0.0.0.0/0` for ALB 443
7. **Access logging** — ALB logs to S3, S3 access logging enabled
8. **VPC endpoints** — for S3, ECR, CloudWatch, Secrets Manager

## Cost-Optimized Defaults

| Setting | Dev | Staging | Production |
|---------|-----|---------|------------|
| Instance family | t4g (Graviton) | t4g | m7g/c7g |
| NAT Gateway | Single | Single | Multi-AZ |
| RDS Multi-AZ | No | No | Yes |
| ElastiCache replicas | 0 | 0 | 1-2 |
| Spot instances | Workers only | Workers | Workers + some API |
| CloudWatch retention | 7 days | 14 days | 30 days |
| S3 storage class | Standard | Intelligent-Tiering | Intelligent-Tiering |
| Backup retention | 1 day | 7 days | 30 days |

## Tagging Convention

Every resource gets these tags:

```hcl
tags = {
  Name        = "${var.project}-${var.environment}-${local.resource_name}"
  Environment = var.environment
  Project     = var.project
  ManagedBy   = "terraform"
}
```

## Terraform Code Standards

- Pin provider versions: `~> 5.0` not `>= 5.0`
- All variables have `description`, `type`, and sensible `default`
- Use `locals` for computed values and naming
- Use `data` sources for AWS account ID, region, caller identity
- S3 + DynamoDB backend for remote state
- `terraform fmt` compatible formatting
- Cost comments on resources: `# ~$12/mo for db.t4g.micro`

## Environment Variable Mapping

```hcl
# From docker-compose environment to AWS:
# DATABASE_URL → constructed from RDS endpoint + Secrets Manager password
# REDIS_URL → constructed from ElastiCache endpoint
# S3_BUCKET → aws_s3_bucket.main.id
# S3_ENDPOINT → not needed (native S3)
# JWT_SECRET → aws_secretsmanager_secret
# API_KEY → aws_secretsmanager_secret
```

## Generated Supporting Files

Beyond IaC, always generate:

1. **Dockerfile** (if missing) — multi-stage, Graviton-compatible (linux/arm64), non-root user
2. **CI/CD pipeline** — `.github/workflows/deploy.yml` for Build → Test → ECR Push → Deploy
3. **infra/README.md** — prerequisites, quick start, deploy commands, cost estimate

## Quality Gate

Before delivering generated IaC:
- [ ] `terraform fmt` compatible
- [ ] `terraform validate` would pass (no syntax errors)
- [ ] All variables have descriptions and defaults
- [ ] No hardcoded secrets or IPs
- [ ] Security groups follow least-privilege
- [ ] Cost comments on expensive resources
- [ ] Environment tfvars for dev/staging/prod
- [ ] README with deploy instructions
