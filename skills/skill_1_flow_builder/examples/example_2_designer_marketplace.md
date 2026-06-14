# Example 2: AI Designer Marketplace Workflow

## Scenario

A freelance marketplace wants to build an AI-powered designer matching and project management system that:
1. Takes a client's design brief
2. Analyzes the project requirements (brand, style, deliverables)
3. Matches with the best freelance designer from a pool
4. Generates a project brief, mood board, and timeline
5. Facilitates the design review cycle
6. Handles payment and delivery

**Goal**: Design a multi-agent workflow for end-to-end project management.
**Input**: Client fills out a project form with brand info, style preferences, budget, deadline
**Constraints**: Must match designers based on style compatibility, $0.20 max per project creation, 30s max for the full match+brief cycle

---

## Phase 1: Discovery

```
GOAL: Automate client-onboarding-to-designer-matching pipeline for a creative marketplace
SCOPE: Brand identity projects (logo, color palette, typography, brand guidelines)
INPUT: Client brief form + designer portfolio data (JSON)
OUTPUT: Matched designer, project brief, mood board, timeline, estimated cost
CONSTRAINTS:
  - Latency: <30s for full pipeline
  - Budget: <$0.20/project creation
  - Must handle 500+ designers in the matching pool
  - Designers must be rankable by style compatibility
SIGN-OFF: ✅ Confirmed
```

---

## Phase 2: Agent Design

### Agent 1: Brief Analyzer
```yaml
name: brief_analyzer
role: Extract structured requirements from free-form client brief
type: skills: quadcode.ai
assigned_to: auto
system_prompt: |
  You are a project brief analyst for a creative marketplace.
  Extract structured project requirements from the client's free-form input.

  Output JSON with:
  - project_type (logo/brand_identity/brand_guidelines/full_brand)
  - brand_personality: [adjectives like modern, playful, luxury]
  - color_preferences: {primary, secondary, accent, or null}
  - style_references: [urls or descriptions]
  - deliverables: [{type, quantity, format}]
  - budget_range: {min, max, currency}
  - timeline: {weeks, is_flexible}
user_prompt_template: |
  Client brief: {client_brief_text}
  Industry: {industry}
  Company description: {company_description}
output_schema: |
  { "project_type": "logo",
    "brand_personality": ["modern", "minimalist"],
    "color_preferences": {"primary": "#2C3E50", "secondary": "#3498DB", "accent": null},
    "style_references": [],
    "deliverables": [{"type": "logo", "quantity": 3, "format": "vector"}],
    "budget_range": {"min": 500, "max": 2000, "currency": "USD"},
    "timeline": {"weeks": 3, "is_flexible": true}
  }
validation:
  - gate: all required fields present
  - retry_count: 1
```

### Agent 2: Designer Matcher
```yaml
name: designer_matcher
role: Rank and recommend the best-fit designer from the pool
type: skills: quadcode.ai
assigned_to: auto
system_prompt: |
  You are a designer matching algorithm. Given:
  1. The structured brief from the Brief Analyzer
  2. The designer portfolio database

  Match designers based on:
  - Style compatibility (60% weight): Compare brand personality adjectives with
    designer's portfolio tags and self-described style
  - Past project similarity (20% weight): Projects completed in similar industries
  - Budget compatibility (10% weight): Designer rates within budget range
  - Availability (10% weight): Can meet the timeline

  Return top 3 ranked designers with match scores and rationale.
user_prompt_template: |
  Brief: {brief_json}
  Designers: {designer_pool_json}
  Output top 3: [{designer_id, name, match_score, matching_factors, portfolio_examples}]
```

### Agent 3: Mood Board Generator (Lumi)
```yaml
name: mood_board_generator
role: Generate visual mood board from brief
type: tools: designer
assigned_to: lumi
system_prompt: |
  Create a mood board for a brand identity project. The mood board should
  convey the brand personality, color palette, and design direction.
tools:
  - alias: design_build_color_script
    purpose: Generate color script/mood board from brand brief
    inputs: brand personality, color preferences, style references
    output: Mood board image composite
```

### Agent 4: Project Manager
```yaml
name: project_manager
role: Generate timeline, deliverables checklist, and milestones
type: skills: quadcode.ai
assigned_to: auto
system_prompt: |
  You are a project manager for creative projects. Given the brief, matched
  designer, and constraints, generate a project plan with:
  - Milestones with dates
  - Deliverable checklist
  - Review cycle schedule
  - Payment milestones
user_prompt_template: |
  Brief: {brief_json}
  Designer: {designer_name}, rate: {designer_rate}
  Timeline: {timeline_weeks} weeks
  Output structured project plan JSON
```

---

## Phase 3: Tool Selection

| Agent | Tool | Template Alias | Purpose |
|-------|------|---------------|---------|
| Brief Analyzer | LLM analysis | (built-in) | Extract structured data from text |
| Designer Matcher | LLM matching | (built-in) | Semantic matching algorithm |
| Mood Board Gen | Image gen | `design_build_color_script` | Generate visual mood board |
| Project Manager | LLM planning | (built-in) | Generate project timeline |

---

## Phase 4: Error Handling

```yaml
error_handling:
  no_match_found:
    condition: All designers score below 60%
    action: Expand search criteria, reduce style weight to 40%
    escalate: Flag to admin for manual matching

  mood_board_failed:
    condition: Image generation returns error
    action: Retry with simpler prompt (remove references)
    fallback: Generate text description of mood board concept

  budget_mismatch:
    condition: All designers exceed budget
    action: Suggest budget increase or reduce deliverables
    escalate: Notify client with alternatives
```

---

## Cost Analysis

```
Per project creation cost:
- Brief Analyzer: 2K tokens → $0.002
- Designer Matcher: 3K tokens → $0.004
- Mood Board: 1 image generation → $0.005
- Project Manager: 2K tokens → $0.002
Total: ~$0.013 per project (well under $0.20 budget)
```
