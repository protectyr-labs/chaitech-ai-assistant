---
description: Read the full filled state, flag gaps, capture per-section confidence, suggest next step.
---

# /brand-review

Quality gate. Use any time during the workshop to see where things stand, what is missing, and how confident the founder is per section. Confidence ratings are passed to *Find My Brand DNA* on handoff so the AI synthesis knows where to probe deepest.

## Behavior

1. Check that `brand-workshop/STATE.md` exists. If not, tell the user to run `/brand-start` first and stop.

2. Read every section (1–15) and produce a status table:

   ```
   | #  | Exercise                   | Status         | Notes                       |
   |----|---------------------------|----------------|-----------------------------|
   | 1  | Stakeholders               | ✅ complete    | 3 stakeholders captured     |
   | 2  | Needs (F/E/S)              | ⚠ partial     | Social needs missing for #2 |
   | 3  | Purpose Archetype          | ✅ complete    | Reduce Friction (primary)   |
   | 4  | Purpose Sentence (long)    | ✅ complete    |                             |
   | 5  | Purpose Words              | ⚠ partial     | Short sentence missing      |
   | 6  | Superpower                 | ❌ not started |                             |
   | 7  | Strategic Cascade          | ❌ not started |                             |
   | 8  | Strategic Pillars          | ❌ not started |                             |
   | 9  | Origin Story               | ❌ not started |                             |
   | 10 | Customer Transformation    | ❌ not started |                             |
   | 11 | Brand IS / IS NOT          | ❌ not started |                             |
   | 12 | Central Brand Tension      | ❌ not started |                             |
   | 13 | What We Will NOT Do        | ❌ not started |                             |
   | 14 | Values (opt, Catalyst 17)  | ❌ skipped     | Optional                    |
   | 15 | Brand Movement (opt)       | ❌ skipped     | Optional                    |
   ```

   Status values:
   - ✅ complete — section has substantive content in every required field
   - ⚠ partial — section has *some* content but a required field is empty or single-line
   - ❌ not started — section is at template default
   - ❌ skipped — optional section, not blocking

3. Below the table, surface up to 3 specific issues that would weaken the deck if exported now. Examples:

   > - Section 4 field "How we make money sustainably" is "TBD" — a purpose statement without a viability line is a hobby. Revisit before export.
   > - Section 7 (cascade) "Where to play" has no exclusion. Cascades fail without a "will not play" line.
   > - Section 8 has 5 pillars; the cap is 4. Cut one before export.

4. **Confidence calibration.** If the user has run `/brand-review` for the first time and at least 4 sections are `✅ complete`, ask:

   > "Quick calibration. Rate your confidence in each block — High, Medium, or Low.
   > - Define (sections 1–4): how solid?
   > - Narrate (sections 9, 10, 11): how solid?
   > - Affinity (sections 6, 7, 8, 12, 13): how solid?"

   Capture the answers and write them to section 16 of `STATE.md`:

   ```markdown
   ## 16. Confidence Calibration (per block)

   - **Define (1–4):** High | Medium | Low
   - **Narrate (9–11):** High | Medium | Low
   - **Affinity (6, 7, 8, 12, 13):** High | Medium | Low
   - **Last reviewed:** YYYY-MM-DD
   ```

   If section 16 already has values, don't ask again — just show the existing ratings in the review and ask "Still accurate, or do you want to update?"

5. Recommend the **next single action**. One command. One sentence.

   > "Recommended next: `/brand-superpower` (section 6 is empty and the cascade depends on it)."

   If the workbook is complete, the recommended next action is:

   > "Recommended next: `/brand-export` to write your draft, then take it into *Find My Brand DNA* for the AI synthesis."

6. Stop. Do not run the next command automatically.

## Confidence calibration · why this matters

Confidence ratings travel with the export into the *Find My Brand DNA* app. Sections marked Low are where the AI synthesis is instructed to probe deepest. Sections marked High are accepted at face value. Calibrating honestly here saves time downstream.

If the founder is using the skill standalone (not handing off to the app), the confidence ratings still help — they tell the founder which sections to revisit when their brand evolves.

## Constraints

- Do not invent issues. If the workbook is fine, say so in one line.
- Do not rate the *quality* of the founder's answers. The review is about completeness, not editorial judgment. (Quality conversations belong inside each exercise.)
- Keep the whole review under 30 lines of output. The founder is here to act, not read a report.
- Do not ask for confidence ratings if fewer than 4 sections are complete — there's not enough material to calibrate against yet.
- Do not mention *Find My Brand DNA* by name unless the user has not already been pointed at it; the SKILL.md has the canonical mention.
