# Flow Builder — Architecture

## Overview

The Flow Builder is a meta-skill that designs other multi-agent AI workflows. It operates as a structured design engine with six phases: Discovery → Agent Design → Tool Selection → Prompt Engineering → Error Handling → Output Assembly.

## Core Architecture Pattern

```
                     ┌─────────────────────────┐
                     │   User Input (Goal +    │
                     │   Constraints + Context) │
                     └───────────┬─────────────┘
                                 │
                                 ▼
                    ┌────────────────────────┐
                    │   Phase 1: Discovery   │
                    │   Clarify + Scope +    │
                    │   Confirm Sign-off     │
                    └───────────┬────────────┘
                                 │
                                 ▼
                    ┌────────────────────────┐
                    │   Phase 2: Agent       │
                    │   Design               │
                    │   Decompose → Define   │
                    │   → Assign → Handoff   │
                    └───────────┬────────────┘
                                 │
                    ┌────────────┼────────────┐
                    ▼            ▼            ▼
            ┌──────────┐ ┌──────────┐ ┌──────────┐
            │ Agent A  │ │ Agent B  │ │ Agent C  │
            │ (Design) │ │ (Logic)  │ │ (Motion) │
            └──────────┘ └──────────┘ └──────────┘
                    │            │            │
                    ▼            ▼            ▼
            ┌──────────────────────────────────────┐
            │  Phase 3: Tool Selection             │
            │  Template lookup + capability mapping │
            └──────────────────┬───────────────────┘
                               │
                               ▼
                    ┌────────────────────────┐
                    │  Phase 4: Prompt Eng.  │
                    │  System + User +       │
                    │  Output Schemas        │
                    └───────────┬────────────┘
                               │
                               ▼
                    ┌────────────────────────┐
                    │  Phase 5: Error         │
                    │  Handling & Quality     │
                    │  Validation gates +     │
                    │  Retry + Circuit Breaker│
                    └───────────┬────────────┘
                               │
                               ▼
                    ┌────────────────────────┐
                    │  Phase 6: Output        │
                    │  Assembly               │
                    │  Workflow Spec +        │
                    │  Decision Log + Plan    │
                    └────────────────────────┘
```

## Agent Model

Each agent in a designed workflow follows this schema:

```yaml
agent:
  name: <agent_name>
  role: <single_responsibility>
  type: <quadcode.ai_skill_type>
  assigned_to: <lumi|sonic|archy|auto>
  system_prompt: <full_prompt_text>
  user_prompt_template: <template_with_variables>
  output_schema: <json_schema_or_format_description>
  tools:
    - alias: <template_alias>
      purpose: <why_this_tool>
      inputs: <required_inputs>
      output: <expected_output>
  validation:
    - gate: <check_description>
    - retry_count: <n>
    - backoff: <linear|exponential>
    - escalation: <human_review|abort>
```

## Data Flow Design

Workflows use a directed acyclic graph (DAG) pattern:

- **Sequential agents**: Output of Agent A becomes input for Agent B
- **Parallel agents**: Independent agents run concurrently, results merge
- **Conditional branches**: Agent output determines which agent runs next
- **Feedback loops**: Agent C's output feeds back to Agent A (with circuit breaker)

## Template Integration

The skill maps tool needs to Quadcode.ai templates via `ToolGetTemplates`:

| Capability | Template Type | Example Aliases |
|------------|--------------|-----------------|
| Image generation | `tools: designer` | `design_generate_icon`, `design_build_color_script` |
| Video/sound | `tools: motion designer` | `gamedev_create_video_background` |
| Workflow logic | `skills: quadcode.ai` | Domain-specific skills |
| Analysis | `skills: product` | UX research, market analysis |
| Game design | `skills: gamedev` | Scene brief, level design |

## Cost Model

The architecture includes a cost estimation layer:

```yaml
cost_estimate:
  per_agent:
    tokens_per_call: <estimated_tokens>
    api_cost_per_call: <usd>
    avg_calls_per_run: <n>
  total_per_run:
    estimated_cost: <sum>
    estimated_tokens: <sum>
  cost_optimization:
    suggestions:
      - <cost_saving_recommendation>
```

## Error Handling Architecture

```
┌─────────────┐     Retry (n times)     ┌─────────────┐
│  Agent      │ ──────────────────────► │  Re-run     │
│  Fails      │                         │  with       │
│             │ ◄────────────────────── │  backoff    │
└──────┬──────┘     Success              └─────────────┘
       │
       │ All retries exhausted
       ▼
┌─────────────┐
│  Circuit    │
│  Breaker    │ ──► Log error ──► Notify human
│  Engaged    │ ──► Fallback: simplified path or graceful degradation
└─────────────┘
```

## Scaling Considerations

- **Stateless agents** — each agent invocation should be self-contained
- **Idempotent design** — retrying the same input must produce consistent results
- **Parallel execution** — independent agents should run concurrently where possible
- **Caching** — similar inputs should reuse cached outputs (TTL: configurable)
- **Rate limiting** — API rate limits must be considered in agent design
