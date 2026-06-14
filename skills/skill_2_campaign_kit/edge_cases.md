# Campaign Kit — Edge Cases & Failure Modes

## Edge Case 1: Missing Brand Guidelines

**Symptom**: User wants campaign assets but has no defined brand colors, fonts, or voice.

**Resolution**: Propose default guidelines based on their industry and product type. Ask: "What 3 words describe your brand?" to derive a tone. Generate a "brand light" direction and flag in the deliverable that this should be validated against actual brand guidelines.

---

## Edge Case 2: Lumi Is Unavailable

**Symptom**: ToolRequestHelp(Lumi) fails or Lumi cannot generate the requested image style.

**Resolution**: 
1. Retry with simplified prompt (remove style references)
2. If still fails, generate detailed text descriptions of what the images should look like
3. Flag the visual assets as "requires manual creation" in the asset manifest
4. Provide the image brief (composition, colors, dimensions) for a human designer

---

## Edge Case 3: Sonic Is Unavailable

**Symptom**: ToolRequestHelp(Sonic) fails or cannot generate the requested video/sound.

**Resolution**:
1. Retry with simplified motion direction
2. If still fails, provide detailed storyboard and audio direction as text
3. Flag motion assets as "requires manual production"
4. Include technical specs (frame rate, resolution, duration, BPM for music)

---

## Edge Case 4: Inappropriate or Unsafe Content

**Symptom**: Generated copy, images, or video contain offensive, unsafe, or policy-violating content.

**Resolution**:
1. Reject the output and log the issue
2. Check the prompt for problematic framing and revise
3. Add content safety guardrails to prompts (e.g., "do not generate harmful stereotypes")
4. If patterns persist, abort and recommend human copywriting/design

---

## Edge Case 5: Copy-Visual Misalignment

**Symptom**: The generated copy says one thing but the visuals show something different.

**Resolution**:
1. Cross-reference the key message from the brief against both copy and image descriptions
2. Regenerate the mismatched asset with a unified prompt referencing the one-line concept
3. Add a validation step: "Does this visual reinforce the headline?"

---

## Edge Case 6: Platform Constraint Violations

**Symptom**: Generated video is 90s but platform limit is 60s, or image is wrong aspect ratio.

**Resolution**:
1. Validate all assets against the platform specs table (see architecture.md)
2. Regenerate any violating assets with correct specs
3. Add a pre-validation step before generation

---

## Edge Case 7: Budget Overrun

**Symptom**: Total generation cost exceeds user's budget.

**Resolution**:
1. Identify the most expensive asset types (usually video)
2. Suggest generating fewer variants or lower resolution
3. Optimize: still images instead of video, shorter clips, fewer iterations
4. Report estimated cost before generation if budget is tight

---

## Edge Case 8: Language/Locale Mismatch

**Symptom**: Copy is generated in wrong language or uses culturally inappropriate references.

**Resolution**:
1. Always confirm the target language and locale in Phase 1
2. Generate copy in the specified language
3. Check for culturally specific references and flag them
4. Recommend local human review for non-English campaigns

---

## Edge Case 9: Generator Refuses Content (Safety Filters)

**Symptom**: Image or video generator refuses the prompt due to content policy.

**Resolution**:
1. Review the prompt against content policies
2. Rephrase to be within guidelines while preserving creative intent
3. If the concept fundamentally violates policy, suggest an alternative creative direction
4. Document the refusal in the campaign notes

---

## Edge Case 10: Inconsistent Visual Style Across Assets

**Symptom**: Social posts, banner, and video all look like they're from different campaigns.

**Resolution**:
1. Ensure all Lumi prompts reference the same brand guidelines
2. Regenerate the outlier assets with explicit style references
3. Use a "reference image" approach — generate one hero asset first, then use it as a style reference for all others

---

## Failure Mode Matrix

| Failure Mode | Detection | Severity | Action | Escalation |
|-------------|-----------|----------|--------|------------|
| Lumi unavailable | ToolRequestHelp fails | High | Provide image brief text | Manual design |
| Sonic unavailable | ToolRequestHelp fails | High | Provide storyboard text | Manual production |
| Content policy violation | Generator refusal | High | Rephrase prompt | Creative director review |
| Budget exceeded | Cost > limit | Medium | Reduce scope/variants | Client approval |
| Wrong format/size | Manifest check | Medium | Regenerate with correct specs | Quality check |
| Copy-visual mismatch | Manual review | Medium | Regenerate outlier asset | Creative review |
| Language error | User complaint | High | Regenerate in correct language | Localization review |
