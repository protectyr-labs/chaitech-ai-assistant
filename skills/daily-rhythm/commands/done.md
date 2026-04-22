---
description: Log a completed task. Optionally suggest what to do next.
---

# /done

When the user invokes `/done [task description]`:

1. Resolve today's date as `YYYY-MM-DD` and current local time as `HH:MM`.
2. Open `daily-log/YYYY-MM-DD.md`. If it does not exist, create it using the template from `/daily-start`.
3. Parse the argument:
   - If the user typed `/done <description>`, use that string.
   - If the user typed just `/done`, ask what they finished in one sentence.
4. Append to the `## Log` section:

```markdown
- HH:MM — finished <description>
```

5. Read the `## Morning` section and look at the top tasks list:
   - If the completed task matches one of the top tasks, mark it internally.
   - If there are remaining top tasks, suggest the next uncompleted one.
   - If all top tasks are complete, congratulate the user and suggest a short break or a bonus task.
6. Print: "Logged at HH:MM. Next suggested: <task or nothing>. Want to start it?"

## Constraints

- Never delete entries from the log.
- Never rewrite the morning focus without explicit user request.
- Keep the response to 2 lines unless the user asks for more.
