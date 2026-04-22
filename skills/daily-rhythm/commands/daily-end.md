---
description: Close the workday. Summarize what shipped, carry over, seed tomorrow.
---

# /daily-end

When the user invokes `/daily-end`:

1. Resolve today's date as `YYYY-MM-DD`.
2. Open `daily-log/YYYY-MM-DD.md`. If it does not exist, tell the user there is nothing to close and stop.
3. Read the `## Morning` section (top tasks) and the `## Log` section (completions).
4. Compute:
   - **What shipped**: the list of completions from the log.
   - **What carries over**: top tasks from the morning that do not appear as completed in the log.
5. Ask the user in their voice: "What is tomorrow's seed in one sentence?"
6. Write to the `## Evening` section:

```markdown
## Evening
- What shipped:
  - <list>
- What carries over:
  - <list or "none">
- Tomorrow's seed: <user's answer>
```

7. Print a 4-line summary and say "See you tomorrow."

## Constraints

- Do not overwrite an existing evening section without asking.
- If the carryover list is long (more than 3 items), mention it explicitly so the user is not surprised tomorrow morning.
- Keep the prompt to one question ("tomorrow's seed"). No multi-part forms.
