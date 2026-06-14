# Flow Builder — Evaluation Criteria

## 1. Completeness

| Criteria | Weight | Description |
|----------|--------|-------------|
| All 6 phases present | 20% | Discovery, Agent Design, Tool Selection, Prompt Engineering, Error Handling, Output Assembly |
| All agents have defined roles | 15% | No agent is missing role, type, system prompt, output schema |
| Error handling for every step | 15% | Every workflow step has defined failure handling |
| Data contracts specified | 10% | Every agent handoff has input/output schemas |

## 2. Quality

| Criteria | Weight | Description |
|----------|--------|-------------|
| Prompts are copy-paste ready | 15% | System prompts are complete and detailed enough to use directly |
| Real tool aliases used | 10% | Tool selections reference actual Quadcode.ai template aliases |
| Cost analysis is accurate | 5% | Token counts and cost estimates are reasonable |
| Edge cases covered | 10% | At least 3 edge cases are explicitly documented |

## 3. Usability

| Criteria | Weight | Description |
|----------|--------|-------------|
| Non-technical readability | - | A product manager should understand the workflow flow |
| Actionable next steps | - | Output includes deployment notes and iteration plan |
| Versioned and documented | - | Spec includes version number and decision log |

## Scoring Rubric

| Score | Meaning |
|-------|---------|
| 1 (Poor) | Missing critical sections, agents undefined, no error handling |
| 2 (Basic) | All phases present but shallow, prompts are placeholders |
| 3 (Good) | Complete spec with working prompts, real tool aliases, error handling |
| 4 (Excellent) | Production-ready spec with cost analysis, edge cases, deployment notes |
| 5 (Outstanding) | Beyond spec — includes iteration plan, monitoring setup, A/B test strategy |

## Test Suite

### Test 1: Simple Two-Agent Workflow
**Input**: "Generate a workflow that reads customer reviews and summarizes sentiment"
**Expected**: 2 agents (reader + analyzer), data contract between them, error handling for empty input
**Pass criteria**: All 6 phases present, agents have prompts, validation gates exist

### Test 2: Complex Multi-Agent with Visual Output
**Input**: "Design a workflow that takes a product brief and produces: product images, marketing copy, and a video ad"
**Expected**: 4+ agents including Lumi (images), Sonic (video), copywriter, reviewer
**Pass criteria**: Real template aliases used for image/video tools, parallel execution defined

### Test 3: Constrained Budget Scenario
**Input**: "Design a workflow for <$0.05 per run that generates social media posts"
**Expected**: Cost optimization strategies, tiered model usage, caching recommendations
**Pass criteria**: Cost analysis within budget, optimization suggestions provided
