# Flow Builder — Edge Cases & Failure Modes

## Edge Case 1: Vague or Contradictory Goals

**Symptom**: User says "I want a workflow that handles everything" or describes conflicting requirements.

**Resolution**: The skill must push back with structured questions to narrow scope. If contradictions persist, document them explicitly in the spec as "open design decisions" and flag for human resolution.

**Prevention**: Phase 1 Discovery must complete with explicit sign-off before Phase 2 begins.

---

## Edge Case 2: Too Many Agents

**Symptom**: The decomposed workflow has 15+ agents, creating coordination complexity.

**Resolution**: Enforce a maximum of 8 agents per workflow. Suggest merging agents with overlapping responsibilities. If more agents are genuinely needed, design a sub-workflow pattern where groups of agents form a higher-level module.

**Rule of thumb**: If an agent's responsibility can be described in under 10 words, it's likely too granular.

---

## Edge Case 3: No Suitable Tool Exists

**Symptom**: A required capability has no matching Quadcode.ai template.

**Resolution**: Document the gap explicitly. Provide a "custom tool specification" — describe what the tool needs to do, input/output schema, and how it would integrate. Flag as "requires custom development" in the spec.

---

## Edge Case 4: Agent Output Schema Mismatch

**Symptom**: Agent A produces data in a format Agent B cannot consume.

**Resolution**: Add a "transformation step" between agents — a lightweight agent or adapter that converts formats. Document transformation logic explicitly.

**Prevention**: Define data contracts upfront during Phase 2.

---

## Edge Case 5: Latency Requirements Conflict with Agent Design

**Symptom**: User needs sub-second responses but the workflow requires 3-4 sequential LLM calls.

**Resolution**: Identify which agents can run in parallel. For sequential chains, suggest caching or pre-computation strategies. If fundamentally incompatible, document the trade-off and suggest human review.

---

## Edge Case 6: Budget Exceeded

**Symptom**: Estimated cost per workflow run exceeds user's budget by 3x or more.

**Resolution**: Offer cost optimization strategies:
- Replace expensive agents with simpler rule-based alternatives
- Add caching layers
- Reduce parallel agent count
- Use cheaper model tiers for non-critical steps
- Batch similar requests

---

## Edge Case 7: Hallucinated Agent Handoffs

**Symptom**: Workflow design assumes Agent B receives data that Agent A was never specified to produce.

**Resolution**: Cross-reference all data contracts in Phase 6 validation. Every input must have a matching output from a preceding agent. Auto-generate a "data provenance map" to verify.

---

## Edge Case 8: Security & Privacy Requirements

**Symptom**: The workflow processes PII, credentials, or proprietary data.

**Resolution**: Flag all data sensitivity concerns. Add notes about:
- Data encryption in transit and at rest
- Which agents should NOT log raw data
- Access control requirements
- Data retention policies
- Compliance considerations (GDPR, SOC2, HIPAA)

---

## Edge Case 9: Agent Prompt Bleed

**Symptom**: System prompts from different agents share context they shouldn't, or prompt injection risks emerge.

**Resolution**: Design isolation boundaries per agent. System prompts should not contain raw data. User prompts should be sanitized. Add prompt injection detection notes.

---

## Edge Case 10: No Clear Success Criteria

**Symptom**: User cannot articulate what a successful workflow run looks like.

**Resolution**: Define proxy metrics:
- Task completion rate (%)
- Average quality score (1-5)
- Human intervention rate
- Average latency
- Cost per successful run

Document these as "initial success criteria" with a note to validate and refine after 100+ runs.

---

## Failure Mode Matrix

| Failure Mode | Detection | Severity | Retry Strategy | Escalation |
|-------------|-----------|----------|---------------|------------|
| Agent timeout | >30s no response | Medium | Retry 2x with 5s backoff | Log warning, continue if optional |
| Invalid output schema | JSON parse fails | High | Retry with stricter prompt | Human review |
| API quota exceeded | 429 response | High | Exponential backoff, 3 retries | Alert ops team |
| Empty agent output | Null/empty response | High | Retry with rephrased prompt | Human review |
| Cascading failure | Agent C fails due to Agent A error | Critical | Halt workflow | Full incident review |
| Input validation failure | Malformed user input | Low | Ask user to re-input | N/A (user-facing) |
