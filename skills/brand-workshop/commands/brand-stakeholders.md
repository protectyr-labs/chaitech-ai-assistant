---
description: Exercise 1 — list all stakeholders, then pick the top 3.
---

# /brand-stakeholders

Exercise 1 of the Brand Workshop. Two halves: cast a wide net, then trim to three.

## Pre-checks

- If `brand-workshop/STATE.md` does not exist, tell the user to run `/brand-start` first and stop.
- Read the existing `## 1. Stakeholders` section. If it is already filled, ask the user whether to revise it or move on.

## Half A — All Stakeholders

1. Explain in one sentence what a stakeholder is, with examples:

   > "A stakeholder is anyone whose needs your brand has to answer to. Customers are obvious. But also: employees, suppliers, your investors, the regulator, the city, your family, the competitor you respect, even the planet. Cast wide first; we trim later."

2. Ask the user to list as many as they can think of. Encourage at least 10. Suggest categories if they get stuck (users, buyers, employees, partners, suppliers, owners, family, community, regulators, press, planet).

3. **Use existing context first.** Before asking, scan the workspace for `README.md`, `pitch.md`, `about.md`, `docs/`, or any pitch deck. If you find named partners, customer types, or investors, propose them as starting items in the list.

4. Write the list to `brand-workshop/STATE.md` under `### All stakeholders` as a bulleted list.

## Half B — Top 3

1. Ask:

   > "Now — of everyone on that list, which three would your brand fail without? Not the most numerous. The most vital. Pick three."

2. If the user struggles, offer a heuristic:

   > "Three useful tests: (1) If this stakeholder walked away tomorrow, would the business survive a year? (2) Whose decision are we trying to influence first? (3) Whose praise do we most want?"

3. For each of the three, ask the user for a one-sentence description — not a job title, a specific human:

   > "Not 'small businesses' — describe the actual person. 'A 35-person dental clinic owner whose IT manager is also their bookkeeper' is what we want."

4. Write the three to `brand-workshop/STATE.md` under `### Top 3` as:

   ```markdown
   1. **<Stakeholder name / archetype>** — <one-sentence description>
   2. ...
   3. ...
   ```

## Wrap

Confirm in one line:

> "Written to section 1 of `brand-workshop/STATE.md`. Next is `/brand-needs` — what each of these three needs to *do*, *feel*, and *signal*."

Stop. Do not auto-run the next exercise.

## Constraints

- Do not pick the top 3 for the user. Offer the heuristic if they freeze, but the choice is theirs.
- Do not allow more than 3 in Half B. If the user insists on 4+, ask them to rank and pick the top 3 — the rest can stay in `### All stakeholders`.
- Never assume "customers" is the answer to top 3 without testing it. For B2B2C and platform businesses, the most vital stakeholder is often a developer, a regulator, or a channel partner.
