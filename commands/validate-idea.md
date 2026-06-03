---
description: Brutally honest startup and SaaS idea validation. Evaluates problem validity, market demand, competition, willingness to pay, and execution complexity. Gives a GO/NO-GO verdict with evidence. Use BEFORE writing any code.
---

# Validate Idea Command

Invokes the **idea-validator** agent to evaluate whether your startup/SaaS idea is worth building — or a waste of your time.

## Usage

```
/validate-idea [describe your idea]
```

### Examples

```
/validate-idea AI-powered code review tool for React developers
/validate-idea Multi-tenant file sharing SaaS with BYOS (Bring Your Own Storage)
/validate-idea Voice AI assistant platform for customer support
/validate-idea Freelancer invoice and contract automation tool
/validate-idea Open-source alternative to Notion for developer documentation
/validate-idea Compliance automation platform for EU AI Act
```

## What It Evaluates (8 Dimensions)

| Dimension | Weight | What It Answers |
|-----------|--------|----------------|
| **Problem Validity** | 25% | Is this a real problem real people have? |
| **Solution Fit** | 15% | Does YOUR solution actually solve it? |
| **Market Size** | 15% | Are there enough paying users? |
| **Competition** | 10% | Who else does this? Can you win? |
| **Willingness to Pay** | 15% | Will people pay? How much? |
| **Founder-Market Fit** | 5% | Are YOU the right person? |
| **Timing** | 5% | Is NOW the right time? |
| **Execution Complexity** | 10% | Can you actually build and ship this? |

## Verdict Scale

| Score | Verdict | Meaning |
|-------|---------|---------|
| 8.0-10.0 | **BUILD IT NOW** | Stop researching. Ship MVP in 2 weeks. |
| 6.5-7.9 | **VALIDATE FIRST** | Promising. Run 2-3 experiments before coding. |
| 5.0-6.4 | **PIVOT THE IDEA** | Core insight has value. Current form won't work. |
| 3.5-4.9 | **SIDE PROJECT ONLY** | Not a business. Fine for learning. Don't quit your job. |
| 1.0-3.4 | **DON'T BUILD THIS** | No real problem, market, or path to revenue. |

## What You Get

1. **Honest TL;DR verdict** — no sugarcoating
2. **8-dimension scored breakdown** with evidence
3. **Top 3 risks** that could kill the idea
4. **Validation experiments** — specific tests to run before coding
5. **Pivot directions** — 3 adjacent ideas that score better
6. **Uncomfortable questions** — things you should honestly answer

## This Agent Will NOT

- Tell you "great idea!" to make you feel good
- Skip research and give you a vibe-based opinion
- Confuse "cool project" with "viable business"
- Let you spend 6 months building something nobody wants

## Recommended Workflow

```
/validate-idea [your idea]        ← Is this worth building?
/research [technical approach]    ← What already exists?
/competitive-analysis [market]    ← Who are the competitors?
/plan [MVP scope]                 ← Plan the minimum viable product
/tdd [implementation]             ← Build it
```

## For Honest Self-Assessment

Before running this command, ask yourself:
- Can I name 5 specific people who have this problem?
- Would they pay $X/month for a solution?
- What do they use today? Why is that not good enough?
- Why am I the right person to build this?

If you can't answer these, the agent will ask you.

## Related

- **Agent**: `idea-validator` (`~/.claude/agents/idea-validator.md`)
- **Command**: `/research` — deep technical research before building
- **Command**: `/competitive-analysis` — detailed competitor analysis
- **Command**: `/aws-advisor` — deployment cost estimation after validation
- **Skill**: `market-research` — market sizing and industry intelligence
