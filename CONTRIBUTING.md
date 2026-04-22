# Contributing

Anyone in the ChaiTech community can contribute a skill. This guide gets you from "I use this thing in Claude Code every day" to "it's a shareable skill in the repo" in about 10 minutes.

## What makes a good skill for this repo

- You actually use it.
- It solves one clear problem.
- It does not contain secrets, client data, or anything you wouldn't hand a stranger.
- It is generic enough that another founder could install it without knowing your business.

## The 10-minute extraction process

### 1. Find the skill you want to share

It is usually already somewhere in your local Claude Code config, for example:

```
~/.claude/skills/<name>/
.claude/skills/<name>/   (inside a specific project)
.claude/commands/<name>.md
```

### 2. Copy it to a working directory

```bash
cp -r ~/.claude/skills/my-skill ./skills-draft/my-skill
```

### 3. Scrub secrets and business specifics

Read every file. Remove:

- Client names, project code names, real revenue figures.
- API keys, tokens, webhook URLs, SSH hosts.
- File paths that only exist on your machine.
- Assumptions about specific tools (for example Jira, PostgreSQL, Stripe) if the skill could work without them.

Replace with generic placeholders like `<your-client>`, `<your-tool>`, `<your-project-root>`.

### 4. Structure the skill directory

Most skills in this repo follow this layout:

```
skills/<name>/
  SKILL.md        # the Claude Code manifest (frontmatter + body)
  README.md       # human explanation, install steps, examples
  (optional) commands/, agents/, state/, templates/
```

The `SKILL.md` frontmatter should include:

```yaml
---
name: my-skill
description: |
  One sentence on what the skill does. Add a second line with when to trigger.
license: MIT
compatibility: claude-code
---
```

### 5. Write the README.md

Answer these four questions in order:

1. **What does this do?** (two sentences)
2. **When should I use it?** (bullet list of triggers)
3. **How do I install it?** (exact commands)
4. **What's an example run?** (1 short transcript or walkthrough)

### 6. Open a pull request

```bash
git clone https://github.com/<owner>/chaitech-claude-skills-seed.git
cd chaitech-claude-skills-seed
cp -r ../skills-draft/my-skill skills/
git checkout -b add-my-skill
git add skills/my-skill
git commit -m "Add my-skill"
git push origin add-my-skill
```

Open the PR against `main`. A steward reviews for secrets, scope, and clarity. Usually merged within a few days.

## Worked example: `daily-rhythm`

The `skills/daily-rhythm/` directory shows what a clean contribution looks like. It started as a Protectyr-internal workflow tied to Jira. The extraction steps applied:

- **Stripped:** Jira CLI calls, Protectyr persona labels, real engagement names, revenue metrics.
- **Replaced with:** plain-text log file (`daily-log.md`), generic task states (`todo`, `doing`, `done`), and optional hooks you wire up yourself if you want Jira or Linear later.
- **Kept:** the rhythm itself — morning triage, task completion, end-of-day close.

Compare this with any founder's own morning routine and you see the pattern: pick the structure, leave the business specifics behind.

## Contribution checklist

Before you open a PR, verify:

- [ ] No client names, API keys, or personal paths remain.
- [ ] `SKILL.md` has valid frontmatter (`name`, `description`, `license`).
- [ ] `README.md` answers the four questions (what, when, how, example).
- [ ] `LICENSE` is present in the skill directory if it differs from repo default (MIT).
- [ ] You actually used this skill in your own work recently.

## Not a developer?

Open an issue using the "Submit a skill idea" template. Describe:

1. What problem you want Claude to solve.
2. How you currently do it manually.
3. Whether you want the skill to run in one project or across all of them.

A steward will turn it into a real skill and credit you as the idea author.

## Credit and attribution

Every contribution is credited in the skill's README and repo commit history. If you adapt an external skill, cite the original author. Forking permissive-license skills is welcome with credit; republishing without credit is not.

## Steward

Alexander Madaniev, ChaiTech Cohort 7, founding steward during Cohort 7.
