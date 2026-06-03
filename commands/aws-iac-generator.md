---
description: Generate production-ready Terraform, CDK, or CloudFormation from your project architecture. Reads docker-compose, package.json, and docs to create modular AWS IaC.
---

# AWS IaC Generator Command

This command invokes the **aws-iac-generator** agent with the **aws-iac-generator** skill to produce Infrastructure-as-Code from your project.

## What This Command Does

1. **Discover architecture** - Reads docker-compose, CLAUDE.md, package.json, Dockerfiles, .env, Prisma schemas
2. **Design infrastructure** - Maps services to AWS resources (VPC, ECS/EC2, RDS, ElastiCache, S3, ALB, CloudFront)
3. **Generate IaC** - Writes modular Terraform (default), CDK, or CloudFormation files
4. **Create supporting files** - Dockerfiles, CI/CD pipelines, infra README
5. **Estimate costs** - Monthly cost breakdown for generated infrastructure

## Usage

```
/aws-iac-generator [project-path-or-options]
```

### Examples

```
/aws-iac-generator Generate Terraform for C:\Users\Abcom\Desktop\ShareX
/aws-iac-generator Generate CDK (TypeScript) for this project
/aws-iac-generator Create Terraform for a Fastify + PostgreSQL + Redis + S3 SaaS
/aws-iac-generator Add monitoring module to existing infra/
/aws-iac-generator Generate ECS Fargate deployment for this Node.js monorepo
```

## IaC Formats

### Terraform (default)
- Modular structure with 7 modules (networking, compute, database, cache, storage, cdn, monitoring)
- Environment-specific tfvars (dev/staging/prod)
- S3 + DynamoDB remote state backend
- Ready for `terraform init && terraform apply`

### AWS CDK (TypeScript)
```
/aws-iac-generator Generate CDK for [project]
```
- 5 stacks (network, compute, data, cdn, monitoring)
- TypeScript with proper types
- Ready for `cdk deploy`

### CloudFormation
```
/aws-iac-generator Generate CloudFormation for [project]
```
- Nested stacks with cross-stack references
- YAML format with parameters

## Output

After generation, you get:
1. List of every file created with descriptions
2. Exact deploy commands (`terraform init`, `terraform plan`, `terraform apply`)
3. Monthly cost estimate for the infrastructure
4. Any manual steps needed (domain verification, SSL approval)

## Integration with Other Commands

- Use `/aws-advisor` first to compare deployment options and estimate costs
- Use `/ecc:plan` to plan the migration from local to AWS
- Use `/ecc:code-review` to review generated IaC
- Use `/ecc:tdd` for infrastructure testing patterns

## Related

- **Agent**: `aws-iac-generator` (`~/.claude/agents/aws-iac-generator.md`)
- **Skill**: `aws-iac-generator` (`~/.claude/skills/aws-iac-generator/SKILL.md`)
- **Agent**: `aws-advisor` (cost estimation before generating IaC)
- **Skill**: `aws-deployment-cost` (pricing reference)
