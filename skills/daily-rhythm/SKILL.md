---
name: daily-rhythm
description: |
  Founder daily loop for Claude Code. Three commands that bracket your workday:
  /daily-start in the morning (triage, top task), /done after finishing work
  (log, celebrate, suggest next), /daily-end in the evening (wrap-up, tomorrow
  seed). File-based. No external dependencies.
license: MIT
compatibility: claude-code
allowed-tools:
  - Read
  - Write
  - Edit
  - Glob
---

# Daily Rhythm

A three-command workflow for solo founders and operators who want Claude Code to bracket their workday with structure they do not have to think about.

## When to invoke

- User types `/daily-start` in the morning.
- User types `/done` or `/done <task>` after finishing a piece of work.
- User types `/daily-end` in the evening.

## Data model

One plain-text log file per day at `daily-log/YYYY-MM-DD.md`. The file has three sections:

```markdown
## Morning (written by /daily-start)
- Today's focus: <one sentence>
- Top tasks: <list>

## Log (appended to by /done)
- 09:42 — finished <task>
- 11:18 — finished <task>

## Evening (written by /daily-end)
- What shipped: <list>
- What carries over: <list>
- Tomorrow's seed: <one sentence>
```

If the file does not exist when `/daily-start` runs, create it. Subsequent commands append to the existing file.

## Command behavior

See `commands/daily-start.md`, `commands/done.md`, `commands/daily-end.md` for full behavior. Each command reads the current day's log file, performs its action, and writes back.

## Install

Copy `commands/*.md` to your Claude Code commands directory:

```bash
cp commands/*.md ~/.claude/commands/
# or for a project
cp commands/*.md /path/to/project/.claude/commands/
```

Then invoke the three commands from Claude Code.

## Optional hooks

The skill works standalone. If you want to wire it to external systems later (Jira, Linear, Todoist, Notion), add a hook in your own config that reads the daily log file and syncs tasks. The skill does not depend on any external service.
