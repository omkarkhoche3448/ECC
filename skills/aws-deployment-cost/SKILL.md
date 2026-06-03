---
name: aws-deployment-cost
description: AWS deployment architecture and cost estimation for SaaS, API, and web applications. Use when evaluating cloud deployment strategies, estimating AWS costs, comparing EKS vs ECS vs EC2 vs Lambda, optimizing cloud spend, or planning infrastructure budgets.
origin: ECC
---

# AWS Deployment & Cost Advisory

Spend less, scale more, sleep at night.

## Live Pricing Sources (Always Verify)

Before quoting any price, check these sources:

| Source | URL | Best for |
|--------|-----|----------|
| **Vantage EC2** | `https://instances.vantage.sh/` | EC2 instance comparison |
| **Vantage RDS** | `https://instances.vantage.sh/rds/` | RDS instance comparison |
| **Vantage ElastiCache** | `https://instances.vantage.sh/elasticache/` | Cache instance comparison |
| **CloudPrice** | `https://cloudprice.net/aws/ec2` | 1000+ instances, real-time pricing |
| **CloudPrice Spot History** | `https://cloudprice.net/aws/spot-history` | Spot price trends |
| **CloudBurn EC2** | `https://cloudburn.io/tools/amazon-ec2-pricing-calculator` | Side-by-side comparison |
| **CloudBurn S3** | `https://cloudburn.io/tools/amazon-s3-pricing-calculator` | S3 storage class comparison |
| **Holori Calculator** | `https://calculator.holori.com/aws` | Daily-updated prices |
| **AWS Calculator** | `https://calculator.aws/` | Official multi-service estimate |
| **Infracost** | `https://www.infracost.io/` | Terraform IaC cost in PRs |
| **OpenCost** | `https://opencost.io/` | Kubernetes cost monitoring |
| **AWS EC2 Pricing** | `https://aws.amazon.com/ec2/pricing/on-demand/` | Official EC2 prices |
| **AWS Spot Pricing** | `https://aws.amazon.com/ec2/spot/pricing/` | Official Spot prices |
| **AWS RDS Pricing** | `https://aws.amazon.com/rds/postgresql/pricing/` | Official RDS prices |
| **AWS S3 Pricing** | `https://aws.amazon.com/s3/pricing/` | Official S3 prices |
| **AWS Fargate Pricing** | `https://aws.amazon.com/fargate/pricing/` | Official Fargate prices |
| **AWS EKS Pricing** | `https://aws.amazon.com/eks/pricing/` | Official EKS prices |
| **Vantage Handbook** | `https://handbook.vantage.sh/` | Best practices per service |

## When to Activate

- choosing between EKS, ECS, EC2, Lambda, or App Runner
- estimating monthly AWS costs for a new project
- optimizing an existing AWS bill
- planning infrastructure for a SaaS product
- evaluating managed vs self-hosted services
- preparing cost projections for investors or budgets
- migrating from local Docker Compose to production AWS

## Decision Framework: Which Compute?

```
                    Is your team > 5 engineers
                    AND you have 5+ microservices
                    AND someone knows Kubernetes?
                           │
                     ┌─────┴─────┐
                     │YES        │NO
                     ▼           ▼
                   EKS      Is your traffic
                            bursty with long
                            idle periods?
                               │
                         ┌─────┴─────┐
                         │YES        │NO
                         ▼           ▼
                      Lambda/    Do you want zero
                      App Runner server management?
                                    │
                              ┌─────┴─────┐
                              │YES        │NO
                              ▼           ▼
                           ECS         EC2 + ECR
                           Fargate     (cheapest,
                           (simple,    most control)
                           auto-scale)
```

## The 80/20 Cost Rule

For most SaaS startups, 80% of AWS cost comes from 4 things:

1. **Compute** (EC2/Fargate/Lambda) — 30-40% of bill
2. **Database** (RDS/Aurora) — 20-30% of bill
3. **Data Transfer** (NAT Gateway + egress) — 10-20% of bill
4. **Storage** (S3 + EBS) — 5-15% of bill

Everything else (CloudWatch, Route 53, ACM, Secrets Manager, SES) is usually < 10%.

## Sizing Guide by User Count

### 0-1,000 Users (Startup)

| Service | Recommended | Monthly Cost |
|---------|-------------|-------------|
| API Server | 1x t4g.small (Spot) | $5 |
| Database | db.t4g.micro (RDS) | $12 |
| Cache | cache.t4g.micro (ElastiCache) | $10 |
| Storage | S3 Standard (50GB) | $1 |
| Load Balancer | ALB | $16 |
| DNS | Route 53 | $1 |
| Monitoring | CloudWatch basic | $5 |
| **Total** | | **~$50/mo** |

### 1,000-10,000 Users (Growth)

| Service | Recommended | Monthly Cost |
|---------|-------------|-------------|
| API Server | 2x t4g.medium (ASG, Spot) | $20 |
| Workers | 1x t4g.small (Spot) | $5 |
| Database | db.t4g.small (RDS Multi-AZ) | $50 |
| Cache | cache.t4g.small (ElastiCache) | $24 |
| Storage | S3 Intelligent-Tiering (500GB) | $12 |
| CDN | CloudFront (100GB/mo) | $9 |
| Load Balancer | ALB | $22 |
| Queue | SQS or self-hosted Redis | $0-5 |
| Monitoring | CloudWatch + alarms | $15 |
| **Total** | | **~$160/mo** |

### 10,000-100,000 Users (Scale)

| Service | Recommended | Monthly Cost |
|---------|-------------|-------------|
| API Server | 3x m7g.large (ASG, mix Spot+OD) | $120 |
| Workers | 2x c7g.medium (Spot) | $30 |
| Database | db.r7g.large (RDS Multi-AZ + read replica) | $500 |
| Cache | cache.r7g.large (ElastiCache cluster) | $200 |
| Storage | S3 IT (5TB) + lifecycle rules | $80 |
| CDN | CloudFront (1TB/mo) | $85 |
| Load Balancer | ALB | $40 |
| NAT Gateway | 1x (or VPC endpoints) | $32 |
| Queue | SQS | $5 |
| Monitoring | CloudWatch + X-Ray | $50 |
| Secrets | Secrets Manager (10 secrets) | $4 |
| **Total** | | **~$1,150/mo** |

## Top 10 Cost Optimizations (Ranked by Impact)

### 1. Graviton Instances — Save 20%
Use `t4g`, `m7g`, `c7g`, `r7g` instead of Intel equivalents.
- Applies to: EC2, RDS, ElastiCache, Lambda
- Risk: LOW (Node.js, Python, Go all support ARM natively)
- Effort: Change instance family in config

### 2. Spot Instances for Stateless Services — Save 60-70%
Use Spot for API servers, workers, build agents.
- Applies to: EC2 ASG, ECS Fargate Spot, EKS node groups
- Risk: MEDIUM (instances can be reclaimed with 2-min warning)
- Mitigation: ASG mixed instances, Spot Fleet diversification

### 3. Reserved Instances / Savings Plans for Databases — Save 30-60%
1-year or 3-year commitments for steady-state workloads.
- Applies to: RDS, ElastiCache (Reserved), EC2 (Savings Plans)
- Risk: LOW (databases rarely change size)
- Effort: Purchase through AWS Console or API

### 4. S3 Intelligent-Tiering — Save 30-50% on Storage
Auto-moves infrequently accessed objects to cheaper tiers.
- Applies to: All S3 buckets with mixed access patterns
- Risk: NONE (no retrieval fees, automatic)
- Effort: Set as default storage class

### 5. Eliminate NAT Gateway Where Possible — Save $32+/mo
Use VPC endpoints for S3, ECR, CloudWatch, SQS, Secrets Manager.
- Applies to: Any private subnet accessing AWS services
- Risk: NONE (VPC endpoints are faster and cheaper)
- Effort: Create VPC endpoints, update route tables

### 6. CloudFront for S3 Egress — Save 40-60% on Transfer
CloudFront egress ($0.085/GB) is cheaper than S3 direct ($0.09/GB), plus caching reduces origin requests.
- Applies to: Any public file downloads
- Risk: NONE (CloudFront is also faster)
- Effort: Create distribution, point to S3 origin

### 7. Right-Size RDS — Save 20-50%
Most dev/staging databases are over-provisioned.
- Check: CloudWatch CPUUtilization, FreeableMemory, ReadIOPS
- If CPU < 20% average: downsize
- If FreeableMemory > 50%: downsize
- Risk: LOW (can resize with minimal downtime)

### 8. CloudWatch Log Retention — Save $5-50/mo
Set log retention to 30 days (default is "never expire").
- Applies to: All log groups
- Risk: NONE (export to S3 Glacier if long-term needed)
- Effort: One API call per log group

### 9. Use Aurora Serverless v2 for Variable Workloads — Save 30%
Scales from 0.5 ACU to 128 ACU. Only pay for what you use.
- Applies to: Databases with variable load (dev, staging, early SaaS)
- Risk: LOW (compatible with PostgreSQL 16)
- Effort: Create new Aurora cluster or migrate from RDS

### 10. Multi-AZ Only in Production — Save 50% on Dev/Staging
Don't run Multi-AZ RDS, ElastiCache in non-production.
- Applies to: dev, staging, QA environments
- Risk: NONE (these environments don't need HA)
- Effort: Disable Multi-AZ in non-prod config

## Architecture Patterns

### Pattern A: Simple SaaS (EC2 + RDS)
```
Route 53 → CloudFront → ALB → EC2 (ASG, t4g) → RDS PostgreSQL
                                  ↕                    ↕
                               Redis (ElastiCache)    S3
```
Best for: 1-3 services, < 10K users, cost-sensitive.

### Pattern B: Containerized SaaS (ECS Fargate)
```
Route 53 → CloudFront → ALB → ECS Fargate Services → RDS Aurora
                                  ├─ API             ↕
                                  ├─ Workers        S3
                                  └─ Cron
                                       ↕
                                    SQS + Redis
```
Best for: 3-8 services, 10K-100K users, want managed containers.

### Pattern C: Kubernetes SaaS (EKS)
```
Route 53 → CloudFront → ALB (ingress) → EKS Cluster → RDS Aurora
                                           ├─ API pods     ↕
                                           ├─ Worker pods  S3
                                           ├─ Cron pods
                                           └─ Monitoring
                                                ↕
                                          ElastiCache + SQS
```
Best for: 8+ services, 100K+ users, K8s expertise, multi-team.

## Cost Estimation Checklist

Before delivering a cost estimate:
- [ ] All services identified (compute, DB, cache, storage, CDN, DNS, monitoring)
- [ ] Data transfer estimated (ingress free, egress costs money)
- [ ] NAT Gateway included if using private subnets
- [ ] S3 request costs included (PUT/GET), not just storage
- [ ] ALB LCU costs estimated (not just base fee)
- [ ] CloudWatch log ingestion costs included
- [ ] Secrets Manager per-secret costs included
- [ ] Growth projections at 3 phases (startup, growth, scale)
- [ ] Savings from optimizations calculated separately
- [ ] All assumptions documented

## Quality Gate

Before delivering:
- [ ] cost estimate matches real AWS pricing (not outdated)
- [ ] comparison includes at least 2 deployment options
- [ ] optimizations are ranked by dollar impact
- [ ] risks and trade-offs are documented for each option
- [ ] migration path from current state is clear
- [ ] the recommendation makes a deployment decision easier
