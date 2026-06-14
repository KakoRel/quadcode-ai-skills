---
name: Flow Builder
alias: flow_builder
description: Designs multi-agent AI workflows by asking structured questions and outputting ready-to-run workflow specs with agent roles, tools, data flow, and prompt templates.
type: skills: quadcode.ai
subtype: workflow
tags: workflow, multi-agent, automation, architecture, ai
author: Archy
---

## Purpose

Designs production-ready multi-agent AI workflows. This skill asks structured discovery questions, then outputs a complete workflow specification including agent role definitions, tool assignments, data flow diagrams, prompt templates, and error handling strategies.

Target users: Developers, product managers, and AI enthusiasts who need to automate complex multi-step tasks with coordinated AI agents.

## Use When

- You need to design a workflow involving multiple AI agents working together
- You have a complex multi-step task that requires coordination between different AI capabilities
- You need a formal workflow specification to hand off to an implementation team
- You're building a new agent-based automation pipeline and need architecture guidance
- You need to document existing workflow logic for maintenance or scaling

## Do Not Use When

- The task can be handled by a single agent with one well-defined prompt
- You're looking for a code implementation rather than a workflow design
- The workflow requires real-time human-in-the-loop decision making at every step
- You need a final production deployment (this produces the spec, not the running system)
- The domain is high-risk (medical diagnosis, financial trading, autonomous vehicles) without human oversight built in

## Inputs

**Required:**
- **Goal**: What the workflow must accomplish (1-3 sentences)
- **Input format**: What data the workflow starts with (file types, API payloads, user input formats)

**Optional:**
- **Constraints**: Budget, latency requirements, allowed tools, excluded approaches
- **Existing components**: Agents, prompts, or tools you already have
- **Scale estimates**: Expected volume of requests, concurrent users
- **Team context**: Who will maintain and operate the workflow
- **Reference examples**: Similar systems or workflows to draw from

## Rules

1. **Start with discovery** — always ask structured questions before designing
2. **One agent, one responsibility** — each agent should have a clear, non-overlapping role
3. **Design for failure** — every workflow step must have a defined error path
4. **Traceability** — all decisions must be documented with rationale
5. **Prompt templates must be complete** — include system prompt, user prompt format, and expected output schema
6. **Data contracts between agents** — specify exact data format each agent expects and produces
7. **Escape hatches** — define what happens when quality checks fail or timeouts occur
8. **Keep it composable** — design agents that can be reused across workflows
9. **Cost-aware design** — note expected token usage and API costs per workflow run
10. **Version the spec** — include a version field and changelog in the output

## Workflow

### Phase 1: Discovery (always execute)

1. **Clarify the goal** — ask: "What is the end-to-end task this workflow should automate? What does success look like?"
2. **Map the input → output** — ask: "What data does the workflow receive? What is the final deliverable?"
3. **Identify bottlenecks** — ask: "What parts of this task are currently slow, error-prone, or manual?"
4. **Elicit constraints** — ask about: budget, latency, scale, security, compliance
5. **Confirm scope** — restate understanding and get sign-off before proceeding

### Phase 2: Agent Design

1. **Decompose the workflow** — break the task into sequential and parallel steps
2. **Define agents** — for each step, define:
   - Agent name and role
   - System prompt (full prompt template)
   - Input data contract (schema/format)
   - Expected output (schema/format)
   - Tools the agent can use
3. **Assign agent types** — map each agent to the appropriate Quadcode.ai skill type:
   - `tools: designer` — for visual generation tasks (delegate to Lumi)
   - `tools: motion designer` — for video/sound generation (delegate to Sonic)
   - `skills: quadcode.ai` — for workflow logic and decision agents
   - `skills: product` — for product/UX analysis agents
   - `skills: gamedev` — for game design agents
4. **Design handoffs** — define how data passes between agents (triggers, queues, direct calls)

### Phase 3: Tool Selection

1. **Identify tool needs** — per agent, list what tools are needed (search, generation, analysis, transformation)
2. **Map to Quadcode.ai capabilities** — use `ToolGetTemplates` to find matching templates for each tool need
3. **Document tool specs** — for each tool, note: alias, input requirements, output format, cost implications

### Phase 4: Prompt Engineering

1. **Write system prompts** — define the role, constraints, and style for each agent
2. **Define user prompt templates** — create the input structure each agent receives
3. **Define output schemas** — specify what each agent must return (JSON schemas preferred)
4. **Add few-shot examples** — include 1-2 examples per agent for complex tasks

### Phase 5: Error Handling & Quality

1. **Define validation gates** — after each agent output, specify quality checks
2. **Design retry logic** — for each failure mode, define: retry count, backoff strategy, escalation path
3. **Plan circuit breakers** — define conditions that halt the workflow and notify a human
4. **Add logging requirements** — specify what to log at each step for debugging and monitoring

### Phase 6: Output Assembly

1. **Compile the workflow spec** — produce the final document with all sections
2. **Include a decision log** — document why each design choice was made
3. **Add deployment notes** — infrastructure needs, environment variables, secrets management
4. **Suggest iteration plan** — what to test first, how to validate, rollout strategy

## Validation

- The goal is clearly stated and scoped
- Every agent has a single, well-defined responsibility
- Data contracts are specified for every agent handoff
- Error handling exists for every step (not just success paths)
- Prompt templates are complete and would work if copy-pasted
- Tool selections reference real Quadcode.ai template aliases
- Cost estimates are included for cloud API calls
- A human review gate is included for critical decisions
- The spec includes a version number and changelog
- A non-technical stakeholder could understand the workflow flow

## Output

A complete workflow specification document containing:

1. **Workflow Overview**: Goal, inputs, outputs, high-level flow diagram (ASCII or Mermaid)
2. **Agent Definitions**: Table of all agents with role, type, assigned tools
3. **Detailed Agent Cards**: Per agent — system prompt, user prompt template, output schema, tools, validation rules
4. **Data Flow Map**: How data moves between agents, including parallel paths
5. **Error Handling Matrix**: Table of failure modes → retry strategy → escalation path
6. **Cost Analysis**: Expected token usage, API costs, total per-run estimate
7. **Deployment Requirements**: Infrastructure, secrets, environment variables
8. **Changelog & Version**: Version history and iteration notes
