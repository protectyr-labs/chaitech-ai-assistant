<div align="center">

<img src="../../docs/assets/skill-multi-project-dashboard.svg" alt="A dashboard window showing four project tiles" width="100%"/>

</div>

# All your projects, one view

> If you juggle more than one business or project, this turns them into a single friendly dashboard that opens in your browser.

## What this does, in plain English

You run multiple projects out of the same computer folder. Each project has its own status: "we are in the build phase," "Q2 launch is in two weeks," "stuck waiting on legal." Right now that status lives in your head or scattered across notes.

This helper walks your folders, reads a tiny status file from each project, and builds a single HTML page with one friendly card per project. Freshness badges show you which projects were updated recently and which are going stale. You open the page in your browser, glance at it for ten seconds, and you know where everything stands.

## Who is this for?

- Founders running more than one business or side project.
- Consultants juggling three or four client engagements at once.
- Anyone who wants a one-page "state of everything" in the morning.

## What you need before using it

- Claude Code installed. (If you have not done this yet, see [the main page](../../README.md#where-do-i-start-if-i-have-never-done-this-before).)
- Each of your projects living as a subfolder in the same parent folder. For example:
  ```
  ~/Documents/
    project-one/
    project-two/
    project-three/
  ```

## How to install it (2 steps)

**Step 1.** Copy the helper into your Claude Code folder:

```bash
cp -r skills/multi-project-dashboard ~/.claude/skills/
```

**Step 2.** Open Claude Code and ask:

> Build me a multi-project dashboard from my Documents folder.

Claude writes an HTML file named `DASHBOARD.html` next to your projects. Open it in your browser.

## What using it looks like

Each project shows as a friendly card: project name, current phase, what you are focused on, when it was last updated. Projects updated in the last hour show a green badge. Within the last day, yellow. Older than that, a gentle "going stale" note.

## How projects tell the dashboard their status

Each project puts a small file called `.dashboard-signal.json` in its own folder. Example:

```json
{
  "project": "my-cool-business",
  "phase": "launch",
  "last_updated": "2026-04-22T09:15:00-04:00",
  "top_focus": "ship the landing page",
  "blockers": [],
  "links": {
    "repo": "https://github.com/...",
    "live": "https://my-cool-business.com"
  }
}
```

Your project writes this file whenever something changes. A simple way to keep it fresh is to have Claude update it at the end of the day as part of `/daily-end` (see the "Your day, bracketed" helper).

If a project does not have this file, the dashboard skips it. Adding one is a one-line instruction to Claude.

## Make it yours

- **Different freshness thresholds.** Green/yellow/red times can be changed in the HTML template.
- **Different parent folder.** The helper accepts any folder you point it at.
- **Different layout.** The HTML is one file. Edit it with Claude's help: "Rearrange the dashboard so the cards are in two columns, not three."

## Credit

Generalized from the Protectyr `master-dashboard` tool used to keep six side projects visible. The public version strips anything Protectyr-specific.
