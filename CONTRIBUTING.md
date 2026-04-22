# How to share what you built

You do not have to be a coder, a developer, or a GitHub person to share something here. If you built a little thing with Claude that made your week easier, someone else will benefit from it. The only goal of this page is to make sharing feel easy.

## Three ways to share

### 1. You have something to share and you know how to use GitHub

Lovely. Here is the fast path.

1. Fork this repository.
2. Copy your helper into `skills/<your-helper-name>/`.
3. Scrub any client names, API keys, or personal folder paths from the files. (See the short checklist below.)
4. Write a short `README.md` answering the four questions (what, who, how, example).
5. Open a pull request. A steward reviews for leaks and clarity, then merges.

Total time: usually about ten minutes.

### 2. You have something to share and GitHub looks scary

No problem. Do this instead.

- Open a [Discussion](https://github.com/protectyr-labs/chaitech-ai-assistant/discussions/new?category=ideas) in the "Ideas" category and paste what you built, or describe it in your own words, or attach a text file.
- A steward will turn it into a proper helper, credit you as the idea author, and tell you when it is live.

You do not need a GitHub account to read the repo, but you do need one (free) to open a Discussion. Making an account takes two minutes. We promise.

### 3. You only have an idea, not a working helper

Even better in some ways. Open a Discussion in the "Ideas" category and describe:

- What problem you want Claude to solve for you.
- How you do it today (by hand, or not at all).
- Whether you already tried and got stuck.

Ideas with that much context turn into helpers quickly.

---

## The short checklist before you share

Before you paste your helper into a pull request or Discussion, read it through once and remove:

- [ ] Client names, company names, project code names.
- [ ] Real numbers you would not want public (revenue, customer counts, personal salaries).
- [ ] API keys, tokens, passwords, SSH hosts.
- [ ] File paths that only exist on your machine (like `/Users/you/...`).
- [ ] Any reference to a paid service that the helper assumes you have (or mark that dependency as optional).

If in doubt, ask in a Discussion first. A steward will tell you if anything stands out.

---

## What a good helper looks like

Read an existing helper to see the shape. The "Your day, bracketed" helper is the simplest and cleanest example to copy from:

→ [skills/daily-rhythm/](skills/daily-rhythm/)

A good helper has:

- A short `README.md` in plain language (what, who, how, example).
- A clear list of what the user types and what Claude does.
- One minimal install path (two copy-paste commands at most).
- Credit to the original author (you).

A good helper avoids:

- Jargon without a definition.
- "Just run this" leaps.
- Assumptions about what the reader already knows.

---

## Contribution credit

Every helper page credits the author by name or handle. Every Discussion-seeded helper credits the idea author. If you want to stay anonymous, say so in the Discussion and we use "anonymous cohort founder."

---

## Questions

Open a [Discussion in the Q and A category](https://github.com/protectyr-labs/chaitech-ai-assistant/discussions/new?category=q-a) and ask. The steward or another cohort member will answer.

## Steward

Alexander Madaniev, ChaiTech Cohort 7. Founding steward during Cohort 7.
