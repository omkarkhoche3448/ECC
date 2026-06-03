---
description: Run competitive intelligence analysis — competitor deep dives, market positioning, pricing intel, and strategic recommendations.
---

# Competitive Analysis Command

This command invokes the **competitive-analyst** agent with the **competitive-intelligence** skill to produce actionable business intelligence.

## What This Command Does

1. **Understand your product** - Read project docs to grasp what you're building
2. **Research competitors** - Web search for competitor data, pricing, positioning
3. **Analyze the landscape** - Apply frameworks (SWOT, Porter's, positioning maps)
4. **Deliver recommendations** - Prioritized strategic moves tied to profitability

## Usage

```
/competitive-analysis [target]
```

### Examples

```
/competitive-analysis Analyze our top 3 competitors
/competitive-analysis Should we enter the enterprise market?
/competitive-analysis How should we price our Pro tier vs competitors?
/competitive-analysis What are the biggest threats to our business in the next 12 months?
/competitive-analysis Compare our voice AI assistant against Siri, Alexa, and Google Assistant
```

## Analysis Modes

### Quick Brief (default for 1-2 competitors)
- Competitor snapshot
- Key differentiators
- Top 2 recommended actions
- Delivery: ~5 minutes

### Full Market Analysis (3+ competitors or "landscape")
- Complete landscape map
- Per-competitor deep dives
- SWOT with actions
- Five forces assessment
- Prioritized strategy
- Delivery: ~15 minutes

### Strategic Decision Brief (when asking "should we...")
- Options with pros/cons
- Competitive implications
- Profitability analysis
- Go/no-go recommendation
- Delivery: ~10 minutes

### Pricing Intelligence (when asking about pricing)
- Competitor pricing matrix
- Packaging comparison
- Pricing model recommendations
- Revenue impact estimates
- Delivery: ~10 minutes

## Integration with Other Commands

After competitive analysis:
- Use `/ecc:plan` to plan implementation of strategic recommendations
- Use `/ecc:multi-plan` for multi-model collaborative planning
- Use `investor-materials` skill to update pitch deck with competitive positioning
- Use `market-research` skill for deeper market sizing

## Related

- **Agent**: `competitive-analyst` (`~/.claude/agents/competitive-analyst.md`)
- **Skill**: `competitive-intelligence` (`~/.claude/skills/competitive-intelligence/SKILL.md`)
- **Skill**: `market-research` (for TAM/SAM/SOM and market sizing)
- **Skill**: `investor-materials` (for competitive slides in pitch decks)
