# Flow Builder — Iteration Notes

## v1.0 — Initial Release

**Date**: 2025-01-15
**Changes**: Initial skill definition

### Known Limitations
- No built-in visualization of the workflow DAG (user must render Mermaid manually)
- Cost estimation is based on rough token counts — needs real-world calibration
- Template discovery relies on user having access to `ToolGetTemplates`
- No automated testing harness yet — validation is manual review only

### Feedback from Initial Testing

| Issue | Severity | Resolution |
|-------|----------|------------|
| Users skip Discovery phase | Medium | Made Discovery mandatory with sign-off gate |
| Prompts too generic | High | Added full prompt templates to examples |
| Missing error handling for API failures | Medium | Added failure mode matrix |
| No budget tracking | Low | Added cost analysis section to output |

---

## v1.1 — Planned

**Target**: Add workflow visualization

### Improvements
- [ ] Auto-generate Mermaid diagram from agent definitions
- [ ] Add JSON schema validation for data contracts
- [ ] Create a "quick start" template for common workflow patterns
- [ ] Add security review checklist for workflows handling PII

### Known Issues
- Edge case 4 (schema mismatch) detection is still manual
- Cost estimation doesn't account for retry costs
- No support for dynamic agent routing based on output content
