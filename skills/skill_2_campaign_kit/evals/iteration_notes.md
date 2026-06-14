# Campaign Kit — Iteration Notes

## v1.0 — Initial Release

**Date**: 2025-01-15
**Changes**: Initial skill definition

### Known Limitations
- No automated brand compliance checker — brand alignment is manual review
- Image prompts are text-only — no visual reference injection yet
- Video direction is text-based — no storyboard generation
- Cost estimation is approximate — real costs depend on Lumi/Sonic pricing tiers
- No A/B variant management — variants are listed but not tracked systematically

### Feedback from Initial Testing

| Issue | Severity | Resolution |
|-------|----------|------------|
| Users forget to specify platform formats | High | Added platform specs table to architecture.md |
| Lumi prompts too vague | High | Added structured prompt templates with required fields |
| Missing cost tracking | Medium | Added cost report to output |
| No fallback when Lumi/Sonic unavailable | High | Added fallback procedures to edge_cases.md |
| Copy inconsistent across channels | Medium | Added unified creative brief requirement in Phase 1 |

---

## v1.1 — Planned

**Target**: Add visual reference injection and brand compliance checker

### Improvements
- [ ] Add automated brand color compliance check for generated images
- [ ] Support reference image injection in Lumi prompts
- [ ] Add storyboard generation for video assets (frame-by-frame text descriptions)
- [ ] Create cost estimator before generation (user sees estimated cost before commit)
- [ ] Add A/B variant tracking with performance projection

### Known Issues
- No direct integration with Lumi/Sonic — relies on ToolRequestHelp
- Cannot batch-generate assets in parallel (still sequential per phase)
- No template library for common campaign types (launch, seasonal, retargeting)
