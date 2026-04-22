---
description: Start the workday. Open today's log, surface carryover, ask for focus.
---

# /daily-start

When the user invokes `/daily-start`:

1. Resolve today's date in local time as `YYYY-MM-DD`.
2. Check if `daily-log/YYYY-MM-DD.md` exists.
   - If yes: read it, summarize the morning section, stop.
   - If no: continue.
3. Check if yesterday's file `daily-log/YYYY-MM-(DD-1).md` exists.
   - If yes: read the evening section, extract any "carries over" items.
   - If no: there is no carryover.
4. Create today's file with the morning template:

```markdown
# Daily log — YYYY-MM-DD

## Morning
- Carryover from yesterday: <list or "none">
- Today's focus: <waiting for user>
- Top tasks:
  1. <waiting>
  2. <waiting>
  3. <waiting>

## Log

## Evening
```

5. Ask the user (in their voice, not a form):
   - "What is today's focus in one sentence?"
   - "Top 1 to 3 tasks?"
6. Write the answers back into the morning section.
7. Print a short confirmation: focus + top tasks, path to log file.

## Constraints

- Do not invent carryover items. If yesterday's file is missing or empty, say so.
- Do not write to the log section yet (that is `/done`).
- Keep the morning conversation to at most two questions.
