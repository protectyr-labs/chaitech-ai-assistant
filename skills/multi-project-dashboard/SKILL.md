---
name: multi-project-dashboard
description: |
  Aggregates status across sibling project directories into a single HTML
  command center. Detects signal files in each project, reads them, and
  renders a visual overview with freshness indicators. Use when you run
  several projects from one machine and want a single glance view.
license: MIT
compatibility: claude-code
allowed-tools:
  - Read
  - Write
  - Glob
  - Bash
---

# Multi-Project Dashboard

A skill that walks your sibling project directories, reads signal files, and produces a single HTML dashboard showing the state of everything.

## When to use it

- You run 3 or more projects side by side in one parent directory.
- Each project has some form of status (git branch, last deploy, open tasks, open PRs).
- You want to open one HTML file in the morning and see all projects at once.

## How it works

1. The skill is given a parent directory (for example `~/Documents/`).
2. It globs for sibling directories that contain a marker file. The default marker is `.dashboard-signal.json`, but you can configure it.
3. For each signal file found, it reads:
   - Last updated timestamp.
   - Current phase or milestone name.
   - Open issues or blockers.
   - Any custom fields the project writes.
4. For directories that do not have a signal file, the skill falls back to reading the project's main README or a known status file if one exists.
5. Output is a single HTML page with one card per project, freshness badges (green within 1 hour, yellow within 24 hours, red beyond), and a summary header.

## Signal file format

Each project writes a small JSON file to its own root:

```json
{
  "project": "my-project",
  "phase": "growth",
  "last_updated": "2026-04-22T09:15:00-04:00",
  "top_focus": "ship landing page redesign",
  "blockers": [],
  "links": {
    "repo": "https://github.com/...",
    "prod": "https://..."
  }
}
```

The skill reads this and renders it into a card. Projects write their own signal files from their own workflows (for example a post-commit hook or a daily script).

## Install

```bash
cp -r multi-project-dashboard ~/.claude/skills/
```

Then from Claude Code:

```
> /dashboard-update
```

The skill writes `DASHBOARD.html` to your parent directory.

## Customize

- Change the marker file name in `SKILL.md`.
- Add or remove cards by editing the HTML template.
- Change the freshness thresholds if you want different color cutoffs.

## Credit

Generalized from the Protectyr `master-dashboard` skill.
