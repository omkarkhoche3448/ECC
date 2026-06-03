---
description: AWS deployment architecture comparison, cost estimation, and optimization plan for any project. Compares EKS vs ECS vs EC2 vs Lambda with accurate pricing.
---

# AWS Advisor Command

This command invokes the **aws-advisor** agent with the **aws-deployment-cost** skill to produce deployment architecture reports with cost breakdowns.

## What This Command Does

1. **Analyze your project** - Reads architecture docs, docker-compose, package.json to understand services
2. **Compare deployment options** - EKS vs ECS Fargate vs EC2+ECR vs Lambda vs App Runner
3. **Estimate costs** - Monthly breakdown at 3 growth phases using current AWS pricing
4. **Optimize spend** - 3-5 high-impact savings (Spot, Graviton, Savings Plans, rightsizing)
5. **Produce architecture diagram** - ASCII diagram of recommended infrastructure

## Usage

```
/aws-advisor [project-path-or-question]
```

### Examples

```
/aws-advisor Analyze C:\Users\Abcom\Desktop\ShareX for AWS deployment
/aws-advisor Compare EKS vs ECS for a Fastify + PostgreSQL + Redis + S3 SaaS app with 500 users
/aws-advisor Our AWS bill is $800/mo — find savings
/aws-advisor What's the cheapest way to deploy a Node.js API + PostgreSQL + BullMQ workers?
/aws-advisor Plan infrastructure for a file-sharing SaaS that needs BYOS (customer S3 buckets)
```

## Report Modes

### Full Deployment Report (default)
- Application profile analysis
- 2-3 deployment option comparison with pros/cons
- Monthly cost at 3 growth phases (startup, growth, scale)
- 5 cost optimizations ranked by impact
- Infrastructure diagram
- Migration path

### Cost Optimization Audit
```
/aws-advisor optimize [describe current setup]
```
- Analyzes each service for waste
- Identifies rightsizing opportunities
- Recommends Spot/Savings Plans
- Estimates total savings percentage

### Quick Cost Estimate
```
/aws-advisor estimate [describe services]
```
- Fast cost breakdown without full comparison
- Single recommended architecture
- Monthly cost range

## Integration with Other Commands

After AWS advisory:
- Use `/ecc:plan` to plan implementation of recommended infrastructure
- Use `containerize-application` skill for Docker optimization
- Use `deployment-patterns` skill for CI/CD pipeline setup
- Use `/competitive-analysis` for pricing decisions based on infrastructure costs

## Related

- **Agent**: `aws-advisor` (`~/.claude/agents/aws-advisor.md`)
- **Skill**: `aws-deployment-cost` (`~/.claude/skills/aws-deployment-cost/SKILL.md`)
- **Skill**: `deployment-patterns` (CI/CD and Docker patterns)
- **Skill**: `docker-patterns` (container optimization)
