---
description: Open the Brand Workshop. Create STATE.md, name the business, route to Exercise 1.
---

# /brand-start

When the user invokes `/brand-start`:

1. Check if `brand-workshop/STATE.md` already exists.
   - If yes: read the **Meta** section, summarize where the user left off, and ask whether to resume or restart. If restart, move the existing file to `brand-workshop/STATE-archived-YYYY-MM-DD.md` before continuing.
   - If no: continue.

2. Greet the user briefly (one to two sentences). Do not lecture. Then ask one question:

   > "Before we start — what are we calling this business in the workbook? It does not have to be the final name."

3. When the user answers, create `brand-workshop/STATE.md` from the template at `templates/brand-state.md` (in this skill folder). Replace the placeholder `<Company Name>` with the user's answer. Set `Started: YYYY-MM-DD` to today. Set `Status: in-progress`.

4. Print one short confirmation (one to two lines) — file created, what comes next — then offer the user a choice:

   > "Exercise 1 is Stakeholders — the people whose needs your brand answers. Want to do it now (`/brand-stakeholders`), see the full menu first (`/brand-review`), or come back later?"

5. Stop. Do not auto-run the next exercise.

## Constraints

- Never invent a business name. If the user has not given one, do not create the file.
- Do not lecture about brand strategy, Roger Martin, or methodology. The user is here to do the work, not read theory.
- If `brand-workshop/` does not exist as a directory, create it before writing the file.
- The state file is markdown, plain text, hand-editable. Never lock it or stamp it with anything the user cannot edit.
