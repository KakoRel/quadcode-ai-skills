# Campaign Kit — Architecture

## Overview

Campaign Kit is a multi-agent campaign production pipeline. It orchestrates three core capabilities — copywriting, visual design, and motion production — by delegating to specialized agents: the core LLM (for strategy and copy), Lumi (for images), and Sonic (for video/sound).

## System Architecture

```
                    ┌─────────────────────────────┐
                    │    Campaign Brief           │
                    │  (goal, audience, brand,    │
                    │   channels, deliverables)   │
                    └──────────┬──────────────────┘
                               │
                               ▼
                    ┌─────────────────────────────┐
                    │  Phase 1: Campaign Strategy │
                    │  ┌───────────────────────┐  │
                    │  │  Core LLM (Archy)     │  │
                    │  │  - Clarify goal       │  │
                    │  │  - Define audience    │  │
                    │  │  - Creative direction │  │
                    │  │  - Tone & brand check │  │
                    │  └───────────────────────┘  │
                    └──────────┬──────────────────┘
                               │
                    ┌──────────┼──────────┐
                    ▼          ▼          ▼
            ┌──────────┐ ┌──────────┐ ┌──────────┐
            │Phase 2   │ │Phase 3   │ │Phase 4   │
            │Copy      │ │Visuals   │ │Motion    │
            │Creation  │ │(→ Lumi)  │ │(→ Sonic) │
            └────┬─────┘ └────┬─────┘ └────┬─────┘
                 │            │            │
                 ▼            ▼            ▼
            ┌──────────────────────────────────────┐
            │  Phase 5: Assembly & Delivery        │
            │  - Compile asset manifest            │
            │  - Package by channel                │
            │  - Add usage notes                   │
            │  - Cost report                       │
            └──────────────────────────────────────┘
                               │
                               ▼
                    ┌─────────────────────────────┐
                    │   Campaign Asset Package    │
                    │  (copy + images + videos    │
                    │   + sound + manifest)       │
                    └─────────────────────────────┘
```

## Agent Delegation Model

The skill acts as a campaign director, delegating specialized work to the right agents:

| Phase | Agent | Tool Used | Responsibility |
|-------|-------|-----------|----------------|
| Strategy | Core LLM (via skill) | Built-in LLM | Analyze brief, define direction |
| Copy | Core LLM (via skill) | Built-in LLM | Generate headlines, body, CTAs |
| Visuals | Lumi | `ToolRequestHelp` → Lumi | Image generation, banners, illustrations |
| Motion | Sonic | `ToolRequestHelp` → Sonic | Video clips, sound effects, background music |
| Assembly | Core LLM (via skill) | Built-in LLM | Compile manifest, package deliverables |

## Channel-Specific Asset Requirements

| Channel | Copy Length | Image Size | Video Length | Sound |
|---------|------------|------------|-------------|-------|
| Instagram Feed | 150-300 chars | 1080×1080 | 15-60s | Optional music |
| Instagram Story | 1-2 lines | 1080×1920 | 1-15s | Music + SFX |
| Facebook Feed | 150-500 chars | 1200×628 | 15-60s | Optional music |
| LinkedIn | 300-1000 chars | 1200×627 | 15-30s | Professional music |
| Twitter/X | 1-280 chars | 1200×675 | 1-10s | Not typical |
| Email | 200-2000 chars | 600×300 banner | N/A | N/A |
| Web Hero | 50-150 chars | 1920×600 | 30-90s | Background music |
| YouTube | Long form | 1280×720 | 15-180s | Full audio mix |
| Print | Varies | 300 DPI | N/A | N/A |

## Creative Brief Schema

```yaml
campaign_brief:
  campaign_name: <string>
  product: <string>
  goal: awareness | conversion | engagement | retention
  target_audience:
    demographics: <string>
    pain_points: [<string>]
    channels: [<channel>]
  creative_direction:
    concept: <one_line>
    key_message: <string>
    cta_strategy: <string>
    tone: professional | playful | urgent | inspirational | authoritative
  brand_guidelines:
    colors: {primary: <hex>, secondary: <hex>, accent: <hex>}
    fonts: {heading: <font>, body: <font>}
    voice: <description>
  deliverables:
    - type: copy | image | video | sound
      channel: <channel>
      quantity: <number>
      specs: <format_details>
  references: [<url_or_description>]
  constraints:
    budget: <usd>
    deadline: <date>
    format_requirements: [<string>]
```

## Cost Tracking Model

```yaml
campaign_cost:
  copy_generation:
    tokens_used: <number>
    cost: <usd>
  visual_generation:
    images_count: <number>
    cost_per_image: <usd>
    total_visual_cost: <usd>
  motion_generation:
    video_count: <number>
    sound_count: <number>
    cost_per_clip: <usd>
    total_motion_cost: <usd>
  total_campaign_cost: <usd>
  cost_per_channel:
    - channel: <channel>
      assets: <count>
      cost: <usd>
```

## Quality Pipeline

```
Copy → Brand Voice Check → Human Review (optional) → Approved
Image → Brand Color Check → Readability Check → Approved
Video → Length Check → Visual Quality → Sound Sync → Approved
Sound → Clarity Check → Format Check → Approved
```

Each phase logs results to the asset manifest for traceability.
