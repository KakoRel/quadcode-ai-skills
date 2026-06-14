# Quadcode.ai Skills — Flow Builder & Campaign Kit

Two production-ready skills for the Quadcode.ai platform. Each skill gives an AI agent a structured methodology to complete a complex task — from designing multi-agent workflows to generating full marketing campaigns.

---

## Skills

### 🔧 Skill 1: Flow Builder

**What it does**: Designs production-ready multi-agent AI workflows. You describe what you want to automate — the skill asks the right questions and outputs a complete workflow specification: agent roles, data flow, prompt templates, error handling, and cost estimates.

**Best for**: Developers, product managers, and AI enthusiasts who need to design and document agent-based automation pipelines.

**How to use**:
1. Load the skill: `ToolGetTemplateContent(alias="flow_builder")`
2. Tell the agent your goal — e.g. *"I need an AI tutoring system for algebra"*
3. Answer the discovery questions (goal, inputs, constraints, scale)
4. Receive a complete workflow spec document

**Example output**: A 4-agent tutoring workflow with diagnostic, lesson planning, content generation (delegated to Lumi), and quiz agents — estimated cost $0.007/session, latency ~3.5s.

**Assigned agent**: Archy (Senior Developer)

---

### 🎨 Skill 2: Campaign Kit

**What it does**: Generates a complete marketing campaign from a single brief — copy, images, video, and sound. Delegates image generation to Lumi and video/audio to Sonic, then assembles everything into a ready-to-use asset package.

**Best for**: Marketers, startup founders, and designers who need fast multi-channel campaign production.

**How to use**:
1. Load the skill: `ToolGetTemplateContent(alias="campaign_kit")`
2. Provide your campaign brief — product, audience, channels, brand guidelines
3. The skill generates copy, then delegates visuals to Lumi and video/sound to Sonic
4. Receive a full asset manifest with all files organized by channel

**Example output**: 10 assets for a coffee brand launch — 5 images, 1 Instagram Reel (15s), 1 soundtrack (30s), 3 copy variants — total cost ~$0.10.

**Assigned agents**: Lumi (Designer) for images, Sonic (Motion Designer) for video & sound

---

## Repository Structure

```
quadcode-ai-skills/
├── README.md                                     # This file
├── skill_1_flow_builder/
│   ├── SKILL.md                                  # Skill definition (load this)
│   ├── description.md                            # One-line catalog description
│   ├── architecture.md                           # How the skill works internally
│   ├── edge_cases.md                             # Known failure modes & fixes
│   ├── examples/
│   │   ├── example_1_tutoring_app.md             # AI tutoring workflow example
│   │   └── example_2_designer_marketplace.md     # Designer matching workflow example
│   └── evals/
│       ├── evaluation_criteria.md                # How to score skill output quality
│       └── iteration_notes.md                    # Version history & known issues
└── skill_2_campaign_kit/
    ├── SKILL.md                                  # Skill definition (load this)
    ├── description.md                            # One-line catalog description
    ├── architecture.md                           # How the skill works internally
    ├── edge_cases.md                             # Known failure modes & fixes
    ├── examples/
    │   └── example_1_coffee_brand.md             # Coffee brand campaign example
    └── evals/
        ├── evaluation_criteria.md                # How to score skill output quality
        └── iteration_notes.md                    # Version history & known issues
```

---

## Quick Start

Skills live in the `skills/` directory of a Quadcode.ai project:

```
skills/
├── flow_builder/
│   └── SKILL.md
└── campaign_kit/
    └── SKILL.md
```

**Discover skills:**
```
ToolGetTemplates(type="skills: quadcode.ai")
```

**Load a skill:**
```
ToolGetTemplateContent(alias="flow_builder")
ToolGetTemplateContent(alias="campaign_kit")
```

---

## Skill Format

Both skills follow the standard `create_skill` specification:

| File | Purpose |
|------|---------|
| `SKILL.md` | YAML frontmatter + full skill body (Purpose, Inputs, Rules, Workflow, Output) |
| `description.md` | Short 1-2 sentence catalog description |
| `architecture.md` | Technical design and internal logic |
| `edge_cases.md` | Failure modes with detection, severity, and resolution steps |
| `examples/` | End-to-end examples showing real inputs → outputs |
| `evals/` | Scoring rubric and iteration history |

---

## Example Results

| Skill | Input | Output |
|-------|-------|--------|
| Flow Builder | "AI algebra tutor, $0.10/session budget, 10K users" | 4-agent workflow spec, Mermaid diagram, cost model, error matrix |
| Campaign Kit | "Summit Roast coffee, Instagram + email + web" | 5 images (Lumi), 1 video + 1 soundtrack (Sonic), full copy deck, asset manifest |

---

## Author

Built by Archy — Senior Developer & Skills Engineer, Quadcode.ai
