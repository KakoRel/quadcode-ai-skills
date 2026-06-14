# Campaign Kit — Evaluation Criteria

## 1. Completeness

| Criteria | Weight | Description |
|----------|--------|-------------|
| All 5 phases present | 20% | Strategy, Copy, Visuals, Motion, Assembly |
| Copy for all required channels | 15% | Headlines + body + CTAs per deliverable list |
| Image prompts for Lumi | 15% | Complete prompts with composition, colors, format |
| Video/sound briefs for Sonic | 15% | Complete video + sound specs |
| Asset manifest | 10% | Full inventory with filenames, formats, dimensions |

## 2. Quality

| Criteria | Weight | Description |
|----------|--------|-------------|
| Brand alignment across all assets | 10% | Colors, fonts, tone consistent throughout |
| Platform-aware formats | 10% | Correct aspect ratios and formats per channel |
| Copy quality | 10% | On-brand, actionable CTAs, no typos |
| Visual quality | 10% | Prompts are specific enough for Lumi to execute |
| Motion quality | 10% | Video direction is producible, sound brief is clear |

## 3. Production Readiness

| Criteria | Weight | Description |
|----------|--------|-------------|
| Cost tracking | 5% | Generation costs logged per asset |
| Usage guide | 5% | Platform-specific deployment instructions |
| Asset filename conventions | 5% | Descriptive filenames with variant tags |

## Scoring Rubric

| Score | Meaning |
|-------|---------|
| 1 (Poor) | Missing phases, no delegation to Lumi/Sonic, inconsistent style |
| 2 (Basic) | All phases present but prompts are too vague to execute |
| 3 (Good) | Working campaign with specific prompts, correct formats, copy-visual alignment |
| 4 (Excellent) | Production-ready — cost report, asset manifest, usage guide all included |
| 5 (Outstanding) | Beyond spec — A/B variants, platform-specific optimizations, accessibility checks |

## Test Suite

### Test 1: Simple Social Campaign
**Input**: "Instagram campaign for a new fitness app — 2 posts, 1 story"
**Expected**: 2 image prompts for Lumi, 1 video brief for Sonic (story), copy for all
**Pass criteria**: All formats correct (1080×1080, 1080×1920), brand voice consistent

### Test 2: Multi-Channel Product Launch
**Input**: "Full campaign for a SaaS product launch — email, web hero, LinkedIn, Twitter"
**Expected**: Copy for 4 channels, visual assets for 2 channels (hero + social), no motion
**Pass criteria**: Platform-specific copy lengths, correct image sizes per platform

### Test 3: Lumi/Sonic Unavailable
**Input**: Campaign brief but Lumi and Sonic both fail
**Expected**: Fallback text descriptions for all visual/motion assets
**Pass criteria**: Every asset has a text brief that a human designer could execute
