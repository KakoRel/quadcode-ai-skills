---
name: Campaign Kit
alias: campaign_kit
description: Generates complete marketing campaign assets — copy, visuals, video clips — using Quadcode.ai's generative capabilities. Delegates image gen to Lumi, video/sound to Sonic.
type: skills: quadcode.ai
subtype: marketing
tags: marketing, campaign, copywriting, image-generation, video, sound, social-media
author: Archy
---

## Purpose

Generates complete marketing campaign assets in a single workflow. Takes a campaign brief (product, audience, channels, tone) and produces: campaign copy (headlines, body, CTAs), visual assets (images, banners), and motion assets (video clips, sound effects/music). Delegates image generation to Lumi (via `tools: designer`) and video/sound generation to Sonic (via `tools: motion designer`).

Target users: Marketers, designers, startup founders who need fast campaign production across multiple channels.

## Use When

- You need a full campaign asset pack: copy + images + video + sound
- You have a clear campaign brief or product description
- You need multi-channel assets (social, web, email, print) in a unified style
- You're running A/B tests and need multiple creative variations
- You need rapid iteration on campaign concepts before investing in production

## Do Not Use When

- You only need one asset type (use a specialized skill instead)
- You don't have a clear campaign direction or brand guidelines
- The campaign involves user-generated content moderation
- You need real-time campaign performance optimization (this is a generation skill, not an analytics skill)
- You have strict compliance requirements you can't articulate upfront (medical, financial, legal advertising)

## Inputs

**Required:**
- **Campaign brief**: Product/service name, description, target audience, campaign goal
- **Brand guidelines** or style direction: Colors, fonts, tone of voice, visual style
- **Channels**: Where the campaign will run (social, web, email, print, video)
- **Deliverable list**: What assets are needed (e.g., "3 social posts, 1 hero image, 1 video ad, 2 email variants")

**Optional:**
- **Reference examples**: Previous campaigns, competitor ads, mood references
- **Constraints**: Budget for asset generation, resolution requirements, format requirements
- **Deadlines**: When each asset type is needed
- **Existing assets**: Logos, product photos, brand imagery to incorporate

## Rules

1. **Always start with a unified creative brief** — all assets must share a common campaign concept
2. **Delegate correctly** — Lumi handles all visual/image tasks ([`tools: designer`]), Sonic handles all video/sound tasks ([`tools: motion designer`])
3. **Style consistency** — all visual assets must reference the same brand guidelines
4. **Copy + visual alignment** — text and imagery must reinforce the same message
5. **Platform-aware sizing** — generate assets in correct aspect ratios for each channel
6. **Accessibility basics** — ensure text contrast, readable font sizes, alt-text descriptions
7. **Legal disclaimer space** — leave room for required disclaimers per channel
8. **Version labeling** — each output asset should have a descriptive filename and variant tag
9. **Asset manifest** — produce a complete list of all generated assets with specs
10. **Cost tracking** — log generation costs per asset type

## Workflow

### Phase 1: Campaign Strategy

1. **Clarify the campaign goal** — awareness, conversion, engagement, or retention?
2. **Define the audience** — demographics, pain points, channel preferences
3. **Set the creative direction** — one-line concept, key message, CTA strategy
4. **Choose the tone** — professional, playful, urgent, inspirational, authoritative
5. **Confirm brand alignment** — check guidelines for colors, fonts, logo usage, voice

### Phase 2: Copy Creation

1. **Write campaign headlines** — 5-10 options per channel (social, email, web, print)
2. **Write body copy** — long-form (email, blog) and short-form (social, ad)
3. **Define CTAs** — per channel, with action-oriented language
4. **Review against brand voice** — ensure tone consistency

### Phase 3: Visual Asset Generation (→ Lumi)

1. **Describe the visual direction** — scene, composition, color palette, mood
2. **Prepare image prompts** — structured for Lumi's image generation capabilities
3. **Specify formats** — per channel: social post sizes, hero banners, email headers
4. **Send to Lumi** — use ToolRequestHelp with agent_name="Lumi" for image generation
5. **Review and iterate** — check brand compliance, readability, composition

### Phase 4: Motion Asset Generation (→ Sonic)

1. **Describe motion direction** — animation style, pacing, transitions
2. **Prepare video prompts** — structured for Sonic's video/sound generation
3. **Specify video formats** — aspect ratio, duration, resolution per channel
4. **Specify sound needs** — background music style, SFX, voiceover requirements
5. **Send to Sonic** — use ToolRequestHelp with agent_name="Sonic" for video/sound generation
6. **Review and iterate** — check timing, quality, brand alignment

### Phase 5: Assembly & Delivery

1. **Compile asset manifest** — list all generated assets with filenames, formats, specs
2. **Package per channel** — group assets by distribution channel
3. **Add usage notes** — platform-specific instructions, legal disclaimer placement
4. **Provide iteration plan** — what to A/B test, which assets to refine

## Validation

- All copy aligns with brand voice guidelines
- Visual assets reflect the same campaign concept as the copy
- Aspect ratios match target platform requirements
- Video duration is within platform limits
- Sound quality is clear, no distortion
- File formats are appropriate for each channel
- Asset manifest is complete with all specs
- Cost tracking is included
- Legal disclaimer space is accounted for
- Files are properly named with variant tags

## Output

A complete campaign asset package containing:

1. **Campaign Brief**: Strategy document with goal, audience, creative direction, tone
2. **Copy Deck**: Headlines, body copy, CTAs per channel (in markdown table or doc)
3. **Visual Assets**: Generated images/banners (delegated to Lumi)
4. **Motion Assets**: Generated videos and sound (delegated to Sonic)
5. **Asset Manifest**: Complete inventory with filenames, formats, dimensions, file sizes
6. **Cost Report**: Generation costs per asset type, total campaign cost
7. **Usage Guide**: Platform-specific notes, legal placement, A/B test recommendations
