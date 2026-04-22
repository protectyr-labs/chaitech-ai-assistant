# multi-project-dashboard

One HTML page that shows the status of every project you work on. Opens in a browser. No backend.

## What it does

Walks your parent directory, finds sibling projects, reads a small status file each project maintains, and generates a single dashboard showing every project at once with freshness indicators.

## When to use it

- You run more than one project and context-switch daily.
- You want to see "where is everything" in under 10 seconds.
- You want the dashboard to be just an HTML file you can open or share.

## Install

```bash
cp -r multi-project-dashboard ~/.claude/skills/
```

From Claude Code:

```
> Regenerate my multi-project dashboard
```

or invoke the skill by name.

## Example output

One card per project with:

- Project name and phase.
- Top focus for the day.
- Freshness badge (green, yellow, red) based on last update time.
- Quick links to the repo and production URL.

## Customize

See `SKILL.md` for signal file format, freshness thresholds, and marker file configuration.

## Credit

Generalized from the Protectyr `master-dashboard` skill.
