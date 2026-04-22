# daily-rhythm

Three commands that bracket your workday. No external tools required.

## What it does

- `/daily-start` opens today's log file, asks for your top focus, lists carryover tasks from yesterday.
- `/done` appends a completion entry, optionally suggests the next task to work on.
- `/daily-end` wraps up the day, lists what shipped, seeds tomorrow.

## When to use it

- You want a simple, file-based daily rhythm in Claude Code.
- You do not want to set up Jira, Linear, or any external tool first.
- You want a log you can grep or share later.

## Install

```bash
cp -r daily-rhythm/commands/* ~/.claude/commands/
mkdir -p daily-log/
```

## Example run

```
> /daily-start
Good morning. I read yesterday's log. Two tasks carried over: "finish pricing deck"
and "call Acme for Q2 renewal". Today's focus?

> "finish pricing deck and ship one email to Acme"

Logged. Top tasks for today:
1. Finish pricing deck
2. Email Acme re: Q2 renewal

Focus written to daily-log/2026-04-22.md.

> /done finished pricing deck v2

Nice. Logged at 11:04.
Next suggested task: Email Acme re: Q2 renewal.
Want to start it?

> /daily-end

Here's today:
- Shipped: pricing deck v2, Acme email
- Carryover: none
- Tomorrow's seed: review Acme's reply before noon

Written to daily-log/2026-04-22.md. See you tomorrow.
```

## Customize

- Change the log directory name by editing the `daily-log/` path in each command.
- Add categories (wins, blockers, learnings) by extending the evening section template.
- Wire it to your task system by reading the log file from a hook or a separate sync script.

## Credit

Extracted from Protectyr Operating System v3 workflow and generalized for community use. Original Protectyr version is Jira-integrated and persona-voiced; this public version is intentionally minimal so any founder can fork.
