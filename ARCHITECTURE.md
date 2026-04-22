# Architecture

Design notes for the ChaiTech Claude Code Commons.

## Problem statement

Founders in Cohort 7 left the first Claude Code session wanting skills to install. There was no shared, curated place to find them. Each founder was researching independently, often duplicating effort, and the knowledge did not accumulate across cohorts.

## Goal

Create a minimal, durable place where:

1. A cohort member can find useful Claude Code skills in under two minutes.
2. A cohort member can contribute a skill they wrote in under ten minutes.
3. Future cohorts inherit what prior cohorts built, without institutional overhead.

## Non-goals

- A marketplace. No paid skills, no vendor directory.
- A framework. We ship plain Claude Code skills, no meta-abstraction.
- A commitment. Contributors own their own work. Stewards keep the lights on.

## Shape

The repo has exactly two top-level directories for content:

```
skills/     # original contributions (code + docs, MIT)
curated/    # linked external skills (credit + source URL)
```

Everything else is convention:

```
.github/    # issue and PR templates
docs/       # banner asset, any long-form docs
```

## Two sections, one repo

A tempting alternative is to put everything in one `skills/` directory and tag some as "external" through metadata. Rejected. Separate directories make the distinction visible at a glance. Contributors are never confused about whether they are about to republish someone else's work.

- `skills/<name>/` — code lives here. Self-contained. MIT.
- `curated/README.md` — single file. Each entry is a short description with source URL, category, and credit. Installing happens from the source repo, not this one.

## Contribution flow

```
Cohort member has a skill they use
          │
          ├─ fork repo, follow CONTRIBUTING.md
          │       │
          │       └─ scrub secrets, write short README, open PR
          │
          └─ not a dev: open "Submit a skill idea" issue
                  │
                  └─ steward packages it into a PR, credits the idea author
```

## Sanitization as the load-bearing rule

The most likely way this repo does harm is by leaking a contributor's client data, API keys, or private paths. Every pull request is scanned for these patterns before merge. The steward's primary job is review, not curation.

Sanitization checklist (enforced in PR template):

- No client names, project code names, revenue figures.
- No API keys, tokens, webhook URLs, SSH hosts.
- No absolute file paths specific to the contributor's machine.
- No assumed dependencies on paid services (make those optional, with clear opt-in).

## Governance

- **Founding steward.** Alexander Madaniev, Cohort 7.
- **Review model.** One reviewer required for merge. Stewards can merge their own contributions if a second reviewer approves.
- **Ownership.** Interim home: `protectyr-labs`. Target home (if ChaiTech adopts): `chaitech` GitHub organization. The repo is structured to make transfer a single operation with no history loss.
- **License default.** MIT. Contributors may declare a different permissive license per skill (Apache-2.0, BSD-3-Clause) but copyleft is rejected to keep the repo uniformly permissive.
- **End of cohort.** If the steward rotates out, a replacement is named before the transition. No orphaned repo.

## What this is not

- **Not a framework.** We ship plain Claude Code skills that work with the stock runtime. Anyone can install any skill here by copying the directory into `~/.claude/skills/`.
- **Not a CI/CD pipeline.** There is no build step. The repository is read by humans and by Claude Code. If we ever need automated checks (for secrets, for schema), we add a minimal GitHub Action and keep the rest plain.
- **Not exclusive to ChaiTech.** The seed is seeded by Cohort 7 but the license and the contribution model are open. Anyone can fork, anyone can use, cohort members just happen to be the first contributors and the natural audience.

## Future work

- A minimal schema check on `SKILL.md` frontmatter (name, description, license present).
- A lightweight secrets scan on pull requests.
- A `curated/` verification script that checks external links for 404s monthly.
- A short "skill of the month" highlight, published by the steward as a GitHub Discussion.

None of these are required to make the repo useful today. They are listed here so future contributors know what has been considered.
