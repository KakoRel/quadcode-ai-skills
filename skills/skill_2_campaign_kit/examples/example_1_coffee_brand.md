# Example 1: Artisan Coffee Brand Launch Campaign

## Campaign Brief

**Product**: "Summit Roast" — a premium single-origin coffee brand launching in urban markets
**Goal**: Generate awareness and pre-orders for the launch
**Target audience**: Urban professionals aged 25-45 who value quality coffee and sustainability
**Channels**: Instagram, email, website hero
**Deliverables**:
- 3 Instagram posts (image + copy)
- 1 email newsletter (header image + body copy)
- 1 website hero banner + supporting text
- 1 short brand video (15s for Instagram Reels)
- Background music for the video
- Launch announcement copy (all channels)

**Brand guidelines**:
- Colors: Primary #2D1B0E (dark brown), Secondary #C4956A (warm gold), Accent #E8D5C4 (cream)
- Fonts: Heading: Playfair Display, Body: Inter
- Tone: Warm, sophisticated, artisan
- Logo: Summit Roast wordmark with mountain peak icon

**Budget**: $2.00 for asset generation
**Deadline**: 1 week

---

## Phase 1: Campaign Strategy

```
GOAL: Generate awareness + pre-orders for Summit Roast coffee launch
AUDIENCE: Urban professionals 25-45, coffee enthusiasts, sustainability-conscious
CREATIVE DIRECTION: "From mountain peak to morning cup — the journey of exceptional coffee"
KEY MESSAGE: Single-origin excellence, sustainably sourced, crafted for the discerning palette
CTA STRATEGY: "Pre-order now — first batch limited to 500 bags"
TONE: Warm, sophisticated, artisan
BRAND CHECK: ✅ Colors/tones/fonts documented
```

---

## Phase 2: Copy Creation

### Headlines (per channel)

| Channel | Headline | Variant A | Variant B |
|---------|----------|-----------|-----------|
| Instagram | "Wake up to the peak of flavor" | "Your morning, elevated" | "From our mountain to your cup" |
| Email | "Introducing Summit Roast: Coffee from the top of the world" | "The roast that redefines your morning ritual" | — |
| Web Hero | "Summit Roast — Premium Single-Origin Coffee" | "Taste the Altitude" | — |

### Body Copy

**Email body**:
```
Subject: ☕ Introducing Summit Roast — The Peak of Coffee

Hi {first_name},

We believe great coffee starts at the source. That's why Summit Roast
is sourced from a single family farm in the highlands of Colombia,
at 1,800 meters elevation.

This isn't just coffee. It's:

🌋 High-altitude beans for a smoother, brighter taste
🌱 Sustainably farmed and fair-trade certified
📦 Small-batch roasted and shipped within 48 hours

We're launching with only 500 bags — and as a subscriber, you get
first access.

[Pre-Order Now — Limited Edition]

Yours in great coffee,
The Summit Roast Team
```

**Instagram caption template**:
```
☕ From {elevation} meters to your cup.

Summit Roast is single-origin excellence from the Colombian highlands.
Small-batch roasted. Sustainably sourced. Unforgettably smooth.

First batch: only 500 bags. Pre-order at the link in bio.

#SummitRoast #SingleOrigin #SpecialtyCoffee #SustainableCoffee
```

---

## Phase 3: Visual Assets (→ Lumi)

Using `ToolRequestHelp` with `agent_name="Lumi"` for each visual asset:

### Asset 1: Instagram Post — Product Shot
```
Prompt: Premium coffee bag on rustic wooden table, warm morning light
streaming through window, dark brown and warm gold packaging with
mountain peak logo. Style: warm, sophisticated, artisan, professional
food photography. Format: 1080×1080, JPG.
Brand colors: #2D1B0E primary, #C4956A gold accent.
```

### Asset 2: Instagram Post — Coffee Farm Scene
```
Prompt: Misty green coffee farm in Colombian highlands at sunrise,
coffee cherries on branch in foreground, warm golden light.
Style: documentary photography, warm tones, natural.
Format: 1080×1080, JPG.
```

### Asset 3: Instagram Post — Lifestyle
```
Prompt: Person in cozy sweater holding warm coffee mug, steam
rising, bookshelf background with plants. Warm morning atmosphere.
Style: lifestyle photography, warm, inviting, artisan feel.
Format: 1080×1080, JPG.
```

### Asset 4: Email Header
```
Prompt: Wide banner showing mountain peak at sunrise with coffee
beans in foreground. Warm gold and dark brown palette.
Format: 600×300 PNG.
```

### Asset 5: Website Hero Banner
```
Prompt: Full-width hero showing coffee beans spilling across the
frame with mountain silhouette in background. Warm gold and cream tones.
Text space on left side for headline.
Format: 1920×600 PNG.
```

---

## Phase 4: Motion Assets (→ Sonic)

Using `ToolRequestHelp` with `agent_name="Sonic"` for motion assets:

### Asset 6: Instagram Reel (15s)
```
Video brief:
- Duration: 15 seconds
- Format: 1080×1920 (vertical) MP4
- Scene 1 (0-3s): Coffee beans cascading in slow motion, warm lighting
- Scene 2 (3-8s): Pour-over coffee brewing, close-up of extraction
- Scene 3 (8-12s): Finished cup with steam, mountain logo overlay
- Scene 4 (12-15s): Text "Summit Roast" + "Pre-Order Now" with CTA
- Transition style: Smooth fades
- Color grade: Warm, golden tones

Sound brief:
- Background music: Acoustic guitar, warm and inviting, light percussion
- Duration: 15s with smooth loop
- Mood: Cozy morning, artisan, premium
- Additional: Natural coffee brewing sounds in background (subtle)
```

---

## Phase 5: Assembly & Delivery

### Asset Manifest

| # | Asset | Type | Channel | Format | Size | Status |
|---|-------|------|---------|--------|------|--------|
| 1 | Product Shot | Image | Instagram | 1080×1080 JPG | — | ✅ Generated |
| 2 | Farm Scene | Image | Instagram | 1080×1080 JPG | — | ✅ Generated |
| 3 | Lifestyle Shot | Image | Instagram | 1080×1080 JPG | — | ✅ Generated |
| 4 | Email Header | Image | Email | 600×300 PNG | — | ✅ Generated |
| 5 | Hero Banner | Image | Web | 1920×600 PNG | — | ✅ Generated |
| 6 | Brand Reel | Video | Instagram | 1080×1920 MP4 @30fps | — | ✅ Generated |
| 7 | BG Music | Sound | Video | MP3 320kbps | — | ✅ Generated |
| 8 | Email Copy | Text | Email | HTML | — | ✅ Generated |
| 9 | Insta Captions | Text | Instagram | Text | — | ✅ Generated |
| 10 | Web Copy | Text | Web | HTML | — | ✅ Generated |

### Cost Report

| Phase | Cost |
|-------|------|
| Copy generation (LLM) | ~$0.01 |
| Image generation (Lumi) 5× | ~$0.025 |
| Video generation (Sonic) | ~$0.05 |
| Sound generation (Sonic) | ~$0.02 |
| **Total** | **~$0.105** |

### Usage Notes

- **Instagram**: Post carousel (Product + Farm + Lifestyle) across 3 days leading to launch
- **Email**: Send on launch day with header image and pre-order link
- **Web**: Hero banner goes live on launch + supporting copy on product page
- **Reel**: Post on launch day with link in bio
- **Legal**: Add "Limited edition" disclaimer, roasting address on website
